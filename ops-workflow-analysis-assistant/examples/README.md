# Examples

This folder contains worked analyses — real-world-inspired workflow descriptions paired with the full output the skill produces.

They serve two purposes:
1. **For users**: See what the skill actually produces before you install it
2. **For contributors**: Understand the expected input/output format when adding new examples

---

## File naming convention

```
[domain]-[workflow-type]-input.md     ← The workflow description given to Claude
[domain]-[workflow-type]-output.md    ← The full skill output
```

Example:
```
saas-client-onboarding-input.md
saas-client-onboarding-output.md
```

---

## Current examples

| Domain | Workflow | Files |
|---|---|---|
| B2B SaaS | Client onboarding | `saas-client-onboarding-input.md` / `saas-client-onboarding-output.md` |
| Internal ops | Weekly reporting | `internal-weekly-reporting-input.md` / `internal-weekly-reporting-output.md` |

---

## Adding a new example

1. Create the input file — write it as if you're a user describing your workflow to Claude in plain language. Don't make it artificially clean or structured. Real descriptions are messy.
2. Run the skill on that input (install it and describe the workflow to Claude)
3. Paste the full output into the output file — don't edit or clean it up
4. Add a row to the table above
5. Submit a PR referencing your issue

---

## Format for input files

```markdown
# [Workflow Name] — Input

**Context provided to Claude:**

[Paste the exact description you gave, as-is]
```

## Format for output files

```markdown
# [Workflow Name] — Skill Output

**Claude's response:**

[Paste the full output, unedited]

---
*Generated using ops-workflow-analysis-assistant v[X.X.X] on Claude [model name]*
```
