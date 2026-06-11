# External Feedback — Review & Assessment

> Two reviewers looked at the Guidde Sales Ops case study. This file captures their feedback, my assessment of how valid each point is, and what we changed in response. Last updated: 2026-06-09.

**Reviewers**
- **Chris Singlemann** — senior rev-ops perspective (experienced operator; substantive, model-level critique). Frames most points as *"be ready to speak to this in the presentation,"* with the **dashboard** being the one area he'd make real changes.
- **Aubrie Lankford** — rapid-fire reactions while scrolling the report; explicitly *"take or leave, I don't have the company context."* Mostly positive + UX polish + two substantive flags.

**Validity key:** 🟢 very valid (act / be ready) · 🟡 valid (worth reflecting) · ⚪ minor / taste

**Overall verdict:** both positive. Structure, assumptions-first framing, and using guidde to demo all landed well ("looks fantastic," "great stuff"). The high-value notes are Chris's model-level points; several of them are actually opportunities to *strengthen* decisions we already made (e.g., scoping MQL out for tier reasons → reframe as a deliberate "PQL is the gate" stance).

---

## Tier 1 — most valid, addressed

### 1. MQL vs PQL definition clash 🟢 (Chris)
> "Does MQL come before PQL? Can they skip / be both? If trial = PQL, why would sales focus on MQL? MQL can become a vanity metric." Offered an **Intent-Qualified Lead (IQL)** alternative (trial started OR demo requested).

**Assessment:** the single sharpest point — names exactly what kills hybrid PLG programs. PQL (product use) dominates MQL (engagement), so a heavy MQL→PQL hand-off is low value. Connects directly to our tier decision to drop the MQL marketing branch — we can reframe that from "couldn't build it" to "deliberately keep MQL lightweight; PQL is the gate."
**Reflected:** added a "Why PQL — not MQL — is the gate" note in Part 1, incl. the IQL alternative.

### 2. PQL data architecture / integration 🟢 (Chris) + (Aubrie)
> Chris: "How does product data get into HubSpot? Product analytics ↔ CRM integration? Clean PQL is impossible without good data architecture — flag it in the implementation plan." Aubrie: "You can pass marketing data through to the contact if you want to measure it."

**Assessment:** real implementation gap — we hand-waved "set by product→HubSpot integration." SaaS product-analytics↔CRM hygiene is notoriously weak. Naming the pipeline (native integration / Segment / reverse-ETL) shows operational depth.
**Reflected:** added an "Implementation dependency — how product signals reach HubSpot" note in Part 1.

### 3. Pipeline stage weights from historic win rates 🟢 (Chris)
> "Are weights from Guidde data? Usually you set them from historic win rates by stage (win 50% at Evaluation → raise above 45%)."

**Assessment:** correct and easy. Our 10/25/45/65/85 are defaults. Flagging calibration shows data-driven thinking.
**Reflected:** added a "stage weights are illustrative defaults, calibrated to historic win rates" note under the pipeline.

### 4. Deal creation timing — SQL deal stage vs "Opportunity" lifecycle 🟢 (Chris) + (Aubrie)
> Chris: "Confusing what prompts deal creation. Deal should be created at **SQL** (keep SQL as the first deal stage), and the contact should transition to **Opportunity** when the deal moves SQL → Discovery." Aubrie: "Auto-creating a deal on 2+ activation events may over-inflate that stage — be ready to speak to it."

**Assessment:** **NOT a request to remove SQL from the deal pipeline** — Chris explicitly endorses SQL as the first deal stage. The issue is the *lifecycle* "Opportunity" timing: HubSpot's native "deal created → Opportunity" fires while the deal is still at SQL, so the person reads as "Opportunity" before any real progress. Cleaner: lifecycle → Opportunity on SQL → Discovery.
**Reflected:** added a "deal creation vs Opportunity" clarification under the pipeline (Opportunity = deal actively worked, fires on SQL→Discovery, not on mere creation).
**Still to decide (build):** A) keep native + define clearly, or B) turn off native toggle and drive lifecycle→Opportunity from deal stage = Discovery via workflow (can fold into WF2).

---

## Tier 2 — valid, partially reflected / be ready

### 5. PLG vs inbound/outbound as "motions" 🟡 (Chris) — *his one real dashboard change*
> "PLG against inbound/outbound isn't a recommendation I'd make — inbound/outbound *support* the motion. Even sales-led has both. The chart should be the channel driving the most PQLs (Sales, referral, inbound, etc.)."

**Assessment:** conceptually sharper — PLG is the GTM *motion*; inbound/outbound/referral are *channels* feeding it. Mixing them is a category error. (Counter: many PLG orgs do track self-serve vs sales-assisted as motions, so defensible — but his framing is cleaner.)
**Reflected:** renamed the dashboard cut "Revenue by Motion" → **"Revenue by Source"** (acquisition source), updated the four-questions language, and added an "on framing & feasibility" note (PLG = motion; sources feed it; sharper question = which source drives the most PQLs).

### 6. Dashboard feasibility / native HubSpot 🟡 (Chris) — *where he'd make real changes*
> "Illustrative data suggests it's shown outside HubSpot's native reporting. Index on layout/UX over illustrating data — otherwise it makes me question whether what you're showing is possible vs. the (strong) narrative."

**Assessment:** legitimate. Most of our KPIs are buildable as HubSpot reports; a few polished cuts would need a BI layer. The "illustrative" watermark we added already signals it's a mockup.
**Reflected:** added a feasibility line (native HubSpot for most KPIs; BI layer for polished cuts; mockup illustrates layout, not a claim every view is a stock chart). Watermark "ILLUSTRATIVE DATA" already on both dashboards.

### 7. "Ask the right questions" meta-frame 🟡 (Chris)
> "Highest signal of a rev-ops candidate is knowing what to plan for AND what questions to ask. Asking the right questions reads as more capable than being prescriptive."

**Assessment:** true and high-signal. Tier-1 items #1–4 are essentially the questions to raise with the team. Best handled as presentation framing / an "open questions to validate" talk track.
**Reflected:** the new notes are written as design choices + things to validate. *Talk-track item for the live presentation.*

---

## Tier 3 — UX / minor (Aubrie)

| # | Feedback | Validity | Status |
|---|---|---|---|
| 8 | Add a label like "Approach:" to the hero thesis line | ⚪ | optional polish — easy |
| 9 | Mobile: horizontal pipeline shows as stacked columns → tell them to view on laptop | ⚪ practical | add "best viewed on desktop" note or make responsive |
| 10 | "What is guidde? A recording platform?" | ⚪ | the actual audience (Guidde) knows their product — low priority; a one-liner wouldn't hurt |
| 11 | "Not sure this section is needed" (video-pairing callout) | ⚪ debatable | she lacks company context; the callout is useful for the submission — keep or trim |

---

## What changed in the deliverable (`case-study-report.html`)
- Added: **Why PQL not MQL is the gate** note (#1)
- Added: **product-signal data architecture** note (#2)
- Added: **stage weights = win-rate calibration** + **Opportunity timing** note (#3, #4)
- Reframed: dashboard **"Revenue by Motion" → "Revenue by Source"** + framing/feasibility note (#5, #6)
- Updated: four-questions language and question→KPI table to "channels/sources"

## Still open (decide / discuss)
- **Build:** Opportunity-timing — keep HubSpot native vs. custom workflow on deal stage = Discovery (#4, fold into WF2).
- **Talk track:** MQL-vs-PQL / IQL stance (#1), data-hygiene risk (#2), "questions I'd ask the team" framing (#7).
- **Optional UX:** hero label, mobile note (#8, #9).
- **Not changing:** SQL stays the first deal stage (Chris endorsed it) — do not remove it.
