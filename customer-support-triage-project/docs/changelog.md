# Changelog

All notable changes to the Customer Support Triage Skill will be documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [1.0.0] — 2026-06-06

### Added
- Initial production release
- Full SKILL.md with system prompt, operating principles, output schema
- Category taxonomy: 6 primary domains, 30+ subcategories
- Urgency detection: 4 levels with trigger phrase overrides
- Emotional state detection: 4 levels with sentiment scoring
- Risk flag registry: 10 flags with triggers and actions
- Combination rules for multi-flag scenarios
- Draft response templates: 7 templates across channel types
- Channel tone guidelines: email, chat, WhatsApp, ticket, call summary, social
- Confidence handling: 4 levels (HIGH → INSUFFICIENT)
- Escalation logic: immediate, post-response, and no-escalation paths
- Failure handling: 5 edge case types
- Human-in-the-loop checkpoints
- Production usage guide (references/production-guide.md)
- 6 fully worked examples (references/examples.md)
- System prompt for API deployment (prompts/system-prompt.md)
- Input templates for all 6 channels + batch mode (prompts/input-templates.md)
- Blank triage report template (templates/triage-report-template.md)
- All response templates separated (templates/response-templates.md)
- Category taxonomy in JSON (config/category-taxonomy.json)
- Risk flags in JSON (config/risk-flags.json)
- Urgency rules in JSON (config/urgency-rules.json)
- 8 test cases with expected outputs (tests/test-cases.json)
- Manual QA eval checklist (tests/eval-checklist.md)
- Integration guide for API, Zendesk, Freshdesk, Intercom, HubSpot (docs/integration-guide.md)
- Customization guide for taxonomy, thresholds, templates, multi-brand (docs/customization-guide.md)

---

## [Unreleased]

### Planned
- Structured JSON output mode (optional — for direct helpdesk field mapping)
- Spanish-language system prompt variant
- Additional test cases: non-English input, batch processing, call summary edge cases
- Metric dashboard template for tracking triage quality KPIs
- Webhook handler starter code (Node.js and Python)
