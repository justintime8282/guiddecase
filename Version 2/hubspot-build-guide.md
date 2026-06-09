# HubSpot Build & Submission Guide (v2) — Hands-On Work

This is the **do-it-yourself checklist** for everything that can't be produced as a document. The case study (`case-study-v2.md`) is the spec; this guide is how you turn it into a real build + recording + submission.

> **Critical decision first:** the two required workflows, custom lifecycle stages, and rotate-owner actions are **HubSpot Professional features — not in the free tier.** The assignment says "free account," so you must decide how to handle the gap. **Path taken: built on the 14-day Sales Hub Professional free trial** (no charge, full Workflows access), with this assumption stated explicitly in the writeup. Do not submit a build that silently relies on paid features without acknowledging it — a Sales Ops evaluator will notice.
>
> **Tier nuance discovered mid-build:** Workflows, custom lifecycle stages, and rotate-owner live in **Sales Hub Pro** (the trial used here). But **native contact lead scoring is *Marketing* Hub Pro** — a separate subscription not in this trial. So lead scoring was **not** built live; the §1.2 model is documented as design, and Workflow 1 uses **direct product-activation triggers** as the buildable equivalent (single event → PQL; 2+ events / BDR-qualified / demo → SQL). With a full Marketing + Sales stack it runs as a live `HubSpot Score`.

---

## Step 0 — Account setup
- [ ] Create a free HubSpot CRM account (work or personal email).
- [x] Start the **Sales Hub Professional 14-day free trial** to unlock Workflows and custom lifecycle stages. *(Settings → expand a Pro feature → "Try for free.")* **Note:** native contact lead scoring needs **Marketing Hub Pro** (separate) — not activated; see scoring note below.
- [ ] **Plan your timing:** the trial is 14 days. Do the build + screenshots + recording within that window, then submit. Don't start the trial until you're ready to build.
- [ ] In your writeup/deck, add the one-line tier note (already in `case-study-v2.md` §0 assumption 7 and Slide 3).

**If you choose NOT to use the trial:** build the pipeline + properties (free), then *document* the two workflows as build-ready specs with the free-tier fallback (manual SOP + saved lists) called out. This is weaker for a "build workflows" assignment — only fall back if the trial is unavailable.

---

## Step 1 — Build the pipeline (free tier OK)
- [x] Settings → Objects → Deals → Pipelines → create **"New Business."**
- [x] Add the 7 stages with these win probabilities (edit later as you like):
  1. SQL / New Opportunity — 10%
  2. Discovery & Demo — 25%
  3. Evaluation / Trial (POC) — 45%
  4. Proposal & Negotiation — 65%
  5. Verbal Commit / Contract Sent — 85%
  6. **Closed Won** — 100% (mark as won)
  7. **Closed Lost** — 0% (mark as lost)
- [x] Screenshot the finished pipeline board.

---

## Step 2 — Create custom properties
Build these before the workflows (the workflows reference them).

**Contact properties:**
- [ ] `First guidde created` (single checkbox / bool) — *normally set by product→HubSpot integration; for the demo, set manually or via a test form.*
- [ ] `Guidde published` (bool)
- [ ] `Teammate invited` (bool)
- [ ] `PQL Date` (date)
- [ ] `Lifecycle Change Reason` (dropdown)
- [ ] `BDR Qualified` (bool)
- [ ] `Count of Open Deals` (number — populated by rollup/data-quality automation; see Step 4)
- [ ] **Lead scoring — NOT built (requires Marketing Hub Pro, not in the Sales Hub trial).** The §1.2 point model is documented as design; Workflow 1 uses direct product-activation branches as the equivalent (single event → PQL; 2+ events / BDR-qualified / demo → SQL). *With Marketing Hub Pro:* configure §1.2 in Settings → Lead Scoring → populates the read-only `HubSpot Score`.
- [ ] Add custom **lifecycle stage `PQL`** between MQL and SQL (Pro). *On free, skip and use an active list instead.*

**Deal properties:**
- [ ] `Deal Source` (dropdown: PLG / Inbound / Outbound)
- [ ] `ICP Fit` (dropdown)
- [ ] `Use Case` (dropdown)
- [ ] `Product Interest` (dropdown)
- [ ] `Closed-Lost Reason` (dropdown — required on Closed Lost)
- [ ] `Competitor` (dropdown)
- [ ] Progressive stage fields from the Part 2-A table (Champion Identified, Success Criteria, Confirmed ACV, etc.)

---

## Step 3 — Workflow 1: Lead Lifecycle (Pro)
- [ ] Contact-based workflow.
- [ ] **Enrollment (OR):** `First Guidde Created = true` OR `Guidde Published = true` OR `Teammate Invited = true` OR `BDR Qualified = true`. *(Product-activation triggers — the build-equivalent of the §1.2 score, since native scoring needs Marketing Hub Pro.)*
- [ ] Build the lifecycle promotion branches exactly per `case-study-v2.md` §1.4 (Lead → MQL → PQL → SQL → Opportunity → Customer).
- [ ] Add forward-only guardrail branch ("if current stage ≥ target, skip").
- [ ] Add rotate-owner action + internal notification on PQL.
- [ ] Stamp `Lifecycle Change Reason` + date on each move.
- [ ] **Test:** create 2–3 test contacts, fire each trigger, confirm correct stage moves. Screenshot the workflow canvas + a test contact's timeline.

---

## Step 4 — Workflow 2: Deal Automation (Pro)
- [ ] First, set up the **`Count of Open Deals` rollup** (Data Quality automation or a small helper workflow that counts associated open deals) so dedupe can branch on it.
- [ ] Contact-based workflow. **Enrollment (OR):** Lifecycle=SQL OR `BDR Qualified=true` OR Demo meeting booked.
- [ ] **Dedupe branch:** `Count of Open Deals = 0` → Create; `≥1` → Update.
- [ ] **Create branch:** create deal at SQL stage; set Deal Source; owner = Contact Owner; stamp ICP/Use Case/Product Interest/Estimated Amount/Target Close Date; create 48h task; notify owner.
- [ ] **Update branch:** Demo→Discovery; `Trial Started`→Evaluation; refresh `Last Activity Date`.
- [ ] Add validation: incomplete-deal task/hold; stale-deal alert; require Closed-Lost Reason; CS handoff on Closed Won.
- [ ] **Test:** run a contact with no deal (expect create) and one with an open deal (expect update). Screenshot both outcomes.

---

## Step 5 — (Optional but strong) Seed sample data for the dashboard
- [ ] Import or hand-create ~15–25 deals across stages, reps, and Deal Sources so the dashboard mockup has something to show.
- [ ] This makes the "revenue by motion" and per-rep KPIs render as real charts in screenshots.

*(Note: Part 3 does NOT require building the dashboard in HubSpot — design only. Building it is bonus polish for the recording.)*

---

## Step 6 — Record the guidde walkthrough (the "creative presentation")
- [ ] Install the guidde Chrome extension / app (free).
- [ ] Record ~4–6 minutes in this order: GTM framing → lifecycle & PQL → pipeline & ownership → Workflow 1 → Workflow 2 → dashboard.
- [ ] Capture the HubSpot pipeline + both workflow canvases on screen.
- [ ] Export the shareable guidde link.
- [ ] Keep static screenshots as backup in case the reviewer can't open the link.

---

## Step 7 — Final submission package (email to yuval.haramaty@guidde.co)
- [ ] **Fill in your last name** everywhere it says `[LAST NAME]` (case-study-v2.md, deck Slides 1, build screenshots).
- [ ] Written explanation — Part 1 logic + assumptions + scalability/hygiene/forecasting/efficiency (from `case-study-v2.md`).
- [ ] Part 2 doc — pipeline table, deal creation, risks.
- [ ] Part 3 — dashboard outline + KPI definitions.
- [ ] The deck (export `presentation-deck-v2.md` to slides) OR a clean PDF.
- [ ] The **guidde recording link**.
- [ ] HubSpot screenshots (pipeline + 2 workflows + sample dashboard if built).
- [ ] Short, friendly cover email.

---

## Open items / waiting on you
| Item | Owner | Status |
|---|---|---|
| HubSpot account + Pro trial start | You | ⏳ pending |
| Pipeline build + screenshot | You | ⏳ pending |
| Workflow 1 build + test screenshots | You | ⏳ pending |
| Workflow 2 build + test screenshots | You | ⏳ pending |
| guidde recording | You | ⏳ pending |
| Fill in real last name | You | ⏳ pending |
| Confirm free-tier vs Pro-trial decision | You | ⏳ decision needed |

Once the account exists and you've started the build, share screenshots and I can sanity-check the workflow logic against the spec and tighten the deck.
