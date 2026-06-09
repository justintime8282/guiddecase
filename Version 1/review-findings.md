# Review Findings — Guidde Sales Operations Manager Take-Home

**Reviewer:** Critical review pass (gaps-first, not a cheerleader)
**Date:** 2026-06-05
**Sources of truth:** `Sales Operations Manager - Home assignment.pdf` (the REQUIREMENTS) + the locked decisions provided in the review brief (the BASELINE).
**Drafts under review:** `case-study-draft.md`, `case-study-deck-source.md`, `presentation-outline.md`.

---

## Assumptions & Caveats (read first)

1. **The baseline brief `guidde-salesops-handoff.md` is missing from this folder.** I could not find it (only the assignment PDF and three .md drafts exist). I therefore validated against the locked decisions you listed in the review request, not the full handoff document. If the handoff contains additional standards (specific KPI targets, naming conventions, tone, page limits), those have **not** been checked. **Recommend locating that file before final submission.**
2. The three .md files are *documents/specs only*. The assignment's Part 1 and the "creative presentation" are **hands-on** (build in HubSpot + record a guidde). Those cannot be satisfied by editing docs — tracked in a separate section at the end.
3. I did not modify any draft file. This is review output only.
4. HubSpot tier-gating claims below reflect the locked decision ("HubSpot Workflows tool requires Pro tier") plus standard HubSpot packaging; verify against the current free-tier feature set when you do the build.

---

# PASS 1 — Inventory & Coverage

## 1.1 Explicit deliverables required by the assignment

**Part 1 — HubSpot Workflow & Automation**
- 1a. Create a **free** HubSpot CRM account *(hands-on)*
- 1b. Build a **customized sales pipeline with ≥5 deal stages** *(hands-on)*
- 1c. Build **Workflow 1 — Lead Lifecycle** (move leads through lifecycle on triggers) *(hands-on)*
- 1d. Build **Workflow 2 — Deal Automation** (create/update deals on criteria) *(hands-on)*
- 1e. Submit a **creative presentation** of the solution
- 1f. Submit a **short written explanation**: (i) logic & **assumptions**; (ii) how the workflows improve **scalability, data hygiene, forecasting, team efficiency**

**Part 2 — Sales Process Design**
- 2A. Pipeline table: **Stage names, Entry & exit criteria, Required fields per stage, Owner (BDR/AE/CS), Automations recommended** → submitted as `Stage → Definition → Requirements → Owner`
- 2B. Deal creation: **who creates & when; mandatory properties (ACV, ICP fit, use case, buying group, timeline…); data validation rules; automations to maintain accuracy; how it supports forecasting**
- 2C. Risks/bottlenecks/opportunities (1–3 paragraphs): **operational risks; data reliability issues; potential bottlenecks; automation/tooling recommendations**

**Part 3 — Dashboard & KPI**
- 3a. Dashboard outline (table / mockup / bullets) that lets leadership answer the **four leadership questions**: who performs best; **what activities/motions generate most revenue**; where are bottlenecks; what changes will increase revenue
- 3b. KPIs grouped into **Pipeline & Forecasting / Sales Performance (per-rep + team) / Productivity & Efficiency**
- 3c. **A list of KPIs *with definitions***
- 3d. A **creative presentation** of the solution

## 1.2 Locked decisions (baseline) to enforce

| # | Locked decision | 
|---|---|
| D1 | PLG-hybrid GTM motion |
| D2 | BDR + AE + CS ownership model |
| D3 | PQL defined by in-product activation |
| D4 | Hybrid deal creation = BDR qualifies, then system auto-creates |
| D5 | Outbound = **light appendix only** (one diagram + a few sentences), not a third workflow |
| D6 | **HubSpot Workflows tool requires Pro tier** |

## 1.3 Coverage table

| Requirement | Covered in | Status |
|---|---|---|
| 1a Free HubSpot account | — (hands-on) | **Missing (hands-on)** |
| 1b ≥5-stage pipeline | `case-study-draft.md` §Part 1.A, §Part 2-A; both decks Slide 5 | **Complete (as spec)** — 6 stages |
| 1c Lead Lifecycle workflow | draft §Part 1.E; deck Slide 6; outline Slide 6 | **Complete as spec / Partial build-readiness** (see 2.1) |
| 1d Deal Automation workflow | draft §Part 1.F; deck Slide 7; outline Slide 7 | **Complete as spec / Partial build-readiness** (see 2.1) |
| 1e Creative presentation | draft §3.E; deck Slide 12; outline Slide 12 | **Partial** — recommended (guidde recording) but not produced (hands-on) |
| 1f(i) Logic & **assumptions** | draft §Executive Framing; deck Slide 3 | **Partial** — logic strong; "assumptions" never labeled as such in Part 1 |
| 1f(ii) Scalability/hygiene/forecasting/efficiency | draft §Part 1.G | **Complete** |
| 2A Pipeline table | draft §Part 2-A | **Complete** |
| 2B Deal creation | draft §Part 2-B; deck Slide 9 | **Complete** |
| 2C Risks/bottlenecks/opps | draft §Part 2-C | **Complete** (tooling rec is light) |
| 3a Dashboard answers 4 questions | draft §Part 3.A/B | **Partial / Contradicts itself** — Q2 "motions that generate revenue" not actually answered (see 2.3) |
| 3b KPI grouping | draft §Part 3.B | **Complete** — groups match brief exactly |
| 3c KPIs **with definitions** | draft §Part 3.C | **Partial** — several listed KPIs are undefined |
| 3d Creative presentation | draft §3.E; decks Slide 12 | **Partial** — bullets only, no visual mockup; recording is hands-on |
| D1 PLG-hybrid | all files | **Complete** |
| D2 BDR+AE+CS | draft §Part 2-A, §2-B; deck Slide 8 | **Complete** |
| D3 PQL by in-product activation | draft §Part 1.C/D | **Complete** |
| D4 Hybrid deal creation | draft §Part 1.F, §Part 2-B | **Complete** |
| D5 Outbound = light appendix | draft §Appendix + §2-C | **Partial** — within size, but no diagram and mentioned in 3 places |
| D6 Workflows require Pro tier | — | **Missing / Contradicts assignment** — never acknowledged anywhere (see P0-1) |

---

# PASS 2 — Quality & Correctness (per deliverable)

## 2.1 Part 1 — Workflows & Automation

**Strengths.** The lifecycle-vs-deal-stage split is articulated cleanly (draft §Part 1.B: "lifecycle stage answers 'where is this person…' while deal stage answers 'where is this specific revenue opportunity?'"). Section G hits all four required improvement dimensions explicitly. Decisions D1–D4 are honored consistently.

**Critical problem — the free-tier contradiction (D6).** The assignment says *"Create a **free** HubSpot CRM account"* and then *"Build … 2 automated workflows."* Per your own locked decision D6, the **Workflows tool is Professional-tier**, not free. **No draft acknowledges this anywhere.** The same gate also affects other things the design depends on:
- **Custom lead scoring** (the `+20/+15/+10…` model in §Part 1.D) — scoring is a paid feature.
- **Custom lifecycle stage "PQL"** inserted between MQL and SQL (§Part 1.C) — custom lifecycle stages are not a free-tier capability; "PQL" is not a default HubSpot stage.
- **Round-robin / rotate-owner action** ("assign the Contact Owner through round-robin" §Part 1.E step 4) — rotation actions live in Workflows (paid).

This is the single biggest evaluator risk: a Sales-Ops reviewer who knows HubSpot will immediately see that the entire Part 1 build cannot exist in a free account, and the docs never address the workaround. See P0-1 for the fix.

**Build-readiness gaps (the two specs are *mostly* build-ready, with soft predicates):**
- **MQL criterion is undefined.** §Part 1.E step 2: *"If qualification criteria are met but intent is still light, promote … to MQL."* Deck Slide 6 restates it circularly: *"MQL when marketing qualification is met."* What event/property triggers MQL? Not specified — not buildable as written.
- **Dedupe step has no implementation.** §Part 1.F Step 1: *"the workflow checks whether the contact already has an open deal."* Native HubSpot workflows don't trivially branch on associated-open-deal count; this needs a specific property/association-based branch. As written it reads simple but is the trickiest part to actually build — and an evaluator will probe it.
- **Update-branch routing is loose.** §Part 1.F "Update branch": *"If a demo is booked, move to Discovery & Demo; if a trial/POC begins, move to Evaluation…"* — but how does *this* workflow detect those within the same enrollment? Needs explicit branch conditions on meeting type / property change.
- **Auto-stamped fields have no source.** §Part 1.F create branch stamps "Estimated Amount" and "Target Close Date" — from what input? Unspecified.
- **Routing logic vague.** "round-robin or segment logic" — which segments? Not defined.

**Potential circular triggering (worth a sanity check at build time).** Lifecycle workflow promotes to SQL on "demo booked / BDR qualifies / score" (§1.E step 5); Deal Automation enrolls on "Lifecycle becomes SQL / BDR Qualified / Demo booked" (§1.F triggers). Overlapping triggers across two workflows can double-fire. Not necessarily wrong, but needs explicit suppression/re-enrollment handling — currently absent.

**Pipeline modeling note.** "Closed Won / Closed Lost" is presented as one stage (§Part 1.A item 6, §Part 2-A last row). In HubSpot these must be **two separate deal stages**. Counting is fine (≥5 satisfied either way), but the spec should show them as two stages so it maps to a real build.

**Assumptions not labeled (1f-i).** The assignment explicitly asks for "logic **and assumptions**." The draft's Part 1 has principles and framing but no labeled assumptions list. The deck Slide 3 has "Operating assumptions" — but the *written explanation* (the draft) should carry an explicit "Assumptions" block.

## 2.2 Part 2 — Sales Process Design

**2A Pipeline table — solid.** All five required attributes present (entry/exit folded into the Definition column; required fields; owner; automation). Progressive-required-fields rationale (§"Why this pipeline design works") is a genuine Sales-Ops signal. D2 honored: BDR qualifies/routes → AE owns → CS supports trial + owns post-sale.
- *Minor:* Entry & exit criteria are **buried inside the Definition cell**. The assignment lists them as distinct items; splitting into explicit Entry / Exit columns would read as more rigorous.

**2B Deal creation — complete.** Covers who/when (BDR judgment → system creates, = D4), mandatory properties (includes all the assignment's examples: ACV, ICP fit, use case, buying group, timeline), validation rules (picklist loss reason, no dup open deals, progressive fields), automations, and forecasting linkage. No material gaps.

**2C Risks/bottlenecks/opps — complete but thin on tooling.** Three paragraphs, within the 1–3 limit. Covers over-/under-routing risk, the Trial/POC bottleneck, and data-reliability (loss-reason capture, handoffs). The assignment's fourth bullet — **"automation or tooling recommendations"** — is the weakest: it's gestured at ("structured fields, picklists, task automation") but no concrete *tooling* (e.g., enrichment vendor, dedup tool, data-quality monitor) is named. Could be a half-sentence stronger.

**D5 (outbound = light appendix).** Within scope on size, but: (a) the locked decision said "one **diagram** + a few sentences" — the appendix is a **bullet model, not a diagram**; (b) outbound now appears in **three** places (§2-C closing sentence, §Appendix, deck Slide 10 / outline Slide 10). It hasn't ballooned into a third workflow (good), but the triple-mention is mild over-exposure for a "light appendix."

## 2.3 Part 3 — Dashboard & KPI

**Grouping is exactly on-brief (3b).** Pipeline & Forecasting / Sales Performance (per-rep + team) / Productivity & Efficiency — matches the assignment's three categories verbatim. Good.

**Critical gap — the dashboard does not answer one of its own four questions (3a).** The draft claims (§Part 3.A, lines ~230–233) to let leadership answer *"What activities or motions generate the most revenue?"* — but **no KPI breaks revenue down by motion / Deal Source.** Given the whole submission rests on a PLG-hybrid model with a `Deal Source` property (PLG / Inbound / Outbound), the obvious, expected KPI — **Revenue & Win-rate by Deal Source/motion** — is missing from the outline. This is both a **direct miss on an explicit Part 3 requirement** and an **internal contradiction** (claims to answer a question the dashboard can't answer). Strong finding; see P0-2.

**KPI definitions incomplete (3c).** The assignment asks for "a list of KPIs **with definitions**." The outline (§Part 3.B) lists ~20 KPIs; §Part 3.C defines only ~13. Listed-but-undefined include: *Stage-to-stage conversion rates; Pipeline created by rep; Closed-lost reasons by rep/team; Meetings held per rep; Follow-up SLA attainment; Discovery-to-trial* is defined but *Demo booked rate* etc. — net: several KPIs have no definition. Either define each or trim the list so every listed KPI is defined.

**Presentation is bullets-only (3d).** Acceptable per the rubric ("bullet-based structure" allowed), but the assignment twice rewards a "creative way to present," and there is **no table or visual mockup** of the dashboard — a missed differentiation opportunity for a Sales-Ops role where dashboard *design* is the deliverable.

**Minor positives.** "Top performers" (per-rep KPIs) and "bottlenecks" (avg days in stage, stage conversion) are well covered. Forecast accuracy, weighted pipeline, coverage vs target are the right Pipeline KPIs.

## 2.4 Cross-file consistency

- 6-stage pipeline, lifecycle string, PQL concept, ownership model, and the two workflows are **consistent** across all three files. Good.
- **Two overlapping presentation files.** `case-study-deck-source.md` (full slide copy) and `presentation-outline.md` (lighter outline) cover the same 13 slides. Redundant; risks confusion about which is the deliverable. Pick one canonical deck.
- **KPI drift between files.** The decks (Slide 11 in both) carry a *subset* of the draft's KPIs and reorder them. Harmless, but tighten so the deck doesn't silently drop KPIs the written doc defines.
- **`Justin [Last Name]` placeholder** unfilled in `case-study-deck-source.md` Slide 1 and `presentation-outline.md` Slide 1. Would go out the door unfinished if not caught.

---

# PASS 3 — Prioritized Fix List

### P0 — Must fix before submitting

**P0-1. Acknowledge and resolve the HubSpot free-tier / Workflows-Pro contradiction (D6).**
- *What's wrong:* The whole Part 1 build (2 workflows + custom lead scoring + custom "PQL" lifecycle stage + round-robin) is **not available on a free HubSpot account**, yet the assignment says "free account" and no draft mentions this.
- *Why it matters:* A Sales-Ops evaluator who knows HubSpot will spot this instantly; silence reads as not knowing the tool's packaging — the exact competency being tested.
- *Fix:* Add an explicit note (in the written explanation and on a slide): "Workflows, lead scoring, and custom lifecycle stages require Professional tier. I used HubSpot's **14-day Professional free trial** to build the automations; on a permanently-free seat these would be implemented as [manual stage updates / scheduled imports / the paid feature]." Decide your real build path (Pro trial is the clean answer) and state it.

**P0-2. Add a "revenue by motion / Deal Source" KPI to the dashboard.**
- *What's wrong:* §Part 3.A claims the dashboard answers "what activities or motions generate the most revenue?" but no KPI segments revenue by PLG vs Inbound vs Outbound.
- *Why it matters:* It's an explicit Part 3 leadership question AND the dashboard contradicts its own stated purpose — easy, damaging catch.
- *Fix:* Add to Pipeline & Forecasting (or a new "Motion" cut): **Revenue / Win-rate / Avg deal size by Deal Source**, and **Pipeline created by motion**. This also ties the dashboard back to the PLG-hybrid thesis.

*(Hands-on P0 items — the actual build and recording — are listed separately below so they aren't lost.)*

### P1 — Should fix

**P1-1. Fill the `Justin [Last Name]` placeholder** in both presentation files (Slide 1). Trivial, but it's a submission-readiness red flag if missed.

**P1-2. Define every listed KPI (3c).** Add definitions for Stage-to-stage conversion, Pipeline created by rep, Closed-lost reasons, Meetings held per rep, Follow-up SLA attainment (and any others listed without a definition), or trim the list. *Why:* the assignment literally asks for "KPIs with definitions."

**P1-3. Specify the MQL trigger** in Workflow 1. Replace "qualification criteria are met / marketing qualification is met" with concrete conditions (e.g., "≥2 marketing email clicks OR pricing-page visit OR mid-intent form fill"). *Why:* an undefined predicate makes the spec non-build-ready at the exact spot evaluators probe.

**P1-4. Make the dedupe + update-branch logic build-ready** in Workflow 2. State *how* "has an open deal" is evaluated (association-count property / branch) and *what conditions* drive each update move (meeting type = Demo; property "Trial Started" = true). *Why:* this is the technically hardest part; vagueness here undercuts the "build scalable workflows" objective.

**P1-5. Add a labeled "Assumptions" block to the Part 1 written explanation (1f-i).** Pull the operating assumptions (deck Slide 3) into the draft explicitly. *Why:* the assignment names "assumptions" as a required submission element.

**P1-6. Consolidate to one presentation file.** Keep `case-study-deck-source.md` (or the outline) as canonical; delete/clearly-mark the other. *Why:* avoids ambiguity about the deliverable and KPI drift between them.

**P1-7. Split Entry / Exit into their own columns** in the §Part 2-A table (or bold them within the cell). *Why:* the assignment lists entry & exit criteria as a distinct requirement; making them scannable reads as more rigorous.

**P1-8. Represent Closed Won and Closed Lost as two stages** in the pipeline spec, matching how HubSpot actually models them.

### P2 — Nice to have

- **P2-1.** Add a **visual dashboard mockup** (even an ASCII/table wireframe) — the role is dashboard design; bullets under-sell it.
- **P2-2.** Replace the outbound appendix bullets with **one actual diagram** (per D5's "one diagram") and cut outbound from one of its three current mentions.
- **P2-3.** Name a concrete **tooling recommendation** in §Part 2-C (enrichment/dedup/data-quality tool) to satisfy that bullet fully.
- **P2-4.** Specify the **source of auto-stamped fields** (Estimated Amount, Close Date) in Workflow 2's create branch.
- **P2-5.** Add an explicit **re-enrollment / double-fire suppression** note given the overlapping triggers between the two workflows.

---

# HANDS-ON ITEMS (cannot be fixed by editing docs — keep for yourself)

These are required by the assignment but are *your* build/record work, not doc edits:

1. **Create the HubSpot account** — and decide the tier path. Recommended: start the **14-day Professional free trial** so Workflows/scoring/custom lifecycle stages are actually available (ties to P0-1).
2. **Build the 6-stage pipeline** in HubSpot (Closed Won + Closed Lost as separate stages).
3. **Build Workflow 1 (Lead Lifecycle)** — and capture screenshots of the enrollment trigger + branches.
4. **Build Workflow 2 (Deal Automation)** — including the dedupe branch; capture screenshots. Confirm the dedupe is actually achievable as designed (P1-4) — if not, adjust the spec to match what you built.
5. **Record the guidde walkthrough** (the "creative presentation," ~4–6 min per outline Slide 12) covering: GTM framing → lifecycle/PQL → pipeline & ownership → both workflows → dashboard.
6. **Take backup screenshots** of pipeline + workflows to embed in the deck (the deck promises these).
7. **Confirm the final submission package** goes to `yuval.haramaty@guidde.co` (per assignment p.4) and contains: written explanation (Part 1), Part 2 doc, Part 3 dashboard, the deck, and the guidde recording link.

---

## Bottom line

The thinking is coherent and the locked decisions D1–D4 are honored consistently — this is a competent strategic submission. But it is not yet submission-ready for a *Sales Ops* evaluator because of two substantive misses: (1) it never confronts that the HubSpot build it specifies **can't run on a free account** (D6 ignored, and it contradicts the assignment's own wording), and (2) the dashboard **fails to answer one of the four leadership questions it claims to answer** (revenue by motion). Fix those two, fill the name placeholder, complete the KPI definitions and the two soft workflow predicates, and the package goes from "good narrative" to "I can clearly tell this person operates HubSpot and builds dashboards."
