# Contributing to Operations Workflow Analysis Assistant

First off — thank you. This skill gets better when people who use it in real operational contexts bring back what they've learned.

---

## What We're Looking For

### High-value contributions
- **New worked examples** in `examples/` — real workflow types the current examples don't cover (HR, finance, logistics, content, support, etc.)
- **Scoring refinements** — if the BSS or ASI weights feel wrong for a specific domain, open an issue with your reasoning
- **Edge case handling** — workflows that broke the methodology or produced unhelpful output
- **Prompt improvements** — if a section of `SKILL.md` or the reference files is producing vague or incorrect behavior, show us what happened and what you expected
- **Translations** — the ROI rate proxies currently cover India and US/global; other regional defaults are welcome

### Lower priority (but not closed)
- Aesthetic/wording changes without behavioral rationale
- Adding complexity to the scoring systems without evidence it improves output
- Restructuring the file layout without a clear gain

---

## How to Contribute

### 1. Open an issue first (for anything non-trivial)

Before writing a PR, open an issue describing:
- What you're changing and why
- What behavior the current version produces
- What behavior you expect after your change

This prevents effort going into PRs that won't be merged.

### 2. Fork and branch

```bash
git fork https://github.com/[your-username]/ops-workflow-analysis-assistant
git checkout -b feature/your-change-name
```

Use descriptive branch names:
- `feature/add-hr-onboarding-example`
- `fix/asi-scoring-edge-case`
- `docs/expand-bottleneck-signals`

### 3. Make your changes

Follow the conventions already in place:

**In `SKILL.md`:**
- Keep it under 500 lines
- Every behavioral rule should be specific enough to be testable
- Tag assumptions with `[ASSUMPTION]`, observations with `[OBSERVED]`

**In `references/methodology.md` or `references/formats.md`:**
- Use the existing table and code block formats for consistency
- Add to the Examples section rather than replacing existing ones
- If adding a new scoring dimension, include interpretation guidance

**In `examples/`:**
- Use the established example format (see `examples/README.md`)
- Include both the input (workflow description) and the full output
- Real-world inspired examples are far more useful than toy cases

### 4. Update `CHANGELOG.md`

Add your change under an `[Unreleased]` section at the top:

```markdown
## [Unreleased]
### Added
- Example: HR employee onboarding workflow analysis
```

### 5. Submit your PR

In your PR description:
- Link the issue it resolves
- Describe what changed and why
- Note if the change affects output format (breaking change = major version bump)

---

## Code of Conduct

This is a professional tooling repo. Contributions should be:
- Specific and evidence-based (not vibes-driven)
- Respectful of existing design decisions even when proposing changes
- Clear about tradeoffs — if your change improves X at the cost of Y, say so

---

## Questions?

Open a [Discussion](../../discussions) rather than an issue for questions, ideas you're not sure about, or feedback that isn't a bug or feature request.
