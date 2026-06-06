# Integration Guide — Customer Support Triage Skill

How to wire this skill into your existing helpdesk and support infrastructure.

---

## Option A: Claude Skill (claude.ai / Claude for Teams)

1. Install `skill/SKILL.md` into your Claude skill library.
2. The skill triggers automatically when you paste or describe a support message.
3. Use `prompts/input-templates.md` for consistent structured input.
4. Copy triage output into your helpdesk as an internal note before assigning the ticket.

**Best for:** Teams already using Claude for Teams or Claude.ai Pro.
**Limitation:** Manual step to copy output into helpdesk. No automation.

---

## Option B: API Integration (Recommended for Production)

### Step 1: Set up your API call

```javascript
const response = await fetch("https://api.anthropic.com/v1/messages", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "x-api-key": process.env.ANTHROPIC_API_KEY,
    "anthropic-version": "2023-06-01"
  },
  body: JSON.stringify({
    model: "claude-sonnet-4-20250514",
    max_tokens: 2000,
    system: "[paste contents of prompts/system-prompt.md here]",
    messages: [
      {
        role: "user",
        content: formatTicketForTriage(incomingTicket)
      }
    ]
  })
});
```

### Step 2: Format incoming tickets

```javascript
function formatTicketForTriage(ticket) {
  return [
    `CHANNEL: ${ticket.channel}`,
    `FROM: ${ticket.customerName || 'Unknown'}`,
    `ACCOUNT: ${ticket.accountId || 'Not provided'}`,
    `MESSAGE:`,
    ticket.body,
    ``,
    `CONTEXT:`,
    ticket.priorHistory || 'No prior history provided'
  ].join('\n');
}
```

### Step 3: Parse the triage output

The output is human-readable text. Parse by section headers:

```javascript
function parseTriageOutput(text) {
  const sections = {};
  const lines = text.split('\n');
  let currentSection = null;

  for (const line of lines) {
    if (line.startsWith('CATEGORY')) {
      sections.category = line.split(':')[1].trim();
    } else if (line.startsWith('URGENCY')) {
      sections.urgency = line.split(':')[1].trim();
    } else if (line.startsWith('EMOTIONAL STATE')) {
      sections.emotionalState = line.split(':')[1].trim();
    } else if (line.startsWith('RISK FLAGS')) {
      sections.riskFlags = line.split(':')[1].trim();
    }
    // Extend for other fields as needed
  }

  return sections;
}
```

### Step 4: Write back to helpdesk

Use your helpdesk's API to attach the triage report as an internal note, set the ticket
category, and assign priority based on urgency mapping:

```javascript
const URGENCY_TO_PRIORITY = {
  CRITICAL: 'urgent',
  HIGH: 'high',
  MEDIUM: 'normal',
  LOW: 'low'
};

await helpdeskClient.tickets.update(ticketId, {
  priority: URGENCY_TO_PRIORITY[triage.urgency],
  tags: parseRiskFlags(triage.riskFlags),
  internalNote: fullTriageReport
});
```

---

## Option C: Helpdesk Native Integration

### Zendesk
- Use Zendesk's "Triggers" + API to fire triage on ticket creation
- Attach triage as internal note via Zendesk API
- Use triage urgency to set ticket priority via `priority` field
- Use triage category to set ticket group/tag via `tags` field

### Freshdesk
- Use Freshdesk Automations → "Ticket Created" webhook
- POST to your triage endpoint, write back via Freshdesk API
- Map urgency → `priority` field (1=LOW, 2=MEDIUM, 3=HIGH, 4=URGENT)

### Intercom
- Use Intercom Webhooks → `conversation.created` event
- Attach triage as internal note via Intercom Conversations API
- Tag conversation based on risk flags

### HubSpot Service Hub
- Use Workflow automation → webhook action on ticket creation
- Write triage output to ticket custom properties
- Route by urgency using HubSpot ticket pipeline stages

---

## Webhook Architecture (Recommended Pattern)

```
[Helpdesk Webhook] 
       ↓
[Triage Service — your API wrapper]
       ↓
[Claude API — triage skill]
       ↓
[Parse output]
       ↓
[Write back to helpdesk]
       ↓
[Route to correct queue]
```

**Recommended:** Run triage asynchronously. Do not block ticket creation on triage completion.
Triage should complete within 3–8 seconds per ticket.

---

## Error Handling

| Error | Action |
|-------|--------|
| API timeout | Retry once; if second timeout, assign to MEDIUM queue without triage and flag for manual review |
| Parse failure | Log raw output; assign default MEDIUM priority; flag for human triage |
| Rate limit | Queue requests; most helpdesks have lower volume than API rate limits |
| Unexpected format | Log for review; do not block ticket routing |

---

## Monitoring

Set up alerts for:
- Triage latency > 10 seconds (investigate API performance)
- CRITICAL tickets with no escalation acknowledgement within 30 minutes
- GDPR DSAR tickets not acknowledged within 24 hours
- Triage failure rate > 2% (investigate parsing or API errors)
