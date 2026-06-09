# Version 2 — README & Changelog

## Folder layout
```
260605 Guidde Case/
├─ Sales Operations Manager - Home assignment.pdf   ← source of truth (shared)
├─ Version 1/                                        ← archived v1 drafts + review
│   ├─ case-study-draft.md
│   ├─ case-study-deck-source.md
│   ├─ presentation-outline.md
│   └─ review-findings.md                            ← the critical review
└─ Version 2/                                        ← WORKING FILES (use these)
    ├─ 00-README-changelog.md                        ← this file
    ├─ case-study-v2.md                              ← main written deliverable (Parts 1–3)
    ├─ presentation-deck-v2.md                       ← single canonical deck (merged the 2 old files)
    └─ hubspot-build-guide.md                        ← hands-on build + record + submit checklist
```

## What's new in v2 (file consolidation)
- **Three drafts → two deliverables + one build guide.** v1's two overlapping presentation files are merged into one canonical deck. The written content lives in `case-study-v2.md`.
- All hands-on / "waiting-on" work is pulled into `hubspot-build-guide.md` so it's not lost.

---

## Changelog — every review finding → what changed

### P0 (blockers) — fixed in docs
| Finding (from review) | Resolution in v2 |
|---|---|
| **P0-1 Free-tier contradiction** — Workflows/scoring/custom stages are Pro, never acknowledged | Added Assumption #7 (case-study §0), tier notes on Slide 3 and at each workflow, and a full **Pro-trial vs free-tier decision** + fallback in the build guide |
| **P0-2 Dashboard didn't answer "what motions generate revenue?"** | Added a dedicated **Revenue by Motion** KPI group (won $, win rate, avg deal size, pipeline created — by Deal Source) + a question→KPI mapping table (Part 3.4) |
| **P0 hands-on** (build + recording not done) | Captured as the full `hubspot-build-guide.md` with step-by-step instructions and an open-items table |

### P1 (should-fix) — addressed
- **KPI definitions incomplete** → every listed KPI now has a definition (Part 3.3).
- **MQL trigger undefined** → now explicit: ≥2 email clicks OR pricing-page view OR mid-intent form (§1.4 step 2).
- **Dedupe not build-ready** → defined via a `Count of Open Deals` rollup property with explicit create/update branches (§1.5).
- **Update-branch routing implicit** → each move is now an explicit branch condition (Demo→Discovery, Trial Started→Evaluation).
- **No labeled assumptions** → §0 Assumptions block added.
- **Two duplicate decks** → merged into one canonical deck.
- **Entry/Exit buried in one column** → Part 2-A now has separate Entry and Exit columns.
- **Closed Won/Lost as one stage** → split into two stages (matches how HubSpot models terminal stages).
- **`Justin [Last Name]` placeholder** → flagged prominently as `[LAST NAME — fill before sending]` in every spot + an open-item checkbox. *(Still needs your real last name.)*

### P2 (nice-to-have) — addressed
- **No visual dashboard mockup** → added an ASCII wireframe (Part 3.2).
- **Outbound had no diagram** → added a diagram for the one-gate, two-motion model (appendix + Slide 11).
- **No concrete tooling rec** → named enrichment (Clearbit/Apollo), dedup/data-quality monitor, SLA alerting (Part 2-C).
- **Auto-stamped fields had no source** → Estimated Amount = plan×seats lookup; Close Date = today + standard cycle (§1.5).
- **Trigger double-fire risk** → added re-enrollment / "skip if already ≥ stage" control (§1.4 guardrails).

---

## Key takeaways to remember
1. **The single biggest risk was tool literacy, not strategy.** The strategy (PLG-hybrid, PQL, BDR/AE/CS, hybrid deal creation) was already sound and consistent. What would have sunk it with a Sales Ops evaluator was specifying a build that can't run on the "free account" the assignment names. v2 confronts that head-on.
2. **A dashboard must answer the exact questions it claims to.** v1 listed the four leadership questions but couldn't answer "what motions drive revenue." Always close that loop.
3. **"Build-ready" means no undefined predicates.** MQL criteria, dedupe mechanics, and auto-stamp sources are exactly where an interviewer probes. Spell them out.
4. **One canonical deck, not several.** Reduces drift and ambiguity about the deliverable.

## Still outstanding (decisions/actions only you can take)
See the open-items table at the bottom of `hubspot-build-guide.md`. Top three:
1. **Decide:** Pro 14-day trial (recommended) vs free-tier fallback.
2. **Do:** create account, build pipeline + 2 workflows, screenshot, record the guidde.
3. **Fill:** your real last name before sending.
