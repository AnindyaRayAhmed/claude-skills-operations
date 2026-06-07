# SaaS Client Onboarding — Skill Output

**Claude's response:**

---

Let me restate the workflow as I understand it before proceeding — confirm or correct anything I've got wrong.

**Workflow: New Client Onboarding (B2B SaaS)**

```
Step 1: Sales closes deal → sends unstructured email to ops
  Input:    Signed deal
  Output:   Email with partial client info
  Tool:     Email
  Handoff:  Ops team
  Tag:      [MANUAL] [HANDOFF]

Step 2: Ops retrieves remaining details from Salesforce
  Input:    Sales email + Salesforce record
  Output:   Complete client data (ideally)
  Tool:     Salesforce + email cross-reference
  Tag:      [MANUAL] [TOOL-ASSISTED]

Step 3: Ops creates client account in platform
  Input:    Client data from Step 2
  Output:   Active platform account
  Tool:     Internal platform (manual entry)
  Tag:      [MANUAL]

Step 4: Ops sends welcome email to client
  Input:    Account created
  Output:   Welcome email sent
  Tool:     Email (template assumed)
  Tag:      [MANUAL]

Step 5: Ops schedules kickoff via email back-and-forth
  Input:    Welcome email sent
  Output:   Confirmed kickoff time
  Tool:     Email
  Duration: 1–4 days elapsed [OBSERVED]
  Tag:      [MANUAL] [WAIT] [BOTTLENECK]

Step 6: Ops assigns CSM
  Input:    Kickoff confirmed
  Output:   Named CSM on account
  Tool:     Unknown — capacity-based [ASSUMPTION]
  Tag:      [MANUAL] [DECISION]

Step 7: CSM reviews Salesforce pre-kickoff
  Input:    Salesforce record
  Output:   CSM prepared for kickoff
  Tool:     Salesforce
  Tag:      [TOOL-ASSISTED] [WAIT — clarification loop]
```

Does this match how things actually run? I'll proceed on the assumption it does, flagging anything inferred.

---

## OPERATIONAL WORKFLOW AUDIT

**Workflow:** New Client Onboarding
**Volume:** 15–20 clients/month [OBSERVED]
**Stated problems:** 2–3 day delay before client contact; CSMs underprepared at kickoff [OBSERVED]

---

### EXECUTIVE SUMMARY

This onboarding workflow has three compounding problems: an unstructured handoff at the start that creates data loss, a scheduling loop in the middle that is the primary driver of the 2–3 day delay, and an information gap at the end that leaves CSMs under-prepared. None of these are complex to fix individually. Together, they create a first impression problem that will worsen linearly with scale. The highest-leverage first move is not automation — it is standardizing the sales-to-ops handoff. Everything else flows from that.

**Overall Efficiency Rating: 4/10**
**Primary Inefficiency Type:** Handoff + Communication
**Estimated weekly time lost:** ~6–9 hrs/week across team [ESTIMATED — based on 15–20 clients/month]
**Priority improvement:** Replace the email handoff (Step 1) with a structured deal-close form that auto-populates ops and triggers account creation

---

### DIAGNOSTIC FINDINGS

#### Bottlenecks

**BOTTLENECK 1: Unstructured sales-to-ops handoff (Step 1)**
BSS: 8.2 / 10 — Critical

- Frequency: Every single client (15–20/month)
- Cascade: Forces Step 2 (manual Salesforce lookup), increases error risk in Step 3, and delays every downstream step
- Root cause: No standardized handoff format; sales sends what they remember
- Symptom: Ops must reconcile email + Salesforce before doing anything productive

**BOTTLENECK 2: Kickoff scheduling via email (Step 5)**
BSS: 8.6 / 10 — Critical

- Frequency: Every single client
- Elapsed time: 1–4 days [OBSERVED] — this is the direct cause of the 2–3 day client silence complaint
- Root cause: No scheduling tool in use; manual email negotiation for a task that is fully automatable
- Single fix potential: Calendly or equivalent eliminates this entirely at near-zero cost

**BOTTLENECK 3: Incomplete Salesforce records causing CSM clarification loop (Step 7)**
BSS: 6.0 / 10 — High

- Frequency: "Usually" — [OBSERVED], implies majority of clients
- Cascade: Adds async delay before kickoff; CSM goes in underprepared
- Root cause: Salesforce hygiene is a sales responsibility that isn't enforced; problem starts at Step 1

---

#### Repetitive Manual Tasks

| Task | Frequency | Estimated time | ASI Score | Recommendation |
|---|---|---|---|---|
| Account creation in platform (Step 3) | 15–20x/month | ~20 min/client | 4.6 | Automate via CRM→platform sync |
| Welcome email send (Step 4) | 15–20x/month | ~10 min/client | 4.8 | Automate — triggered on account creation |
| Salesforce data retrieval (Step 2) | 15–20x/month | ~15 min/client | 2.1 | Eliminate by fixing Step 1 |

---

#### Communication Inefficiencies

| Pattern | Where | Impact |
|---|---|---|
| Unstructured email as handoff mechanism | Step 1 | Data loss, ambiguity, ops re-work |
| Email scheduling back-and-forth | Step 5 | 1–4 day delay, poor client experience |
| Verbal/informal CSM assignment | Step 6 | No audit trail, unclear capacity logic [ASSUMPTION] |
| CSM→ops clarification loop | Step 7 | Async delay, repeated effort, information arriving too late |

---

#### Dependency Issues

Critical path: Step 1 → Step 2 → Step 3 → Step 4 → Step 5 → Step 6 → Step 7

Every step is sequential. No parallelization currently exists. Opportunities:
- Steps 3 + 4 could be triggered simultaneously once data is clean [PARALLELIZABLE]
- Step 6 (CSM assignment) could happen at Step 1 (deal close) if assignment criteria are defined [PARALLELIZABLE]
- Step 7 prep could be automated from CRM data rather than manual review [PARALLELIZABLE with Step 5]

**Hidden dependency:** Steps 2, 3, and 7 all depend on Salesforce record quality — which depends on sales discipline. This is a `[RESOURCE-CONFLICT]` — the same data quality problem surfaces in three places.

---

### RECOMMENDATIONS

---

**REC-1: Replace email handoff with a structured deal-close form**
**Type:** Standardize
**Priority:** P1 Quick Win — Impact: High × Feasibility: High
**Targets:** Step 1, Step 2
**Current state:** Sales sends a freeform email; ops cross-references Salesforce to fill gaps
**Proposed change:** Build a short form (Google Form, Typeform, or native CRM field set) that sales completes at deal close. Required fields: client name, plan tier, primary contact email, special requirements, expected go-live date. Form submission notifies ops with complete data and optionally triggers Step 3 automatically.
**Expected outcome:** Eliminates Step 2 entirely; reduces ops intake time from ~15 min to ~2 min; improves data quality for Steps 3, 6, and 7
**Estimated effort:** 2–3 days to build and roll out
**ROI horizon:** Immediate — recovers ~3.75 hrs/month in ops time [ESTIMATED]
🟡 ADOPTION risk: Sales may resist an extra step at close. Mitigate by making the form as short as possible and framing it as "protecting your commission from ops errors."

---

**REC-2: Replace kickoff scheduling email loop with a scheduling link**
**Type:** Eliminate
**Priority:** P1 Quick Win — Impact: High × Feasibility: High
**Targets:** Step 5
**Current state:** Ops emails client, waits for reply, negotiates time — averaging 1–4 days
**Proposed change:** Embed a Calendly (or equivalent) link in the welcome email. Client self-schedules. Kickoff appears on calendar automatically.
**Expected outcome:** Reduces kickoff scheduling from 1–4 days to same-day or next-day. Directly resolves the primary client complaint.
**Estimated effort:** 1 day setup
**ROI horizon:** Immediate — eliminates the single biggest source of delay
🟢 Low risk — well-understood tool, client-friendly, no internal dependencies

---

**REC-3: Automate account creation and welcome email**
**Type:** Automate
**Priority:** P1 Strategic — Impact: High × Feasibility: Medium
**Targets:** Steps 3 + 4
**Current state:** Ops manually enters data into platform and writes/sends welcome email
**Proposed change:** Connect CRM (Salesforce) to platform via Zapier, Make, or native API. Account creation triggers automatically on deal-close form submission. Welcome email (with scheduling link from REC-2 embedded) sends automatically from the same trigger.
**Expected outcome:** Eliminates ~30 min of ops manual work per client; removes human error from account creation; welcome email sent within minutes of deal close (not hours or days)
**Estimated effort:** 1–2 weeks depending on platform API availability [ASSUMPTION: API access exists]
**ROI [ESTIMATED]:** At 20 clients/month, saves ~10 hrs/month ops time. At ₹600/hr, that's ₹72,000/year recovered. A Zapier plan at ~₹8,000/month costs ₹96,000/year — net ROI positive within ~16 months. At 40 clients/month (your scale target), payback is under 8 months.
🔴 TECHNICAL risk: Depends on platform API quality. Validate before building. Start with manual trigger (button click) before going fully automatic.

---

**REC-4: Define and document CSM assignment criteria**
**Type:** Standardize
**Priority:** P2 — Impact: Medium × Feasibility: High
**Targets:** Step 6
**Current state:** Assignment is informal — "whoever has capacity" [OBSERVED], with unclear rules
**Proposed change:** Document a simple assignment matrix: capacity threshold, territory/vertical match, relationship history. Assignment still human-made, but now against written criteria with a visible capacity dashboard.
**Expected outcome:** Faster assignment, better client-CSM fit, audit trail if assignment is questioned
**Estimated effort:** 1 week (criteria definition + lightweight tracking)
**Note:** Keep this step human. Automated assignment is possible but introduces edge cases (client preference, relationship context) that aren't worth the complexity at this volume.
🟠 CULTURAL risk: CSMs may feel their autonomy is being reduced. Frame as "fewer bad surprises" not "more monitoring."

---

**REC-5: Create a pre-kickoff briefing template auto-populated from CRM**
**Type:** Simplify
**Priority:** P2 — Impact: Medium × Feasibility: Medium
**Targets:** Step 7
**Current state:** CSM reviews Salesforce manually; frequently has to ask ops clarifying questions
**Proposed change:** Build a one-page kickoff brief template that pulls key fields from Salesforce automatically (or is completed by sales at deal close as part of REC-1). CSM receives it alongside their assignment notification.
**Expected outcome:** Eliminates clarification loop; CSMs go into kickoffs prepared; client experience improves
**Estimated effort:** 1 week
🟡 DEPENDENCY risk: Requires Salesforce data to actually be complete (resolved upstream by REC-1)

---

### IMPLEMENTATION ROADMAP

**Phase 1 — Quick Wins (Week 1–2)**
- REC-2: Set up scheduling link — 1 day, zero cost
- REC-1: Build deal-close form — 2–3 days, zero/low cost
- REC-4: Draft CSM assignment criteria — parallel to above

**Phase 2 — Structural (Week 2–6)**
- REC-5: Build kickoff briefing template
- REC-3: Begin CRM→platform automation (validate API first)

**Phase 3 — Scale-ready (Week 6+)**
- REC-3 full automation live
- Review all metrics; set baseline for 40 clients/month readiness

---

### HUMAN COLLABORATION NOTES

**Step 6 — KEEP HUMAN: CSM assignment**
Reasoning: Requires relationship context, capacity judgment, and named accountability. Automate the visibility (capacity dashboard), not the decision.

**Step 7 — KEEP HUMAN: CSM kickoff preparation and the kickoff itself**
Reasoning: Client relationship, tone calibration, discovery — irreducibly human. Automate the brief, not the conversation.

---

### OPEN QUESTIONS

1. Does your platform have an API or native Zapier/Make integration? (Required for REC-3)
2. What tool are you using for internal ops tracking — is there a system of record beyond Salesforce and email?
3. How is CSM capacity currently tracked? A spreadsheet? A field in Salesforce?
4. Is the welcome email currently templated, or written fresh each time?

---

### ASSUMPTIONS LOG

1. [ASSUMPTION] — Salesforce is the system of record for client data
2. [ASSUMPTION] — CSM assignment is capacity-based with no documented criteria
3. [ASSUMPTION] — Welcome email is template-based (no customization required)
4. [ASSUMPTION] — Platform has API access for automation (REC-3 depends on this)
5. [ASSUMPTION] — Blended ops hourly rate ₹600/hr used for ROI estimates

---

*Generated using ops-workflow-analysis-assistant v1.0.0 on Claude Sonnet 4.6*
