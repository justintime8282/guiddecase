# Guidde Sales Operations Manager Case Study Deck Source

Use this as the fastest copy-paste source for Google Slides, Keynote, or PowerPoint.

---

## Slide 1. Title
**Guidde Sales Operations Manager Case Study**

Justin [Last Name]

Designing a scalable Sales Ops system for a PLG-hybrid revenue motion

---

## Slide 2. Executive Summary
**Objective**
Build a practical Sales Ops framework that turns product intent into clean pipeline, reliable execution, and usable forecasting.

**What I designed**
- 6-stage HubSpot pipeline
- PQL-centered lifecycle framework
- 2 workflows: Lead Lifecycle + Deal Automation
- Explicit BDR, AE, and CS ownership
- KPI dashboard for performance, bottlenecks, and revenue opportunities

**Core principle**
Automate what is objective, preserve human judgment where context matters.

---

## Slide 3. Why this model fits Guidde
**Operating assumptions**
- Guidde fits a PLG-hybrid GTM motion
- Product usage should be a primary qualification input
- One person can move through lifecycle without necessarily creating a deal yet
- Revenue ownership spans BDR, AE, and CS

**Key framing**
Lifecycle stage answers: *Where is this person in the funnel?*  
Deal stage answers: *Where is this revenue opportunity?*

---

## Slide 4. Lifecycle Model
**Recommended lifecycle progression**
Subscriber → Lead → MQL → **PQL** → SQL → Opportunity → Customer

**Why PQL matters**
PQL should sit at the center of the model because Guidde’s strongest intent signals come from product behavior, not just form fills.

**Activation examples**
- First guidde created
- Guidde published
- Teammate invited

---

## Slide 5. Pipeline Design
**Recommended HubSpot pipeline**
1. SQL / New Opportunity
2. Discovery & Demo
3. Evaluation / Trial (POC)
4. Proposal & Negotiation
5. Verbal Commit / Contract Sent
6. Closed Won / Closed Lost

**Why this works**
- Clean ownership checkpoints
- Stronger conversion visibility
- Better forecasting discipline
- Built for PLG-led sales engagement

---

## Slide 6. Workflow 1: Lead Lifecycle Workflow
**Enrollment triggers**
- Product signup
- Demo or pricing form submission
- Product activation threshold reached

**Workflow logic**
- Lead on signup/form
- MQL when marketing qualification is met
- PQL when activation criteria are met
- SQL on demo booked, BDR qualification, or score threshold
- Opportunity when a deal is created
- Customer when a deal is Closed Won

**Guardrails**
- Forward-only progression
- Lifecycle reason/date stamping
- Owner assignment and notification

---

## Slide 7. Workflow 2: Deal Automation Workflow
**Enrollment triggers**
- Lifecycle becomes SQL
- BDR marks contact Qualified
- Demo meeting booked

**Step 1: Dedupe check**
- If open deal exists → update it
- If no open deal exists → create it

**Create branch**
- Create deal in SQL / New Opportunity
- Set Deal Source
- Keep Contact Owner continuity
- Create 48-hour follow-up task
- Stamp ICP Fit, Product Interest, Est. Amount, Close Date

**Update branch**
- Demo booked → move to Discovery & Demo
- Trial started → move to Evaluation / Trial (POC)
- Refresh activity signals

---

## Slide 8. Pipeline Governance and Ownership
**BDR**
- Reviews PQL and high-intent signals
- Applies qualification judgment
- Routes qualified opportunities

**AE**
- Owns discovery, evaluation, proposal, and close

**CS**
- Supports trial/onboarding motion
- Owns post-sale handoff on Closed Won
- Feeds adoption and expansion signals back into CRM

**Ops layer**
- Progressive required fields
- Objective exit criteria
- Structured handoffs

---

## Slide 9. Deal Creation Process
**Philosophy**
Judgment by human, creation by system.

**Required creation fields**
- Deal Source
- Primary Contact
- ICP Fit
- Use Case
- Estimated Amount / ACV
- Buying Group
- Expected Timeline
- Product Interest

**Accuracy controls**
- No duplicate open deals
- Incomplete-deal tasks
- Stale-deal alerts
- Structured Closed-Lost Reason

---

## Slide 10. Risks, Bottlenecks, and Opportunities
**Key risks**
- Low-quality PQLs overwhelming sales
- Missed high-intent users due to weak routing
- Dirty stage data and poor CS handoff

**Key bottleneck**
- Trial/POC stage can become a waiting room unless success criteria and usage signals are structured

**Opportunity**
- Add outbound enrichment and ICP scoring as a light appendix feeding the same SQL gate

---

## Slide 11. Dashboard and KPI Design
**Pipeline & Forecasting**
- Pipeline by stage
- Pipeline coverage vs target
- Weighted pipeline by quarter
- Forecast accuracy
- Average days in stage

**Sales Performance (Per Rep + Team)**
- Closed won amount by rep
- Win rate by rep
- SQL to Closed Won conversion
- Average deal size
- Pipeline created by rep

**Productivity & Efficiency**
- Time from PQL to first sales action
- Demo booked rate from SQL
- Discovery to trial conversion
- Trial to proposal conversion
- Follow-up SLA attainment
- Won-deal handoff completion rate

---

## Slide 12. Creative Presentation Format
**Best format**
Record the solution as a guidde walkthrough.

**Why**
- Uses Guidde’s own product as the presentation medium
- Demonstrates communication clarity
- Makes the HubSpot build easy to review

**Suggested walkthrough order**
1. GTM framing
2. Lifecycle and PQL logic
3. Pipeline and ownership model
4. Workflow 1
5. Workflow 2
6. Dashboard and KPI view

---

## Slide 13. Closing
**Summary**
A practical, startup-ready Sales Ops design for a PLG-hybrid motion:
- product-signal-led qualification
- clear ownership across BDR, AE, and CS
- hybrid deal creation logic
- cleaner forecasting and stronger execution

**Closing line**
Thank you for the opportunity. I would be excited to discuss how I would adapt this model to Guidde’s live data, team structure, and growth priorities.
