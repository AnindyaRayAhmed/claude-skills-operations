# Production Usage Guide — Customer Support Triage Skill

## Integration Patterns

### Pattern 1: Pre-Queue Triage (Recommended)
Run triage on every incoming ticket before it reaches the agent queue.
- Input: Raw ticket/message from helpdesk webhook
- Output: Structured triage report attached to ticket as internal note
- Agent sees: Categorized, prioritized ticket with draft ready

### Pattern 2: On-Demand Agent Assist
Agents trigger triage manually on complex or ambiguous tickets.
- Input: Agent pastes message + optional context
- Output: Triage report in sidebar or panel
- Agent decides: Whether to use draft, override urgency, escalate

### Pattern 3: Batch Re-Triage
Re-triage backlog tickets that were categorized manually or inconsistently.
- Input: Export of open tickets with messages
- Output: Updated categories, urgency scores, risk flags
- Use for: Queue rebalancing, SLA compliance audits, staffing decisions

---

## System Prompt Deployment

When deploying as a system prompt, add these lines to your API call:

```
You are operating as the Customer Support Triage Assistant for [Company Name].
Standard response time targets: CRITICAL = 1hr, HIGH = 4hr, MEDIUM = 24hr, LOW = 72hr.
Policy exceptions require approval from: [Role/Name].
Refund authority up to [amount] is at first-line discretion.
Products/services in scope: [list].
```

Customize the bracketed fields per deployment. Do not hard-code policy details into the
skill itself — pass them at runtime to keep the skill reusable across clients.

---

## Batch Processing

For high-volume queues (100+ tickets/day), structure batch input as:

```
BATCH TRIAGE REQUEST
Total messages: N
---
[1]
CHANNEL: email
MESSAGE: ...
---
[2]
CHANNEL: chat
MESSAGE: ...
```

Output will be numbered triage reports in the same order. Flag any message that could not
be parsed with `[PARSE FAILED — message N]`.

---

## Metric Tracking Recommendations

Track these monthly to measure triage quality:
- Urgency override rate (agent disagrees with AI urgency): target <15%
- Category accuracy rate (validated by QA spot-check): target >90%
- Draft adoption rate (agent sends draft with <20% edits): target >60%
- False CRITICAL rate (flagged CRITICAL, resolved at LOW): target <5%
- Missed CRITICAL rate (not flagged, should have been): target 0%

If urgency override rate is high, review the urgency detection rules and recalibrate.
If draft adoption is low, review tone guidelines or draft templates.

---

## Multi-language Handling

The skill will attempt triage in any language but:
- Confidence will often be MEDIUM or LOW for non-English input
- Draft responses will be generated in the detected language
- Always recommend native-speaker review before sending
- For high-volume non-English queues, run language detection upstream and route accordingly

---

## Data Privacy

- Do not log full customer messages in analytics pipelines without consent
- Strip PII (card numbers, passwords, SSNs) before passing to triage if possible
- GDPR DSAR flags require a documented audit trail of who received and acted on the request
- If operating in EU: ensure your AI processing chain has appropriate DPA coverage

---

## Known Limitations

- Cannot access live order/account systems — it works only on what is in the input
- Cannot verify customer identity
- Cannot detect sarcasm reliably — treat ambiguous tone as NEUTRAL unless other signals present
- Very short messages (<10 words) will often result in LOW confidence
- Duplicate detection only works if prior context is explicitly provided in input
- Call summaries vary in quality — accuracy depends on transcription/summary quality provided
