# Customer Support Triage Assistant — Claude Skill

A production-ready Claude Skill that helps support teams process incoming customer queries faster,
more consistently, and with better prioritization. Works as an experienced support operations
specialist embedded directly into your workflow.

---

## What This Skill Does

- Categorizes support requests across 6 domains and 30+ subcategories
- Detects urgency levels (CRITICAL / HIGH / MEDIUM / LOW)
- Identifies emotionally escalated customers
- Extracts key information from any message format
- Generates concise triage summaries
- Recommends next actions
- Drafts professional first responses, channel-tuned
- Detects duplicate or repeated issues
- Flags high-risk and sensitive situations (legal, GDPR, media, fraud)
- Supports human agents without replacing their judgment

---

## Supported Channels

| Channel | Notes |
|---------|-------|
| Email | Full formal responses |
| Chat | Conversational, direct |
| WhatsApp | Friendly, brief |
| Helpdesk tickets | Structured, medium-length |
| Call summaries | Summary-only mode |
| Social media | Brief public reply + move to DM |

---

## Project Structure

```
customer-support-triage/
│
├── README.md                        ← You are here
├── skill/
│   ├── SKILL.md                     ← Core skill instructions (Claude reads this)
│   └── references/
│       ├── examples.md              ← 6 fully worked channel examples
│       └── production-guide.md     ← Integration, metrics, deployment
│
├── prompts/
│   ├── system-prompt.md            ← Ready-to-use system prompt for API deployment
│   └── input-templates.md          ← Copy-paste input formats per channel
│
├── templates/
│   ├── triage-report-template.md   ← Blank triage output template
│   └── response-templates.md       ← All 7 draft response templates
│
├── config/
│   ├── category-taxonomy.json      ← Full category tree in JSON
│   ├── risk-flags.json             ← Risk flag definitions and triggers
│   └── urgency-rules.json         ← Urgency detection rules and phrase triggers
│
├── tests/
│   ├── test-cases.json             ← 8 test inputs with expected outputs
│   └── eval-checklist.md          ← Manual QA checklist for human reviewers
│
└── docs/
    ├── integration-guide.md        ← How to wire this into your helpdesk
    ├── customization-guide.md      ← How to adapt for your business
    └── changelog.md               ← Version history
```

---

## Quick Start

1. **As a Claude Skill**: Install `skill/SKILL.md` into your Claude skill library.
2. **As an API system prompt**: Use `prompts/system-prompt.md` as your `system` parameter.
3. **For structured input**: Use the templates in `prompts/input-templates.md`.
4. **For customization**: Edit `config/category-taxonomy.json` and `config/urgency-rules.json`.

---

## Version

**v1.0.0** — Initial production release  
See `docs/changelog.md` for version history.
