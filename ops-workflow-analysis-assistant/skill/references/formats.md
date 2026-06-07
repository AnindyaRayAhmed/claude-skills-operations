# Output Formats, Scoring, ROI & Risk Logic

## Table of Contents
1. Operational Audit Report Format
2. Bottleneck Severity Score (BSS)
3. Automation Suitability Index (ASI)
4. Impact-Feasibility Priority Matrix
5. ROI Estimation Behavior
6. Risk Assessment Logic
7. Human Collaboration Recommendations
8. Best Practices for Implementation

---

## 1. Operational Audit Report Format

Use this structure for any full workflow audit. Adapt length to complexity — don't pad, don't compress critical findings.

```
═══════════════════════════════════════════════════════
OPERATIONAL WORKFLOW AUDIT
Workflow: [Name]
Scope: [What was analyzed]
Date: [Date of analysis]
Prepared by: Operations Workflow Analysis Assistant
Assumptions flagged: [count]
═══════════════════════════════════════════════════════

## EXECUTIVE SUMMARY
[3–5 sentence summary: what the workflow does, its primary inefficiency pattern,
and the single highest-leverage recommendation. Written for a non-technical reader.]

Overall Efficiency Rating: [X/10]
Primary Inefficiency Type: [Bottleneck / Repetition / Communication / Dependency / Mixed]
Estimated Weekly Time Lost: [X hours/week — state if estimated]
Priority Improvement: [One-line statement of the top recommendation]

---

## WORKFLOW MAP
[Structured decomposition of each step — using the format from methodology.md]

---

## DIAGNOSTIC FINDINGS

### Bottlenecks Identified
[List each bottleneck with BSS score, location in workflow, and root cause]

### Repetitive Manual Tasks
[List each task, frequency, and current time cost]

### Communication Inefficiencies
[List each pattern, where it occurs, and downstream impact]

### Dependency Issues
[Map critical path, parallel opportunities, and any circular dependencies]

### Data Quality Risks
[Any step where data integrity is uncertain or unverified]

---

## RECOMMENDATIONS

[For each recommendation, use this format:]

### REC-[N]: [Short title]
**Type**: [Eliminate / Simplify / Automate / Restructure / Standardize]
**Priority**: [P1 / P2 / P3] — [Impact: High/Med/Low] × [Feasibility: High/Med/Low]
**Targets**: [Which workflow step(s)]
**Current state**: [What's happening now]
**Proposed change**: [Specific, actionable description of the change]
**Expected outcome**: [Measurable result — time saved, errors reduced, etc.]
**Estimated effort**: [Days / Weeks — implementation complexity]
**ROI horizon**: [When the investment pays back]
**Risks**: [What could go wrong]
**Assumptions**: [What must be true for this to work — tag [ASSUMPTION]]

---

## IMPLEMENTATION ROADMAP

### Phase 1 — Quick Wins (0–2 weeks)
[P1 items that are high-impact and low-effort]

### Phase 2 — Structural Changes (2–8 weeks)
[P2 items requiring coordination, tooling, or process redesign]

### Phase 3 — Long-Term Investments (8+ weeks)
[P3 items: automation builds, integrations, cultural shifts]

---

## HUMAN COLLABORATION NOTES
[Explicit list of steps/decisions that should remain human-owned and why]

---

## OPEN QUESTIONS
[What the analyst still needs to complete a full assessment]

---

## ASSUMPTIONS LOG
[Full list of every [ASSUMPTION] tagged in the report]
```

---

## 2. Bottleneck Severity Score (BSS)

Score each identified bottleneck from 1–10.

| Dimension | Weight | Score (1–5) |
|---|---|---|
| Frequency of impact | 30% | How often does this bottleneck activate? |
| Downstream cascade | 30% | How many downstream steps are blocked when it fires? |
| Recovery cost | 20% | How expensive (time/effort) is recovery when it delays? |
| Workaround availability | 20% | Are effective workarounds available? (5 = none exist) |

**BSS = (Freq × 0.3) + (Cascade × 0.3) + (Recovery × 0.2) + (Workaround × 0.2) × 2**

**Interpretation:**
- BSS 8–10: Critical — address immediately
- BSS 5–7: High — include in Phase 1 or 2
- BSS 3–4: Medium — monitor or bundle with other changes
- BSS 1–2: Low — log for future consideration

---

## 3. Automation Suitability Index (ASI)

Score each manual task for automation candidacy. Score each dimension 1–5.

| Dimension | Score 1 | Score 5 |
|---|---|---|
| Input predictability | Highly variable, unstructured | Always structured, predictable |
| Rule clarity | Judgment required | Rules fully documentable |
| Error consequence | Errors are high-stakes | Errors are low-stakes / easily caught |
| Frequency | Rare (<1/month) | Very frequent (>daily) |
| Human value-add | Human adds significant value | Human adds no unique value |
| Integration feasibility | Requires custom build | APIs/tools already available |

**ASI = Average of all 6 dimensions**

**Interpretation:**
- ASI 4.5–5.0: Strong automation candidate — prioritize
- ASI 3.5–4.4: Good candidate — validate edge cases first
- ASI 2.5–3.4: Partial automation possible — automate routine, keep human for exceptions
- ASI 1.0–2.4: Do not automate — optimize the human experience instead

**Hard rule**: Never recommend full automation if Error Consequence score ≥ 4, regardless of overall ASI.

---

## 4. Impact-Feasibility Priority Matrix

Plot each recommendation on this grid to assign priority:

```
        HIGH IMPACT
             │
    P1       │       P1
(Quick Win)  │  (Strategic)
             │
─────────────┼─────────────
             │
    P3       │       P2
 (Low ROI)   │  (Plan for)
             │
        LOW IMPACT

        LOW ◄──────────► HIGH
              FEASIBILITY
```

**Priority definitions:**
- **P1 Quick Win**: High impact + High feasibility → do first, weeks 0–2
- **P1 Strategic**: High impact + Low feasibility → plan carefully, allocate resources
- **P2**: Low-medium impact + High feasibility → batch and execute
- **P3**: Low impact + Low feasibility → deprioritize or drop

---

## 5. ROI Estimation Behavior

**When to estimate ROI:**
Always attempt an ROI estimate for recommendations involving tooling cost, engineering time, or significant process change. Flag all numbers as estimates with `[ESTIMATED]`.

**ROI Estimation formula:**

```
Weekly Time Saved = (steps eliminated or reduced) × (avg step duration) × (frequency/week)
Annual Value = Weekly Time Saved × 52 × (hourly rate or cost proxy)
Implementation Cost = (build/setup time) + (training time) + (tool licensing)
Payback Period = Implementation Cost ÷ (Annual Value ÷ 52)
```

**When no cost data is provided:**
- Use conservative time estimates and flag them
- Use a blended hourly rate proxy of ₹500–800/hr for Indian SMB contexts or $50–80/hr for US/global contexts unless told otherwise
- Always present a range, not a single number

**Example:**
> "Automating the weekly report consolidation [ESTIMATED] saves ~3 hrs/week across 4 team leads. At ₹600/hr blended rate, that's ~₹3,74,400/year in recovered capacity. A no-code dashboard tool at ₹5,000/month costs ₹60,000/year. Net annual benefit: ~₹3,14,400. Payback: under 2 months."

**What ROI estimates do NOT cover (say this explicitly):**
- Change management effort
- Hidden integration complexity
- Adoption failure risk
- Opportunity cost of engineering time

---

## 6. Risk Assessment Logic

Attach a risk flag to every P1 and P2 recommendation.

**Risk categories:**

| Category | Flag | Description |
|---|---|---|
| Adoption risk | 🟡 ADOPTION | Team may resist or fail to sustain the change |
| Technical risk | 🔴 TECHNICAL | Integration complexity, API instability, or build risk |
| Data risk | 🔴 DATA | Change affects data integrity, compliance, or audit trail |
| Dependency risk | 🟡 DEPENDENCY | Change requires coordination with external team or vendor |
| Regression risk | 🟡 REGRESSION | Change may degrade an adjacent process |
| Cultural risk | 🟠 CULTURAL | Change touches team norms, roles, or perceived status |

**Risk mitigation template:**
```
Risk: [Flag] [Description]
Likelihood: [High / Medium / Low]
Mitigation: [Specific action to reduce this risk]
Owner: [Who should manage this risk]
```

---

## 7. Human Collaboration Recommendations

For every workflow analyzed, explicitly identify which steps should remain human-owned. Use this format:

```
Step [N] — KEEP HUMAN: [Brief reason]
Reasoning: [One of the following applies:]
  - Requires relationship context (negotiation, trust, nuance)
  - Requires real-time situational judgment
  - Requires named accountability (audit, legal, compliance)
  - Requires empathy or communication tone calibration
  - Error consequence is too high to automate without fallback
```

**Principle**: The goal is not to minimize human involvement. It is to ensure humans are applied to the steps that genuinely benefit from human judgment — and freed from the ones that don't.

---

## 8. Best Practices for Operational Implementation

Include a "Readiness Check" in any Phase 1 recommendation:

```
BEFORE IMPLEMENTING [REC-N]:
□ Is the current process documented as-is?
□ Do all affected team members understand the proposed change?
□ Is there a rollback plan if the change causes regression?
□ Is there a success metric defined (how will you know it worked)?
□ Is there an owner named for sustaining the change post-launch?
□ Has this been piloted on a small scale before full rollout?
```

**Change sequencing rules:**
1. Never automate a broken process — fix it first, then automate
2. Never change two interdependent steps simultaneously without a controlled test
3. Document the new process before training anyone on it
4. Measure before and after — set the baseline now
5. Plan for the first 30 days of adoption, not just the launch

**Operational metrics to track post-implementation:**
- Cycle time (end-to-end duration for one unit of work)
- Rework rate (% of outputs requiring correction)
- Handoff time (time between step completion and next step start)
- Tool adoption rate (are people actually using the new system?)
- Exception rate (how often does the new process hit an unhandled case?)
