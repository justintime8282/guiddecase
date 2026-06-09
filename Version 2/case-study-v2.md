# Guidde — Sales Operations Manager Case Study (v2)

**Author:** Justin [LAST NAME — fill before sending]
**Submission for:** Sales Operations Manager, guidde
**Theme:** A scalable Sales Ops system for a PLG-hybrid revenue motion — *automate what is objective, preserve human judgment where context matters.*

> **v2 note:** This version incorporates the review of the v1 drafts (see `/Version 1/review-findings.md`). The most important change is that the HubSpot build now explicitly accounts for tier-gating (Workflows/scoring/custom lifecycle stages are Professional features — built on the 14-day Pro trial), and the Part 3 dashboard now answers all four leadership questions, including revenue by motion.

---

## 0. Assumptions (stated up front)

The assignment asks for my **logic and assumptions**. Mine are:

1. **GTM motion:** guidde runs a **PLG-hybrid** motion — low-friction product adoption generates intent signals, and the revenue team converts the right users into qualified pipeline, customers, and expansion. It is not a pure outbound-enterprise motion.
2. **Product usage is a first-class qualification signal**, alongside (not instead of) traditional marketing/sales signals. The qualification model is anchored on a **Product-Qualified Lead (PQL)**.
3. **A person and a revenue opportunity are different objects.** One account can produce many signals, stakeholders, and over time multiple deals. So **lifecycle stage** (where is this *person*) and **deal stage** (where is this *opportunity*) are designed as separate-but-connected systems.
4. **Revenue ownership spans BDR, AE, and CS.** BDR qualifies and routes; AE owns the active deal; CS supports trial and owns the post-sale handoff and expansion signals.
5. **Deal creation is hybrid:** a human makes the qualification call, then the system creates and standardizes the deal ("judgment by human, creation by system").
6. **Outbound is a secondary on-ramp,** not the center of the model. It feeds the same qualification gate as PLG — one pipeline, two acquisition motions.
7. **HubSpot tier:** Workflows, custom lifecycle stages, and rotate-owner actions are **Sales Hub Professional** features; I built the automation on HubSpot's **14-day Sales Hub Pro trial** (see `hubspot-build-guide.md`). **Important tier nuance found during the build:** native **contact** lead scoring is a **Marketing Hub Professional** feature — *not* part of the Sales Hub trial. I therefore did **not** build a live score; the §1.2 score model is presented as design, and Workflow 1 implements the equivalent qualification logic with **direct product-activation triggers** (see §1.2 build note and §1.4). With a full Marketing + Sales Pro stack, the same model runs as a live `HubSpot Score` property and Workflow 1 simply branches on `HubSpot Score ≥ 50`. On a permanently-free seat, the rest degrades to manual stage updates + scheduled imports; fallbacks are noted where relevant.

---

## Part 1 — HubSpot Workflow & Automation Design

### 1.1 Lifecycle model (the person)

I manage the **contact lifecycle** separately from the deal pipeline:

**Subscriber → Lead → MQL → PQL → SQL → Opportunity → Customer**

`PQL` sits at the center because guidde's strongest intent comes from **product behavior**, not just form fills. A contact becomes more valuable not because they downloaded a PDF, but because they did something real in the product.

> **HubSpot reality check:** `PQL` is **not** a default HubSpot lifecycle stage and custom lifecycle stages require a paid tier. On the Pro trial I add `PQL` as a custom stage between MQL and SQL. On free, I would represent PQL with a contact property + active list instead of a true lifecycle stage. (See build guide.)

### 1.2 PQL definition & scoring logic

A contact becomes a **PQL** when they fire **one or more in-product activation events**:
- created their first guidde
- published a guidde
- invited a teammate (weighted highest — signals collaboration, virality, expansion)

**Sample lead score** (HubSpot lead scoring model — see build note below):

| Signal | Points |
|---|---|
| First guidde created | +20 |
| Teammate invited | +15 |
| Guidde published | +10 |
| Pricing page visit | +10 |
| Marketing email click | +5 |
| No product use in 90 days | −10 |

**Two routes into sales qualification (SQL):**
1. **Direct intent** — a demo is booked or the BDR qualifies the contact, OR
2. **Accumulated product intent** — lead score crosses **50** (e.g., first guidde +20, teammate +15, published +10, pricing visit +10 = 55).

This means a *single* activation event makes someone a PQL (worth watching), but it takes either explicit intent or a meaningful *accumulation* of behavior to become an SQL (worth a rep's time).

> **Build note (tier):** Native HubSpot **contact** scoring requires **Marketing Hub Professional**, which was not included in the Sales Hub Pro trial used for this build. So in the live HubSpot build this point model is **not** implemented as a live `HubSpot Score`. Instead, Workflow 1 reproduces the same qualification with **direct product-activation branches**: a single activation event → **PQL**, and *two or more* activation events (or BDR-qualified / demo-booked) → **SQL** — the buildable equivalent of "score ≥ 50." With a full Marketing + Sales stack, the table above is configured directly in *Settings → Lead Scoring* and Workflow 1 branches on `HubSpot Score ≥ 50`.

### 1.3 Deal pipeline (the opportunity)

A **new-business pipeline** that starts at SQL, not at "lead":

1. **SQL / New Opportunity**
2. **Discovery & Demo**
3. **Evaluation / Trial (POC)**
4. **Proposal & Negotiation**
5. **Verbal Commit / Contract Sent**
6. **Closed Won** *(separate stage)*
7. **Closed Lost** *(separate stage)*

> **Change from v1:** Closed Won and Closed Lost are now shown as **two separate stages**, which is how HubSpot actually models terminal stages (each needs its own probability and won/lost flag). The pipeline still comfortably exceeds the assignment's "≥5 stages."

The pipeline begins when product or high-intent signals justify sales engagement — not when a rep decides to open a deal. Full stage table in **Part 2-A**.

### 1.4 Workflow 1 — Lead Lifecycle Workflow

**Object:** Contact-based workflow. **Tier:** Professional (Workflows).

**Enrollment triggers (OR):**
- Product signup / account created (property: `Product Signup Date` is known), OR
- High-intent form submitted (demo request, pricing inquiry, high-intent content), OR
- Lead score reaches the PQL/activation threshold.

**Logic (top to bottom):**

1. **Set to Lead** on signup or form submit; stamp `Original Source` and `First Touch Date`.
2. **Promote to MQL** when *marketing* qualification is met — **explicit, build-ready definition:** `(≥2 marketing email clicks in 30 days) OR (pricing-page view) OR (mid-intent form fill: webinar, guide, comparison)`. *(v2 fix: v1 left "MQL criteria" undefined.)*
3. **Promote to PQL** when any activation event fires: `First guidde created = true` OR `Guidde published = true` OR `Teammate invited = true`.
4. **On PQL:** add score, stamp `PQL Date`, set `Contact Owner` via rotate-owner (round-robin within the inbound BDR pod; segment override for named/enterprise domains), and notify the owner.
5. **Promote to SQL** when ANY: demo booked `OR` BDR sets `Qualified = true` `OR` **2+ product-activation events** (accumulated intent — the build-equivalent of lead score ≥ 50; see §1.2 build note) `OR` pricing-page activity confirms commercial intent.
6. **Promote to Opportunity** when an associated deal is created.
7. **Promote to Customer** when an associated deal is `Closed Won`.

**Guardrails:**
- **Forward-only** progression — a branch checks current stage and **skips backward moves** unless an admin resets the record.
- Every move stamps a **`Lifecycle Change Reason`** + **`Lifecycle Change Date`**.
- **Re-enrollment / double-fire control:** re-enrollment allowed only on the score trigger; a "skip if already ≥ this stage" branch prevents the two workflows from fighting over the same contact (see §1.6).

**Free-tier fallback:** without Workflows, lifecycle moves become a documented manual SOP + a daily active-list review; PQL becomes a saved list rather than a stage.

### 1.5 Workflow 2 — Deal Automation Workflow

**Object:** Contact-based workflow that creates/updates an associated deal. **Tier:** Professional.

**Enrollment triggers (OR):** `Lifecycle = SQL` OR `BDR Qualified = true` OR `Meeting booked, type = Demo`.

**Step 1 — Dedupe (build-ready detail).** v1 said "check whether the contact has an open deal" without saying how. Implementation: maintain a rollup property **`Count of Open Deals`** on the contact (via HubSpot data-quality automation / association rollup). The workflow then branches:
- `Count of Open Deals ≥ 1` → **Update branch**
- `Count of Open Deals = 0` → **Create branch**

**Create branch (no open deal):**
- Create a deal in **New Business** at **SQL / New Opportunity**.
- Set **`Deal Source`** = `PLG` if the triggering signal was product-driven; else `Inbound` / `Outbound`.
- Assign deal owner = existing **Contact Owner** (continuity).
- Stamp starting properties: `ICP Fit`, `Use Case`, `Product Interest`, `Estimated Amount`, `Target Close Date`.
  - **Source of auto-stamped values** *(v2 fix):* `Estimated Amount` defaults from a **plan×seats lookup** keyed off `Product Interest`/`Company Size`; `Target Close Date` defaults to `today + standard cycle (e.g., 30 days)`. Both are rep-editable.
- Create a **48-hour task** for the owner: confirm scope, ACV, next step.
- Notify the owner.

**Update branch (open deal exists):**
- `IF Meeting type = Demo` → move deal to **Discovery & Demo**.
- `IF Trial Started = true` (property set by product/CS) → move deal to **Evaluation / Trial (POC)**.
- Re-stamp `Last Activity Date`; refresh key engagement properties.
- *(Each move is an explicit branch condition — v1 left this implicit.)*

**Validation & accuracy controls:**
- Attempt to progress without required fields → create **"Incomplete deal"** task and hold.
- Deal idle beyond stage SLA → **stale-deal alert**.
- `Closed Lost` → require structured **`Closed-Lost Reason`** (picklist) + `Competitor`.
- `Closed Won` → trigger **CS handoff** sequence automatically.

**Free-tier fallback:** deals created manually at qualification using a required-field deal form; dedupe enforced by a saved view of duplicate open deals reviewed daily.

### 1.6 How the design improves the revenue engine (required explanation)

- **Scalability** — sales effort scales around *qualified* volume (PQL/score/BDR), not raw signup volume. The system, not memory, opens deals.
- **Data hygiene** — forward-only lifecycle, dedupe rollup, progressive required fields, picklist loss reasons, and date stamps prevent the usual CRM rot.
- **Forecasting** — consistent stage definitions + no duplicate open deals + structured commercial fields make stage-conversion, weighted pipeline, and close dates trustworthy.
- **Team efficiency** — auto-routing, owner continuity, task creation, and automatic CS handoff remove manual triage and dropped context.

---

## Part 2 — Sales Process Design

### Part 2-A. Pipeline structure & stage definitions

*(v2 fix: Entry and Exit are now separate columns; required fields are progressive by stage.)*

| Stage | Entry criteria | Exit criteria | Required fields (added at this stage) | Owner | Recommended automation |
|---|---|---|---|---|---|
| **SQL / New Opportunity** | Contact hits SQL (demo booked, score ≥50, or BDR qualified) | Discovery scheduled & fit confirmed | Deal Name, Deal Source, Estimated Amount, ICP Fit, Primary Contact, Use Case | **BDR** → routes to AE | Auto-create deal, dedupe rollup, owner assign, 48h task |
| **Discovery & Demo** | Discovery/demo booked | Need, stakeholders, decision timeline documented | Pain/Need, Decision Timeline, Champion Identified | **AE** | Meeting logging; reminder if no movement 5 days |
| **Evaluation / Trial (POC)** | Guided eval/trial/pilot begins | Success criteria met & decision path confirmed | Success Criteria, Trial Start/End, Active Users, Technical Fit | **AE** + **CS support** | Low-usage alert; notify CS for onboarding |
| **Proposal & Negotiation** | Pricing/proposal sent | Verbal agreement reached | Confirmed ACV, Plan/Seats, Decision Maker, Procurement/Legal Status | **AE** | Proposal reminders; deal-stuck alert at 14 days |
| **Verbal Commit / Contract Sent** | Verbal yes; contract out | Signed or stalled | Contract Sent Date, Confirmed Close Date, Signatory | **AE** | Contract + signature follow-up tasks |
| **Closed Won** | Deal won | Terminal | Final ACV, Seats, CS Owner | **AE → CS** | Onboarding handoff fires |
| **Closed Lost** | Deal lost | Terminal | Closed-Lost Reason (picklist), Competitor, Re-engage Date | **AE** | Stamp structured reason; set re-engage date |

**Why it works:** progressive required fields (not everything at stage 1) reduce junk data entered just to advance a record; **objective exit criteria** beat intuition for forecast quality; ownership is explicit (BDR qualifies/routes → AE owns the deal → CS supports trial and owns post-sale).

### Part 2-B. Deal creation process

**Who creates deals & when.** The **BDR makes the qualification call** using a lightweight framework (ICP fit + product behavior + use-case clarity + buying-group signal + reasonable urgency). Once made, **HubSpot creates the deal automatically** via Workflow 2. This (a) avoids missed opportunities from forgotten manual creation, and (b) avoids pipeline flooding because creation still depends on human qualification or clear high-intent behavior. *(Decision D4.)*

**Mandatory properties at creation:** Deal Source · Primary Contact · ICP Fit · Use Case · Estimated Amount/ACV · Buying Group / key stakeholder · Expected Timeline · Product Interest. *(Covers the assignment's named examples: ACV, ICP fit, use case, buying group, timeline.)*

**Data validation rules:**
- No duplicate open deals per contact/account without admin review (enforced via the `Count of Open Deals` rollup).
- `Closed-Lost Reason` is a **picklist**, never free text.
- Required fields **increase by stage**, not all at creation.
- Incomplete records generate a follow-up task and **block progression** until resolved.

**Automations that maintain accuracy:** auto-create on qualification; auto-assign owner from Contact Owner; tasks at creation and key transitions; automatic milestone date stamps; stale-deal alerts.

**How it supports forecasting:** consistent creation + consistent dedupe + consistent advancement → leaders can trust stage-conversion rates, weighted pipeline, and projected close dates far more than in a manually managed CRM.

### Part 2-C. Risks, bottlenecks & opportunities

**Operational risk.** A PLG-hybrid motion is powerful but fragile if qualification logic is loose. Two failure modes: **over-routing** low-value PQLs (wastes BDR/AE time, erodes trust in product signals) and **under-routing** real intent (product events not mapped cleanly to lifecycle, or unclear ownership). Mitigation: explicit activation rules, the score threshold, and **SLA monitoring** on follow-up speed.

**Bottleneck.** The biggest is the **Trial/POC → commercial** transition: prospects can clearly *use* guidde without revealing buying process, champion strength, or timeline. So **Evaluation / Trial (POC)** must be a structured conversion checkpoint, not a waiting room — success criteria, active-user counts, and CS-supported onboarding make the stage diagnostic.

**Data reliability & tooling.** The core data risks are inconsistent stage movement, weak loss-reason capture, and sloppy AE→CS handoffs. The fix is structure, not more free-text: progressive required fields, picklists, task automation. **Concrete tooling** *(v2 fix — v1 named none):* a **data-enrichment tool** (e.g., Clearbit/Apollo) to auto-fill ICP/firmographics, a **dedup/data-quality monitor** (HubSpot's Data Quality Command Center on Pro, or Insycle) for the open-deals rollup, and **SLA/alerting** in workflows. As an extensibility opportunity, **outbound enrichment + ICP scoring** can sit as a light appendix motion feeding the *same* SQL gate — one unified pipeline, two on-ramps.

### Appendix — Outbound on-ramp (light, by design)

Outbound is a **secondary on-ramp**, not a third workflow. Both motions converge on one SQL gate and one set of stage definitions.

```
PLG path:      free signup ─▶ activation ─▶ PQL ─▶ [ SQL gate ] ─▶ deal stages
Outbound path: target list ─▶ enrichment ─▶ ICP score ─▶ sequence ─▶ reply/meeting ─▶ [ SQL gate ] ─▶ deal stages
                                                                          ▲
                                              one SQL gate · one pipeline · one set of stage definitions
```

One pipeline, two acquisition motions, one qualification standard for forecasting.

---

## Part 3 — Dashboard & KPI Reporting

### 3.1 Design principle

The dashboard exists to answer four leadership questions **fast**:
1. Who is performing best?
2. **What activities or motions generate the most revenue?**
3. Where are the bottlenecks?
4. What changes will most increase revenue?

Structure: an executive summary row + three KPI groups matching the brief, **plus an explicit "Revenue by Motion" cut** so question #2 is actually answered. *(v2 fix: v1 claimed to answer #2 but had no motion-level revenue KPI.)*

### 3.2 Dashboard outline (visual mockup)

```
┌──────────────────────────────────────────────────────────────────────────┐
│ EXECUTIVE SUMMARY                                                           │
│  Open Pipeline $ │ Commit/Best-Case │ Closed Won (period) │ Avg Cycle Days  │
├───────────────────────────────┬────────────────────────────────────────────┤
│ PIPELINE & FORECASTING         │ REVENUE BY MOTION  ◀ answers Q2             │
│  • Pipeline by stage (funnel)  │  • Won $ by Deal Source (PLG/Inbound/Outb.) │
│  • Coverage vs target          │  • Win rate by motion                       │
│  • Stage→stage conversion      │  • Avg deal size by motion                  │
│  • Weighted pipeline / qtr     │  • Pipeline created by motion               │
│  • Forecast accuracy           │                                             │
│  • Avg days in stage (bottleneck heatmap)                                    │
├───────────────────────────────┼────────────────────────────────────────────┤
│ SALES PERFORMANCE (rep + team) │ PRODUCTIVITY & EFFICIENCY                    │
│  • Closed Won $ by rep         │  • Time: PQL → first sales action (SLA)      │
│  • Win rate by rep             │  • Demo-booked rate from SQL                 │
│  • SQL→Won conversion by rep   │  • Discovery→Trial conversion                │
│  • Avg deal size by rep        │  • Trial/POC→Proposal conversion             │
│  • Pipeline created by rep     │  • Meetings held per rep                     │
│  • Closed-lost reasons (rep/team)  • Follow-up SLA attainment                 │
│                                │  • Won-deal handoff completion rate          │
└───────────────────────────────┴────────────────────────────────────────────┘
```

### 3.3 KPI list **with definitions** (every listed KPI defined)

**Executive summary**
- **Open Pipeline $** — total amount of all open deals.
- **Commit / Best-Case Forecast** — sum of deals flagged commit (high confidence) and best-case (possible) for the period.
- **Closed Won (period)** — revenue won in the selected period.
- **Average Sales Cycle Length** — mean days from deal create to Closed Won.

**Pipeline & Forecasting**
- **Pipeline by stage** — amount and count of open deals in each stage.
- **Pipeline coverage vs target** — open pipeline ÷ next-period quota target.
- **Stage-to-stage conversion rate** — % of deals advancing from each stage to the next.
- **Weighted pipeline by quarter** — open pipeline × stage probability, rolled to expected close quarter.
- **Forecast accuracy** — forecasted Closed Won vs actual Closed Won.
- **Average days in stage** — mean time a deal sits in each stage (the bottleneck signal).

**Revenue by Motion** *(new in v2)*
- **Won $ by Deal Source** — Closed Won revenue split by PLG / Inbound / Outbound.
- **Win rate by motion** — Closed Won ÷ resolved deals, per Deal Source.
- **Average deal size by motion** — mean final ACV per Deal Source.
- **Pipeline created by motion** — new pipeline $ generated per Deal Source.

**Sales Performance (per rep + team)**
- **Closed Won $ by rep** — revenue closed in period by AE.
- **Win rate by rep** — Closed Won ÷ total resolved deals, per rep.
- **SQL→Closed Won conversion by rep** — % of a rep's SQLs that become won deals.
- **Average deal size by rep** — mean final ACV of a rep's won deals.
- **Pipeline created by rep** — new pipeline $ a rep generated in period.
- **Closed-lost reasons (rep/team)** — distribution of structured loss reasons.

**Productivity & Efficiency**
- **Time from PQL to first sales action** — elapsed time from `PQL Date` to first logged rep activity.
- **Demo-booked rate from SQL** — % of SQLs that reach Discovery & Demo.
- **Discovery→Trial conversion** — % of Discovery deals reaching Evaluation/Trial.
- **Trial/POC→Proposal conversion** — % of Trial deals reaching Proposal.
- **Meetings held per rep** — count of completed meetings per rep in period.
- **Follow-up SLA attainment** — % of new PQLs/SQLs contacted within the SLA window.
- **Won-deal handoff completion rate** — % of won deals with all CS handoff fields + onboarding tasks complete.

### 3.4 How the dashboard answers each leadership question

| Question | Answered by |
|---|---|
| Who is performing best? | Sales Performance group (Won $, win rate, SQL→Won by rep) |
| What motions generate the most revenue? | **Revenue by Motion group** |
| Where are the bottlenecks? | Avg days in stage + stage-to-stage conversion + funnel |
| What will increase revenue? | Conversion/SLA gaps + loss-reason patterns + coverage vs target |

### 3.5 Creative presentation format

Record the solution as a **guidde walkthrough** — it uses guidde's own product as the medium and demonstrates communication in exactly the format the company sells. Order: GTM framing → lifecycle & PQL → pipeline & ownership → Workflow 1 → Workflow 2 → dashboard. ~4–6 minutes, backed by HubSpot screenshots. (Production steps in `hubspot-build-guide.md`.)

---

## Closing

This is a deliberately practical operating model: automate what is objective, standardize what is repetitive, and preserve human judgment where context matters. For a PLG-hybrid SaaS like guidde, that combination improves scalability, data hygiene, forecasting accuracy, and team efficiency at once — and it is buildable in HubSpot today on a Professional trial, with a documented free-tier fallback.
