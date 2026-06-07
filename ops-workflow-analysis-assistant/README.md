# Operations Workflow Analysis Assistant

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Claude Skill](https://img.shields.io/badge/type-Claude%20Skill-blueviolet)
![Maintained](https://img.shields.io/badge/maintained-yes-brightgreen)

A reusable Claude Skill that functions as a practical internal operations consultant — focused on process optimization, bottleneck analysis, and actionable efficiency improvements.

> Point it at any workflow, described in plain language or bullet points, and it will decompose it, score its inefficiencies, and tell you exactly what to fix first and why.

---

## Demo

**You describe your workflow:**
> *"When sales closes a deal, they send an email to ops, who manually creates the account, sends a welcome email, and schedules the kickoff over email back-and-forth. It usually takes 2–3 days before the client hears from us."*

**The skill produces:**
- A structured step-by-step decomposition with tagged inefficiencies
- Bottleneck Severity Scores for each problem area
- Automation Suitability scores for manual tasks
- Prioritized recommendations (P1/P2/P3) with effort and ROI estimates
- A phased implementation roadmap
- An explicit list of which steps to keep human — and why

→ See the [full worked example](examples/saas-client-onboarding-output.md)

---

## What It Does

| Capability | What you get |
|---|---|
| Workflow decomposition | Every step tagged with type, input, output, tool, handoff, and duration |
| Bottleneck detection | Scored by severity (BSS 1–10) with root cause |
| Manual task audit | Automation Suitability Index (ASI) for every human-operated step |
| Communication analysis | Async/sync mismatches, accountability gaps, information loss |
| Dependency mapping | Critical path, parallel opportunities, circular dependencies |
| Prioritized recommendations | Impact-Feasibility matrix → P1/P2/P3 with effort estimates |
| ROI estimation | Time saved, cost recovered, payback period — with explicit assumptions |
| Risk flags | Adoption, technical, data, cultural, and regression risks per recommendation |
| Human collaboration notes | Which steps to keep human and the exact reasoning |
| Full audit report | Stakeholder-ready structured report on demand |

---

## Installation

### Claude.ai (Web/Mobile/Desktop)

1. Download this repository (Code → Download ZIP, or `git clone`)
2. Go to **Settings → Skills** in your Claude account
3. Click **Install Skill** and upload the folder or `.skill` file
4. The skill is now active — no manual invocation needed

### Claude Code / API

Place the `ops-workflow-analysis-assistant/` directory in your configured skills folder. The skill auto-triggers based on its description.

---

## How to Use

You do not need to invoke the skill manually. Just describe your workflow naturally:

```
"Here's how our team handles client onboarding — it's taking forever..."
"Can you audit our weekly reporting process?"
"Where are we losing the most time in this workflow?"
"What should we automate here?"
"Help me write a process improvement proposal for this."
```

Claude will trigger the skill automatically and begin analysis.

### Workflow description formats — all work

**Prose:**
> "When a request comes in, whoever sees it first picks it up, creates a ticket sometimes, and assigns it to whoever looks available..."

**Bullet list:**
> - Request submitted via email
> - Coordinator reviews (sometimes same day, sometimes not)
> - Assigned to specialist
> - Work completed
> - Client notified manually

**Table or numbered steps — any format you have.**

The skill restates the workflow in structured form and asks you to confirm before building recommendations on top of it.

### Requesting specific outputs

| What you ask | What you get |
|---|---|
| *"Give me the full audit report"* | Complete Operational Audit Report (10 sections) |
| *"Score each step for automation"* | ASI scoring for all manual tasks |
| *"What's the ROI of fixing the handoff?"* | ROI estimate with stated assumptions |
| *"Which recommendation do we do first?"* | Impact-Feasibility priority ranking |
| *"What are the risks of automating step 3?"* | Risk flags with mitigation guidance |

---

## File Structure

```
ops-workflow-analysis-assistant/
│
├── README.md                        ← You are here
├── SKILL.md                         ← Core skill: persona, triggers, principles
├── LICENSE                          ← MIT
├── CHANGELOG.md                     ← Version history and roadmap
├── CONTRIBUTING.md                  ← How to contribute
│
├── references/
│   ├── methodology.md               ← Analysis engine
│   │                                   Workflow decomposition · Bottleneck detection
│   │                                   Manual task identification · Communication analysis
│   │                                   Dependency mapping · Example analyses
│   │
│   └── formats.md                   ← Output layer
│                                       Audit report template · BSS & ASI scoring
│                                       Priority matrix · ROI estimation
│                                       Risk flags · Human collaboration notes
│                                       Implementation best practices
│
├── examples/
│   ├── README.md                    ← How to read and contribute examples
│   ├── saas-client-onboarding-input.md
│   └── saas-client-onboarding-output.md
│
└── .github/
    └── ISSUE_TEMPLATE/
        ├── bug_report.md
        └── feature_request.md
```

---

## Key Concepts

### Step Tags

| Tag | Meaning |
|---|---|
| `[MANUAL]` | Requires human action, no tooling support |
| `[AUTOMATED]` | Runs without human involvement |
| `[TOOL-ASSISTED]` | Uses software but requires human input |
| `[DECISION]` | Requires judgment, approval, or branching |
| `[WAIT]` | Waiting for an external trigger |
| `[HANDOFF]` | Output passes to a different person or team |
| `[BOTTLENECK]` | Slows overall flow disproportionately |
| `[OBSERVED]` | Stated directly by the user |
| `[ASSUMPTION]` | Inferred — not confirmed |
| `[PARALLELIZABLE]` | Could run simultaneously with another step |
| `[RESOURCE-CONFLICT]` | Steps share a constrained resource |

### Scoring Systems

**Bottleneck Severity Score (BSS)** — Rates each bottleneck 1–10 across frequency, downstream cascade, recovery cost, and workaround availability. Scores ≥ 8 are critical.

**Automation Suitability Index (ASI)** — Rates each manual task 1–5 across input predictability, rule clarity, error consequence, frequency, human value-add, and integration feasibility. Tasks scoring ≥ 4.5 are strong automation candidates. High error-consequence tasks are never recommended for full automation regardless of score.

**Impact-Feasibility Priority Matrix** — Each recommendation is P1 Quick Win (high impact, high feasibility), P1 Strategic (high impact, harder to execute), P2 (plan and batch), or P3 (deprioritize).

---

## Design Principles

**Practical over perfect.** A 70% improvement that ships beats a 100% solution that stalls in planning.

**No automation inflation.** Automation is only recommended when a task is high-frequency, low-judgment, and the cost is recoverable. The skill will explicitly tell you when to optimize a human process instead of replacing it.

**Assumptions are always visible.** Every inferred claim is tagged `[ASSUMPTION]`. You always know what the analysis is built on.

**Humans stay where they matter.** The skill explicitly identifies which steps require human judgment, accountability, or relationship context — and recommends keeping them human.

**Specificity is non-negotiable.** Vague outputs like "improve communication" are not produced. Every recommendation names the step, the change, the expected outcome, and the risk.

---

## Limitations

- The skill works from what you describe — it cannot access your actual tools, dashboards, or systems
- ROI estimates are directional and flag assumptions explicitly; validate against your actual cost structure before using in proposals
- Risk assessments are based on common operational patterns — you know your organization's specific dynamics better than the skill does
- For very large multi-team workflows, break the analysis into segments for sharper output

---

## Contributing

Contributions are welcome — especially worked examples, scoring refinements, and edge case handling. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

To suggest a feature or report unexpected behavior, [open an issue](../../issues).

For questions or ideas you're not sure about, [start a discussion](../../discussions).

---

## License

MIT — see [LICENSE](LICENSE). Free to use, adapt, and redistribute.

---

*If this skill saved you time or helped you fix a real process — consider leaving a ⭐ on the repo. It helps others find it.*
