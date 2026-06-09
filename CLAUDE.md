# Guidde Sales Ops Case Study — Working Context (CLAUDE.md)

> Continuation file so we can pick up exactly where we left off. Last updated: 2026-06-09 (overnight).

---

## 0. What this project is
Take-home case study for a **Sales Operations Manager** role at **Guidde** (AI video-documentation / PLG-hybrid SaaS).
Deliverables: (1) HubSpot build — pipeline + 2 workflows, (2) written case study, (3) Part 2 process design, (4) Part 3 dashboard + KPIs, (5) a **guidde walkthrough video** as the "creative presentation."

Submission email (from assignment): `yuval.haramaty@guidde.co`
Author name placeholder still to fill: **Justin [LAST NAME]** — ⚠️ confirm real name before sending. (Account owner in HubSpot is "Woo Chun" — reconcile which name goes on the submission.)

---

## 1. Current status (✅ done / �doing / ⏳ todo)

**Docs (in `/Version 2/`)** — the source of truth
- ✅ `case-study-v2.md` — full written deliverable (Parts 1–3). Already updated with tier/scoring notes.
- ✅ `presentation-deck-v2.md` — slide deck
- ✅ `hubspot-build-guide.md` — build checklist (updated for Sales-Hub-only reality)
- ✅ `00-README-changelog.md` — review→fix changelog
- ✅ `revenue-dashboard-mockup.html` — interactive dashboard (⚠️ currently PURPLE theme — needs re-theme to Guidde RED)
- �NEW `case-study-report.html` — consolidated, restructured, RED-themed report (built overnight; see §5)

**HubSpot build (Sales Hub Pro 14-day trial)**
- ✅ Pipeline "Enrollment Pipeline" — 7 stages
- ✅ All custom properties (deal + contact)
- ✅ PQL custom lifecycle stage
- ✅ 23 sample deals (all stages, mixed source/ICP)
- ✅ 4 demo contacts (lifecycle ladder)
- ✅ **Workflow 1 — Lead Lifecycle** built (enrollment → guard → PQL/SQL branch + reason stamps)
- ⏳ **Workflow 1 test** — not yet run (turn ON + "enroll existing"; expect Dana→SQL, Raj→PQL)
- ⏳ **Workflow 2 — Deal Automation** — NOT built yet (tomorrow). Spec = `case-study-v2.md` §1.5.
- ⏳ **guidde recordings** — WF1 video recorded + step descriptions polished; WF2 video tomorrow.

**Tomorrow's plan (user's words):** wake up → build Workflow 2 → record it.

---

## 2. KEY DECISIONS & FRAMING (don't lose these)

### Tier reality (the spine of the whole submission)
- Built on **Sales Hub Professional trial** (self-serve 14-day). Marketing Hub NOT available (requires sales call).
- **What needs Marketing Hub (so we did NOT build, documented as design instead):**
  - Native **lead scoring** (`hubspotscore` is read-only, set only by Marketing Hub Lead Scoring app)
  - **Marketing email click** tracking
  - **Page-view / pricing-page** behavior tracking
- **What IS buildable on Sales Hub (chose scope, not blocked):** Forms, product-signup property, sales activities, BDR-qualified property, Workflows, custom lifecycle stages, rotate-owner.
- **Workaround used:** WF1 drives qualification off **product-activation events directly** (First Guidde Created / Guidde Published / Teammate Invited) + BDR Qualified — the buildable equivalent of "lead score ≥ 50."

### Defensible narrative (use in writeup + interview)
> "Early-funnel triggers (form fills, marketing engagement, signup) span Sales + Marketing Hub, so some are only partially buildable on a Sales Hub trial. I focused the live build on the **product-qualification mechanism (PQL→SQL)** — the core of a PLG-hybrid model and fully buildable here. The complete lifecycle is in the written design."

### WF1 scope (what we built vs §1.4 full design)
- ✅ Built: enrollment (activation+BDR), forward-only guard, PQL/SQL split, reason stamps, re-enrollment.
- 🔁 Handled by native HubSpot automation: Lead default (contact-created→Lead), Opportunity (deal-created), Customer (deal-won). Confirmed in Settings → Objects → Contacts → Lifecycle Stage → Automate (3 toggles ON, "Sync lifecycle stages" OFF — keep OFF).
- ⏸️ Deferred (tier): MQL via email/page signals.
- ⭕ Skipped (optional, buildable): PQL owner-rotation + internal notification, PQL Date stamp.
- Lifecycle can't move backward in HubSpot → to reset demo contacts you must **clear stage to "" then set** lower value (2-step).

### Lifecycle_change_reason — consolidated
- The 3 "Product Activation — X" options were collapsed to a single **"Product Activation"** (which event fired still lives in the bool properties).

---

## 3. HubSpot reference IDs (for the connector)
- Account: **246436625** · Owner "Woo Chun" ownerId **93622568**
- Pipeline value: `default` (label "Enrollment Pipeline")
- Stages: SQL `3807837923` · Discovery `3807837924` · Evaluation `3807837925` · Proposal `3807837926` · Verbal `3807837927` · `closedwon` · `closedlost`
- PQL lifecycle stage value: `3807837937`
- Demo contacts: Dana Whitfield `499110480626` (Lead; First+Teammate+Published+BDR) · Raj Patel `499068134127` (Lead; First only) · Emily Carter `499083968216` (MQL) · Tom Nguyen `499090075350` (Lead)
- Custom deal props: `deal_source` `icp_fit` `use_case_guidde` `product_interest` `competitor` `closedlost_reason` `champion_identified` `technical_fit` `active_users`
- Custom contact props: `first_guidde_created` `guidde_published` `teammate_invited` `trial_started` `bdr_qualified` `pql_date` `lifecycle_change_reason` `count_of_open_deals`

### Connector capabilities (HubSpot MCP)
- ✅ CAN: create/update CRM **records** (deals, contacts), read properties/objects, search.
- ❌ CANNOT: create property **definitions**, build **workflows**, archive/delete records. Those are manual in the UI.
- Batch limit: **10 objects per create** call.

---

## 4. Workflow 2 — what to build tomorrow (spec = §1.5)
Contact-based workflow that creates/updates an associated deal.
- **Enrollment (OR):** Lifecycle=SQL OR `bdr_qualified=true` OR Demo meeting booked.
- **Step 1 Dedupe:** branch on `count_of_open_deals` rollup → `=0` Create, `≥1` Update.
  - ⚠️ `count_of_open_deals` rollup must be set up first (Data Quality automation / helper). May be fiddly on Sales Hub — confirm at build time; if not available, fall back to `num_associated_deals` or document the limitation.
- **Create branch:** create deal at SQL stage; set `deal_source`, owner=Contact Owner; stamp ICP/use case/product interest; `amount` from plan×seats lookup; `closedate`=today+cycle; 48h task; notify owner.
- **Update branch:** Demo→Discovery; `trial_started=true`→Evaluation; refresh last activity.
- **Validation:** incomplete-deal task/hold; stale-deal alert; require `closedlost_reason` on Closed Lost; CS handoff on Closed Won.
- **Test:** Dana (no open deal) → expect Create; a contact with an open deal → expect Update.
- **Tier/scope notes to surface in the WF2 video & doc:** which actions are native vs built; note `amount` lookup is a static demo default; dedupe mechanism + any fallback.

---

## 5. Overnight deliverables (built while user slept)
1. `Version 2/case-study-report.html` — consolidated RED-themed report = restructured case study + embedded dashboard + tier/scope reconciliation section + **video-reference callouts for WF1 & WF2**.
2. Re-themed `revenue-dashboard-mockup.html` purple → **Guidde RED**.
3. This `CLAUDE.md`.

### Brand
- **Guidde RED** primary ≈ `#E11B22` (from the official red "guidde." wordmark). Logo = lowercase red wordmark with trailing period. Pair with near-black headings + warm off-white bg. (Earlier purple assumption was WRONG — red is correct.)

---

## 6. Immediate next actions (morning)
1. Test WF1 (turn on → enroll existing → verify Dana→SQL, Raj→PQL → screenshot).
2. Build Workflow 2 (§1.5 + §4 above) — agree full spec first, flag build-vs-skip up front.
3. Record WF2 guidde; polish step titles/descriptions; add include/exclude + video-reference notes.
4. Review the overnight `case-study-report.html`; fill last name; finalize submission package.
