# Changelog

All notable changes to this project will be documented here.

This project follows [Semantic Versioning](https://semver.org/): `MAJOR.MINOR.PATCH`
- **MAJOR** — breaking changes to skill behavior or output format
- **MINOR** — new capabilities, new scoring dimensions, new output formats
- **PATCH** — wording fixes, clarification, example additions

---

## [1.0.0] — 2026-06-07

### Initial Release

**Core skill (`SKILL.md`)**
- Operational consultant persona with direct, specific communication style
- On-first-encounter protocol: restate → confirm → identify goal → flag gaps → analyze
- `[OBSERVED]` / `[ASSUMPTION]` tagging discipline throughout
- Six guiding principles baked in: practical over perfect, no automation inflation, humans in loop

**Analysis methodology (`references/methodology.md`)**
- Workflow decomposition with 7 step-level tags
- Bottleneck detection: 7 signal types, 4 severity levels
- Manual task judgment checklist: 8 criteria for automation vs. optimize-human decision
- Communication flow analysis: 7 inefficiency patterns with async/sync framework
- Dependency chain mapping: sequential, parallel, hidden, and circular dependency detection
- Three fully worked example analyses: client onboarding, weekly reporting, bug triage

**Output formats and scoring (`references/formats.md`)**
- Full Operational Audit Report template (10 sections)
- Bottleneck Severity Score (BSS): weighted 4-dimension formula, 1–10 scale
- Automation Suitability Index (ASI): 6-dimension scoring with hard rules
- Impact-Feasibility Priority Matrix (P1 Quick Win / P1 Strategic / P2 / P3)
- ROI estimation with India/global rate proxies and explicit caveats
- 6-category risk flag system with mitigation template
- Human collaboration decision format
- 30-day implementation readiness checklist
- 5 post-implementation operational metrics

---

## Roadmap (Planned)

### [1.1.0] — Upcoming
- `examples/` folder: additional worked analyses (HR onboarding, content publishing pipeline, support ticket triage)
- RACI mapping output format
- Process maturity scoring (ad-hoc → managed → optimized)

### [1.2.0] — Future
- Multi-team workflow analysis support
- Comparative analysis mode (current state vs. proposed state side-by-side)
- Integration with common tool ecosystems (Notion, Jira, Asana workflow descriptions)

---

*To suggest a feature or report an issue, open a [GitHub Issue](../../issues).*
