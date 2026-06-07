# Workflow Analysis Methodology

## Table of Contents
1. Workflow Decomposition
2. Bottleneck Detection
3. Repetition & Manual Task Identification
4. Communication Flow Analysis
5. Dependency Chain Mapping
6. Example Analyses

---

## 1. Workflow Decomposition

Break any described workflow into atomic steps using this structure:

```
Step N: [Action verb] + [what] + [by whom / which system]
  Input:    [what triggers or feeds this step]
  Output:   [what it produces]
  Tool:     [software, form, meeting, Slack, email, spreadsheet, etc.]
  Duration: [stated or estimated]
  Frequency:[per day / week / month / event]
  Handoff:  [who receives the output next]
```

Flag each step with one or more of these tags:
- `[MANUAL]` — requires human action with no tooling support
- `[DECISION]` — requires judgment, approval, or branching
- `[WAIT]` — step involves waiting for an external trigger
- `[HANDOFF]` — output passes to a different person or team
- `[TOOL-ASSISTED]` — uses software but still requires human input
- `[AUTOMATED]` — runs without human involvement

---

## 2. Bottleneck Detection

A bottleneck is any step that slows the overall flow disproportionately to its actual work content.

**Detection signals — look for:**

| Signal | What it looks like |
|---|---|
| Queue accumulation | Work piles up waiting for this step |
| Single point of dependency | Only one person / system can execute |
| Approval gates | Sign-off required before flow can continue |
| Inconsistent execution time | Same step takes 10 min sometimes, 3 days other times |
| Rework loops | Output frequently returned for correction |
| High context-switching | Assignee juggles this with other responsibilities |
| Tooling gaps | Step done in email/spreadsheet instead of a proper system |

**Severity classification (for BSS scoring — see formats.md):**
- **Critical**: Blocks downstream work entirely until resolved
- **High**: Delays downstream by >50% of normal cycle time
- **Medium**: Adds friction but work-arounds exist
- **Low**: Minor inefficiency, manageable

**Questions to ask when bottleneck is suspected:**
- "How often does this step cause delays?"
- "Is there a backup if the usual person is unavailable?"
- "What happens if this step is skipped or delayed?"

---

## 3. Repetition & Manual Task Identification

**High-value repetitive manual tasks** are the primary candidates for optimization (not necessarily automation).

Identify tasks that are:
- Executed >3x per week with the same or near-identical inputs
- Copy-paste operations between systems
- Status updates that aggregate data already available elsewhere
- Report generation from structured data
- Form completion with predictable fields
- Manual routing / forwarding of information

**Judgment checklist for each repetitive task:**

```
□ Is the input always structured and predictable?
□ Are the rules for processing it written down or consistent?
□ Does it require relationship context or negotiation? (→ keep human)
□ Does it require real-time judgment? (→ keep human)
□ Does it require accountability that must be named? (→ keep human)
□ Could the output be wrong in a consequential way? (→ human-in-loop)
```

If the first two boxes are checked and none of the others apply: strong automation candidate.
If any of the last four apply: optimize the human experience, don't remove the human.

---

## 4. Communication Flow Analysis

Inefficient communication is one of the highest-leverage areas for operational improvement — and the most frequently ignored.

**Inefficiency signals:**

| Pattern | Problem |
|---|---|
| Information requested multiple times | No single source of truth |
| Updates sent via DM/email instead of shared tool | No audit trail, no visibility |
| Meetings used to share status | Synchronous used where async would work |
| Decisions made verbally with no record | Creates rework when context is lost |
| CC lists growing over time | Unclear ownership, covering-bases culture |
| "Looping in X for visibility" | Symptom of unclear RACI |
| Replies to replies to replies (email chains) | Fragmented discussion, no resolution |

**Recommendations framework:**
- Async-first for: status updates, informational sharing, non-urgent approvals
- Sync for: ambiguous decisions, conflict resolution, relationship-building, brainstorming
- Documented for: any decision with downstream consequence
- Automated alerts for: threshold events (e.g. SLA breach, budget crossing)

---

## 5. Dependency Chain Mapping

Map dependencies explicitly using this format:

```
Step A → must complete before → Step B
Step B + Step C → both required before → Step D
Step D → triggers (automatically / manually) → Step E
```

Then identify:

**Sequential chains**: Steps that can only run one after another — longest path = critical path. Reducing time here has direct impact on total cycle time.

**Parallel opportunities**: Steps currently run sequentially that could run simultaneously. Flag with `[PARALLELIZABLE]`.

**Hidden dependencies**: Steps that look independent but share a resource (a person, a system, a budget line). Flag with `[RESOURCE-CONFLICT]`.

**Circular dependencies**: A → B → C → A. These are organizational red flags. Surface them explicitly and recommend breaking the loop.

---

## 6. Example Workflow Analyses

### Example A: Client Onboarding (B2B SaaS)

**As described:** Sales closes deal → sends email to ops → ops creates account manually → sends welcome email → schedules kickoff via back-and-forth → kickoff happens → CSM assigned manually → CSM reviews account details from Salesforce.

**Decomposed:**
```
Step 1: [HANDOFF][MANUAL] Sales emails ops with deal details
  Duration: ~5 min (sales) + 0–48hr wait (ops pick-up)
  Problem: Unstructured email → ops must interpret and re-enter data [BOTTLENECK]

Step 2: [MANUAL][TOOL-ASSISTED] Ops creates account in platform
  Duration: ~20 min
  Problem: Data already exists in CRM — re-entry is pure duplication [REPETITIVE]

Step 3: [MANUAL] Ops sends welcome email
  Duration: ~10 min
  Problem: Template-based, no customization needed [AUTOMATION CANDIDATE]

Step 4: [MANUAL][WAIT] Kickoff scheduling via email back-and-forth
  Duration: 1–4 days elapsed
  Problem: Classic scheduling loop — no calendaring tool in use [BOTTLENECK]

Step 5: [MANUAL] CSM assigned by ops
  Duration: unknown
  Problem: Assignment logic unclear — capacity? territory? relationship? [DECISION - keep human but document criteria]

Step 6: [MANUAL][TOOL-ASSISTED] CSM reviews Salesforce
  Duration: ~30 min
  Problem: If Salesforce is current, this is fine. If not, creates rework. [DATA QUALITY RISK]
```

**Key findings:**
- Critical bottleneck: Step 1 (unstructured handoff) and Step 4 (scheduling loop)
- Automation candidates: Steps 2 (CRM→platform sync), 3 (templated email)
- Preserve human: Step 5 (CSM assignment — judgment required)
- Total estimated cycle reduction if Steps 1+2+3+4 optimized: 2–4 days → same day

---

### Example B: Weekly Reporting (Internal Ops)

**As described:** 4 team leads submit numbers via email every Friday → ops coordinator consolidates into spreadsheet → manager reviews → sends summary to director → director sometimes asks for clarifications → second version sent.

**Key findings:**
- Steps 1+2: Classic aggregation loop — replace with shared live dashboard or auto-collected form
- Clarification loop (Step 4→5): Symptom of unclear KPI definitions — fix the metrics, not the report
- Total time estimate: ~3.5 hrs/week across team → reducible to <30 min with form + auto-summary
- Human preserved: Manager interpretation and director narrative — judgment layer stays

---

### Example C: Bug Triage (Engineering Team)

**As described:** User reports bug via email OR Slack OR in-app → whoever sees it first creates a Jira ticket (sometimes) → assigned to any available dev → dev investigates → sometimes escalated → fix deployed → user not always notified.

**Key findings:**
- Multi-channel intake with no routing logic = `[BOTTLENECK]` + `[DATA QUALITY RISK]`
- "Whoever sees it first" = `[SINGLE POINT OF DEPENDENCY]` with no accountability
- "Sometimes" ticket creation = no audit trail, duplicates likely
- User notification gap = trust erosion, repeat contacts
- Priority fix: Single intake channel with auto-routing rules before any automation
