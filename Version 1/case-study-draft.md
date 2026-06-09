# Guidde Sales Operations Manager Case Study Draft

## Executive Framing
Guidde appears to operate in a PLG-hybrid go-to-market motion: free or low-friction product adoption creates intent signals, and the revenue team converts the right users into qualified pipeline, customers, and expansion opportunities. In that environment, Sales Operations should do three things well: define qualification logic, automate what is objective, and preserve human judgment where context matters.

This proposal is built around six design principles:
1. Product-qualified behavior should be the center of the qualification model.
2. Lifecycle stage and deal stage should be designed as separate but connected systems.
3. Deal creation should be hybrid: human qualification, system execution.
4. BDR, AE, and CS ownership should be explicit across the funnel.
5. Data quality should be protected through progressive field requirements and workflow guardrails.
6. Reporting should help leadership see performance, bottlenecks, and revenue opportunities quickly.

---

## Part 1. HubSpot Workflow and Automation Design

### A. Recommended Deal Pipeline
I would build a six-stage new-business pipeline in HubSpot:

1. **SQL / New Opportunity**  
   Sales has accepted the opportunity because fit and intent are confirmed.

2. **Discovery & Demo**  
   The team is running discovery, demo, or both to validate business need, use case, and urgency.

3. **Evaluation / Trial (POC)**  
   The prospect is actively testing the product through a pilot, guided evaluation, or trial motion.

4. **Proposal & Negotiation**  
   Pricing, packaging, commercial review, procurement, or negotiation is in progress.

5. **Verbal Commit / Contract Sent**  
   The buyer has given a verbal yes, and the contract or order form is out for signature.

6. **Closed Won / Closed Lost**  
   The opportunity has been resolved with a structured outcome.

### B. Why this pipeline fits Guidde
This structure is designed for a PLG-hybrid motion rather than a pure outbound enterprise motion. The funnel begins when product or high-intent signals justify sales engagement, not just when a rep decides to open a deal. It also creates clean operating checkpoints for BDR, AE, and CS while preserving forecasting clarity.

The most important design choice is that the pipeline does not start at “lead.” It starts at **SQL / New Opportunity**, because lifecycle stage answers “where is this person in the funnel?” while deal stage answers “where is this specific revenue opportunity?” That distinction is especially important for a product-led company where one account may generate multiple signals, multiple stakeholders, and potentially multiple deals over time.

### C. Lifecycle Model
I would manage the contact lifecycle separately from the deal pipeline using the following progression:

**Subscriber → Lead → MQL → PQL → SQL → Opportunity → Customer**

This is important because Guidde’s qualification model should treat product usage as a first-class signal. A contact becomes more valuable not only because they filled out a form, but because they demonstrated real in-product behavior.

### D. PQL Definition and Scoring Logic
I would make the PQL model the heart of the lifecycle design.

A contact becomes a **PQL** when they show one or more activation events such as:
- creating their first guidde
- publishing a guidde
- inviting a teammate

These events are not equal. Inviting a teammate is especially important because it can indicate collaboration, virality, and future expansion potential.

A sample lead score model:
- **+20** first guidde created
- **+15** teammate invited
- **+10** guidde published
- **+10** pricing page visit
- **+5** marketing email click
- **-10** no product use in 90 days

A score threshold such as **50** can be used to promote a PQL to SQL when explicit rep-engagement has not already happened. This gives the business two routes into sales qualification:
1. direct intent, such as a demo booking
2. accumulated high-intent product behavior

### E. Workflow 1: Lead Lifecycle Workflow
The purpose of the Lead Lifecycle Workflow is to move contacts through lifecycle stages automatically and consistently based on product and go-to-market signals.

**Enrollment triggers**
- Product signup or account creation
- Form submission, such as demo request, pricing inquiry, or high-intent content conversion
- Product activation behavior reaching the PQL threshold

**Workflow logic**
1. If a contact signs up or submits a relevant form, set lifecycle stage to **Lead** and stamp original source plus first-touch date.
2. If qualification criteria are met but intent is still light, promote the contact to **MQL**.
3. If the contact creates a guidde, publishes a guidde, or invites a teammate, promote the contact to **PQL**.
4. When a contact becomes a PQL, increase the lead score, stamp the PQL date, assign the Contact Owner through round-robin or segment logic, and notify the owner.
5. Promote the contact to **SQL** when any of the following happen:
   - a demo is booked
   - the BDR qualifies the contact
   - the PQL score crosses the threshold
   - pricing page activity or other high-intent behavior confirms commercial interest
6. When a deal is created and associated, promote the contact to **Opportunity**.
7. When an associated deal is Closed Won, promote the contact to **Customer**.

**Guardrails**
- Lifecycle progression should be **forward-only** unless an admin explicitly resets a record.
- Each move should stamp a **lifecycle change reason** and **lifecycle change date**.
- If a contact is already farther along, the workflow should skip backward changes.

**Why it matters**
This workflow improves scalability because sales engagement is triggered by qualified behavior instead of raw signup volume. It improves data hygiene because lifecycle changes are standardized and timestamped. It improves forecasting and team efficiency because the business knows exactly when a contact became interesting, why they were routed, and whether follow-up happened fast enough.

### F. Workflow 2: Deal Automation Workflow
The purpose of the Deal Automation Workflow is to create or update deals at the right moment, dedupe against existing pipeline, and enforce a consistent operating standard.

**Enrollment triggers**
- Contact lifecycle becomes **SQL**
- BDR marks a contact as **Qualified**
- A meeting of type **Demo** is booked

**Step 1: Dedupe check**
Before creating anything, the workflow checks whether the contact already has an open deal.

- **If an open deal exists:** update the existing deal.
- **If no open deal exists:** create a new deal.

**Create branch**
If no open deal exists:
- Create a deal in the **New Business** pipeline at **SQL / New Opportunity**.
- Set **Deal Source** to PLG if the signal originated in product usage; otherwise set it to Inbound, Outbound, or another defined source.
- Keep owner continuity by assigning the deal to the existing Contact Owner.
- Create a task for the owner to confirm scope, expected ACV, and next step within 48 hours.
- Stamp required starting properties such as ICP Fit, Product Interest, Estimated Amount, and Target Close Date.
- Notify the owner that a new qualified opportunity has been created.

**Update branch**
If an open deal already exists:
- If a demo is booked, move the deal to **Discovery & Demo**.
- If a trial or POC begins, move the deal to **Evaluation / Trial (POC)**.
- Re-stamp last activity date and refresh key engagement properties.

**Validation and accuracy controls**
- If a rep attempts to progress a deal without required fields, create an “Incomplete deal” task.
- If a deal sits in stage too long, create a stale-deal alert.
- If a deal is Closed Lost, require a structured Closed-Lost Reason.
- If a deal is Closed Won, trigger the CS handoff steps automatically.

**Why it matters**
This workflow supports the principle of “judgment by human, creation by system.” BDRs or high-intent signals determine whether the opportunity is real; HubSpot then standardizes execution so the team avoids missed deals, duplicate deals, and inconsistent field capture.

### G. How the Workflow Design Improves the Revenue Engine
**Scalability**  
The system scales sales effort around qualified volume rather than raw top-of-funnel volume. Product activity helps decide where reps should spend time.

**Data hygiene**  
Forward-only lifecycle logic, dedupe checks, required-field gates, and date stamps reduce messy CRM behavior.

**Forecasting**  
Consistent stage definitions, no duplicate open deals, and structured commercial fields produce more trustworthy pipeline reporting.

**Team efficiency**  
Automatic assignment, owner continuity, task creation, and CS handoff logic reduce manual triage and reduce the risk of dropped context.

---

## Part 2. Sales Process Design

### Part 2-A. Pipeline Structure and Stage Definitions

| Stage | Definition | Required Fields | Owner | Recommended Automation |
|---|---|---|---|---|
| **SQL / New Opportunity** | Entry: contact hits SQL through demo booked, PQL + score threshold, or BDR qualification. Exit: discovery is scheduled and fit is confirmed. | Deal Name, Deal Source, Estimated Amount, ICP Fit, Primary Contact, Use Case | **BDR** with routing to AE | Auto-create deal, dedupe check, assign owner, create 48h follow-up task |
| **Discovery & Demo** | Entry: discovery/demo is booked. Exit: need, stakeholders, and decision timeline are documented. | Pain/Need, Decision Timeline, Champion Identified | **AE** | Meeting logging, activity reminder if no movement in 5 days |
| **Evaluation / Trial (POC)** | Entry: guided evaluation, trial, or pilot begins. Exit: success criteria met and decision path confirmed. | Success Criteria, Trial Start/End, Active Users, Technical Fit | **AE** with **CS support** | Alert on low usage, notify CS for onboarding support |
| **Proposal & Negotiation** | Entry: pricing/proposal is sent. Exit: verbal agreement is reached. | Confirmed ACV, Plan/Seats, Decision Maker, Procurement/Legal Status | **AE** | Proposal reminders, deal-stuck alert if no movement for 14 days |
| **Verbal Commit / Contract Sent** | Entry: verbal yes and contract out. Exit: signed or stalled. | Contract Sent Date, Confirmed Close Date, Signatory | **AE** | Contract reminder, signature follow-up task |
| **Closed Won / Closed Lost** | Entry: deal is won or lost. Exit: terminal. | Won: Final ACV, Seats, CS Owner. Lost: Closed-Lost Reason, Competitor | **AE** to **CS** on Won | Won triggers onboarding handoff; Lost stamps structured reason and re-engage date |

### Why this pipeline design works
This design uses **progressive required fields** rather than forcing too much data at the start. Reps are less likely to enter bad data just to move a record forward. It also uses **objective exit criteria** rather than intuition alone, which is a core requirement for forecast quality.

Finally, ownership is explicit. BDR qualifies and routes. AE owns the active deal. CS enters early during trial or POC support and takes over post-sale on Closed Won.

### Part 2-B. Deal Creation Process
The deal creation process should combine rep judgment with automated execution.

**Who creates deals and when**  
The BDR makes the qualification decision. That decision should be based on a lightweight framework that combines ICP fit, product behavior, use case clarity, buying group signal, and reasonable urgency. Once that decision is made, HubSpot should create the deal automatically through the Deal Automation Workflow.

This is important for two reasons. First, it avoids missing legitimate opportunities because someone forgot to create a deal. Second, it avoids flooding the pipeline with low-quality records because the creation event still depends on human qualification or clear high-intent behavior.

**Mandatory properties at creation**  
At minimum, I would require:
- Deal Source
- Primary Contact
- ICP Fit
- Use Case
- Estimated Amount / ACV
- Buying Group or key stakeholder identified
- Expected Timeline
- Product Interest

**Validation rules**  
- No duplicate open deals for the same contact or account without admin review
- Closed-Lost Reason must be a picklist, not free text
- Required fields should increase by stage, not all at once
- Incomplete deal records trigger follow-up tasks before progression

**Automations that maintain accuracy**  
- Auto-create the deal when qualification criteria are met
- Auto-assign ownership from the Contact Owner for continuity
- Create follow-up tasks at creation and at key stage transitions
- Stamp milestone dates automatically when stages change
- Trigger stale-deal alerts when activity or movement stops

**How this supports forecasting**  
Forecasting improves when opportunities are created consistently, deduped consistently, and advanced with the same rules. A clean deal creation process means leaders can trust stage-based conversion rates, weighted pipeline, and projected close dates more than they could in a manually managed CRM.

### Part 2-C. Risks, Bottlenecks, and Opportunities
A PLG-hybrid motion creates a powerful opportunity, but it also creates operational risk if qualification logic is loose. The first risk is over-routing low-value PQLs into sales, which can waste BDR and AE time and reduce trust in product signals. The second risk is under-routing real buying intent because product events are not mapped cleanly into lifecycle stages or because ownership rules are unclear. Both risks can be reduced by using explicit activation rules, score thresholds, and SLA monitoring for follow-up.

Another likely bottleneck is the transition from trial activity to commercial motion. In a product like Guidde, prospects may clearly use the product without clearly indicating buying process, champion strength, or timeline. That makes the **Evaluation / Trial (POC)** stage especially important. Sales Ops should treat this stage as a structured conversion checkpoint, not just a waiting room. Success criteria, active-user counts, and CS-supported onboarding signals can make this stage far more diagnostic.

The biggest data-reliability risk is inconsistent stage movement, weak loss-reason capture, and poor handoffs between AE and CS. The answer is not more free-text notes. It is structured fields, progressive stage requirements, task automation, and picklists that can be analyzed later. As an extensibility opportunity, outbound enrichment and ICP scoring can sit as a light appendix motion feeding the same SQL gate. That gives Guidde one unified pipeline with two acquisition on-ramps instead of fragmented systems.

### Appendix: Outbound On-Ramp
The two required workflows should govern the core funnel, which is PLG-led. Outbound should be treated as a secondary on-ramp rather than the center of the process.

A simple model:
- PLG path: free signup → activation → PQL → SQL gate → deal stages
- Outbound path: target list → enrichment → ICP scoring → sequence → reply/meeting accepted → SQL gate → deal stages

This keeps the operating model clean: one pipeline, two acquisition motions, one SQL gate, and one set of stage definitions for forecasting.

---

## Part 3. Dashboard and KPI Reporting Design

### A. Dashboard Design Principles
The dashboard should help leadership answer four practical questions quickly:
1. Who is performing best?
2. What activities or motions generate the most revenue?
3. Where are the bottlenecks in the pipeline?
4. What changes are most likely to increase revenue?

To do that, I would structure the dashboard into three KPI groups that match the assignment brief, plus a top summary layer.

### B. Dashboard Outline

**Executive summary row**
- Open pipeline amount
- Commit / best-case forecast
- Closed won this period
- Average sales cycle length

**1. Pipeline and Forecasting KPIs**
- Pipeline by stage
- Pipeline coverage vs target
- Stage-to-stage conversion rates
- Weighted pipeline by quarter
- Commit accuracy or forecast accuracy
- Average days in stage

**2. Sales Performance KPIs (Per Rep + Team Level)**
- Closed won amount by rep
- Win rate by rep
- SQL to Closed Won conversion by rep
- Average deal size by rep
- Pipeline created by rep
- Closed-lost reasons by rep and team

**3. Productivity and Efficiency KPIs**
- Time from PQL to first sales action
- Demo booked rate from SQL
- Discovery to trial conversion rate
- Trial/POC to proposal conversion rate
- Meetings held per rep
- Follow-up SLA attainment
- Won-deal handoff completion rate

### C. KPI Definitions
**Pipeline by stage**  
The amount and count of open opportunities sitting in each deal stage.

**Pipeline coverage vs target**  
Open pipeline divided by the next period’s quota target.

**Weighted pipeline by quarter**  
Open pipeline multiplied by stage probability, rolled up by expected close quarter.

**Forecast accuracy**  
Forecasted closed won amount compared with actual closed won amount.

**Closed won amount by rep**  
Revenue closed in the selected period by account executive.

**Win rate by rep**  
Closed Won deals divided by total resolved deals by rep.

**SQL to Closed Won conversion**  
The percentage of SQL opportunities that convert to won deals.

**Average deal size**  
Average final ACV of won deals.

**Time from PQL to first sales action**  
Elapsed time between the PQL timestamp and the first logged rep action.

**Demo booked rate from SQL**  
The percentage of SQL opportunities that progress into Discovery & Demo.

**Discovery to trial conversion**  
The percentage of Discovery & Demo opportunities that progress into Evaluation / Trial (POC).

**Trial/POC to proposal conversion**  
The percentage of Evaluation / Trial opportunities that move into Proposal & Negotiation.

**Average days in stage**  
Average time a deal spends in each stage before progressing or closing.

**Won-deal handoff completion rate**  
The percentage of won deals with all required CS handoff fields and onboarding tasks completed.

### D. Why this dashboard matters
This dashboard balances performance, efficiency, and pipeline quality. It helps leadership see not only who is closing business, but also what kind of demand is converting, where opportunities are slowing down, and whether operating discipline is strong enough to trust the forecast.

### E. Creative Presentation Format
The strongest presentation format is to record the solution as a **guidde walkthrough**. That directly matches the company’s product and demonstrates communication skill in the same medium Guidde sells.

I would present the work in this order:
1. Explain the GTM logic and why Guidde should be treated as a PLG-hybrid business.
2. Show the lifecycle model and explain why PQL is the central qualification concept.
3. Walk through the deal pipeline and ownership model.
4. Show the two workflows in HubSpot.
5. Close with the dashboard design and how leadership would use it.

If a live HubSpot build is not available, I would still present the workflow logic as build-ready specifications and support the walkthrough with screenshots, diagrams, and mock pipeline views.

---

## Closing Note
My approach is intentionally practical. I would automate what is objective, standardize what is repetitive, and preserve human judgment where context matters. For a PLG-hybrid SaaS company like Guidde, that is the operating model most likely to improve scalability, data hygiene, forecasting accuracy, and team efficiency at the same time.
