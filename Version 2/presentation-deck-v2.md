# Guidde Sales Ops Case Study — Presentation Deck (v2, canonical)

> **This is the single source deck.** v1 had two overlapping files (`case-study-deck-source.md` + `presentation-outline.md`); they are merged here. Copy-paste straight into Google Slides / Keynote / PowerPoint. Speaker notes in *italics*.

---

## Slide 1 — Title
**Guidde Sales Operations Manager Case Study**
Justin [LAST NAME — fill before sending]
*Designing a scalable Sales Ops system for a PLG-hybrid revenue motion*

---

## Slide 2 — Executive summary
**Objective:** turn product intent into clean pipeline, reliable execution, and usable forecasting.
**What I designed:**
- 7-stage HubSpot pipeline (Closed Won & Lost as separate stages)
- PQL-centered lifecycle framework
- 2 workflows: Lead Lifecycle + Deal Automation
- Explicit BDR / AE / CS ownership
- KPI dashboard incl. **revenue-by-motion**
**Core principle:** automate what is objective; preserve human judgment where context matters.

---

## Slide 3 — Why this model fits guidde
**Assumptions:** PLG-hybrid GTM · product usage is a first-class qualification signal · a person can move through lifecycle without a deal yet · ownership spans BDR/AE/CS.
**Key framing:**
- Lifecycle stage → *where is this person?*
- Deal stage → *where is this revenue opportunity?*
*Tier note: Workflows/scoring/custom stages are Pro features — built on the 14-day Pro trial.*

---

## Slide 4 — Lifecycle model
**Subscriber → Lead → MQL → PQL → SQL → Opportunity → Customer**
**Why PQL is central:** guidde's strongest intent is product behavior, not form fills.
**Activation signals:** first guidde created · guidde published · teammate invited (highest weight).
**Two routes to SQL:** direct intent (demo/BDR) **or** accumulated score ≥ 50.

---

## Slide 5 — Pipeline design
1. SQL / New Opportunity
2. Discovery & Demo
3. Evaluation / Trial (POC)
4. Proposal & Negotiation
5. Verbal Commit / Contract Sent
6. Closed Won
7. Closed Lost
**Why:** clean ownership checkpoints · stronger conversion visibility · forecasting discipline · built for PLG-led engagement.

---

## Slide 6 — Workflow 1: Lead Lifecycle
**Triggers (OR):** product signup · high-intent form · score threshold.
**Logic:** Lead → MQL (≥2 email clicks *or* pricing view *or* mid-intent form) → PQL (activation event) → SQL (demo *or* BDR qualified *or* score ≥50) → Opportunity (deal created) → Customer (Closed Won).
**Guardrails:** forward-only · reason/date stamping · owner assign + notify · re-enrollment control.

---

## Slide 7 — Workflow 2: Deal Automation
**Triggers (OR):** Lifecycle=SQL · BDR Qualified · Demo booked.
**Dedupe first:** branch on `Count of Open Deals` rollup.
**Create branch (=0):** new deal at SQL stage · set Deal Source · owner continuity · stamp ICP/Use Case/Est. Amount/Close Date · 48h task.
**Update branch (≥1):** Demo→Discovery · Trial Started→Evaluation · refresh activity.
**Controls:** incomplete-deal hold · stale-deal alert · picklist loss reason · auto CS handoff on Won.

---

## Slide 8 — Pipeline governance & ownership
**BDR** — reviews PQL/high-intent, applies qualification judgment, routes.
**AE** — owns discovery → evaluation → proposal → close.
**CS** — supports trial/onboarding, owns post-sale handoff on Won, feeds adoption/expansion back to CRM.
**Ops layer** — progressive required fields · objective exit criteria · structured handoffs.

---

## Slide 9 — Deal creation process
**Philosophy:** judgment by human, creation by system.
**Required at creation:** Deal Source · Primary Contact · ICP Fit · Use Case · Est. Amount/ACV · Buying Group · Expected Timeline · Product Interest.
**Accuracy controls:** no duplicate open deals · incomplete-deal tasks · stale-deal alerts · structured Closed-Lost Reason.

---

## Slide 10 — Risks, bottlenecks, opportunities
**Risks:** low-quality PQLs overwhelming sales · missed high-intent users · dirty stage data / weak CS handoff.
**Bottleneck:** Trial/POC becomes a waiting room without success criteria + usage signals.
**Tooling:** enrichment (Clearbit/Apollo) · dedup/data-quality monitor · SLA alerting.
**Opportunity:** outbound enrichment + ICP scoring as a light appendix feeding the same SQL gate.

---

## Slide 11 — Outbound on-ramp (light appendix)
```
PLG:      signup ▶ activation ▶ PQL ─┐
                                     ├▶ [ SQL gate ] ▶ deal stages
Outbound: list ▶ enrich ▶ score ▶ sequence ▶ reply ─┘
```
One pipeline · two acquisition motions · one SQL gate · one set of stage definitions.

---

## Slide 12 — Dashboard & KPIs
**Exec row:** open pipeline · commit/best-case · closed won · avg cycle.
**Pipeline & Forecasting:** pipeline by stage · coverage vs target · stage conversion · weighted pipeline · forecast accuracy · avg days in stage.
**Revenue by Motion:** won $ / win rate / avg deal size / pipeline created — by Deal Source. *(answers "what motions drive revenue?")*
**Sales Performance (rep+team):** closed won by rep · win rate · SQL→Won · avg deal size · pipeline created · loss reasons.
**Productivity & Efficiency:** PQL→first action · demo-booked rate · discovery→trial · trial→proposal · meetings/rep · follow-up SLA · handoff completion.

---

## Slide 13 — Creative presentation format
Record the solution as a **guidde walkthrough** (~4–6 min): uses guidde's own product · demonstrates communication clarity · makes the HubSpot build easy to review.
**Order:** GTM framing → lifecycle/PQL → pipeline & ownership → Workflow 1 → Workflow 2 → dashboard.

---

## Slide 14 — Closing
A practical, startup-ready Sales Ops design for a PLG-hybrid motion: product-signal-led qualification · clear BDR/AE/CS ownership · hybrid deal creation · cleaner forecasting and stronger execution.
*Thank you — I'd be glad to discuss how I'd adapt this to guidde's live data, team, and growth priorities.*
