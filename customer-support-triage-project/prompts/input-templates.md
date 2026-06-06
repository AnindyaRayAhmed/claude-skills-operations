# Input Templates — Customer Support Triage Assistant

Copy and fill in the appropriate template before sending to the skill or API.
All fields marked `[required]` must be populated. Others are optional but improve output quality.

---

## Email

```
CHANNEL: email
FROM: [Customer name — required]
ACCOUNT: [Account ID or email — if available]
MESSAGE:
[Paste full email body here — required]

CONTEXT:
[Prior ticket IDs, account notes, or previous conversation summary — optional]
```

---

## Live Chat

```
CHANNEL: chat
FROM: [Customer name or chat ID — required]
ACCOUNT: [Account ID if available]
MESSAGE:
[Paste chat message or short transcript — required]

CONTEXT:
[Prior chat sessions or ticket history — optional]
```

---

## WhatsApp

```
CHANNEL: whatsapp
FROM: [Phone number or name — required]
ACCOUNT: [Account reference if known]
MESSAGE:
[Paste WhatsApp message — required]

CONTEXT:
[Prior WhatsApp history or linked ticket — optional]
```

---

## Helpdesk Ticket

```
CHANNEL: ticket
FROM: [Submitter name — required]
ACCOUNT: [Account or order ID — if available]
TICKET_ID: [Existing ticket ID — if this is a follow-up]
MESSAGE:
[Paste ticket description — required]

CONTEXT:
[Prior ticket activity, agent notes, or status updates — optional]
```

---

## Call Summary

```
CHANNEL: call_summary
FROM: [Customer name — required]
ACCOUNT: [Account ID — if available]
CALL_DATE: [Date of call]
AGENT: [Agent who handled the call — optional]
MESSAGE:
[Paste call transcript or summary — required]

CONTEXT:
[Prior issues, ticket history, CRM notes — optional]
```

---

## Social Media

```
CHANNEL: social
FROM: [@handle or platform username — required]
PLATFORM: [Twitter/X | Facebook | Instagram | LinkedIn | TikTok]
POST_URL: [Link to original post — if available]
MESSAGE:
[Paste post or comment text — required]

CONTEXT:
[Any prior DMs or known account — optional]
```

---

## Batch Input (Multiple Messages)

```
BATCH TRIAGE REQUEST
Total messages: [N]
─────────────────────
[1]
CHANNEL: [channel]
FROM: [name or ID]
MESSAGE:
[message text]
─────────────────────
[2]
CHANNEL: [channel]
FROM: [name or ID]
MESSAGE:
[message text]
─────────────────────
[continue for all N messages]
```

Batch outputs will be numbered `[1]`, `[2]`, etc. in the same order.
Any message that cannot be parsed will be returned as `[N] PARSE FAILED — [reason]`.

---

## Minimal Input (Unstructured)

If you don't have time to format, paste the raw message as-is. The skill will extract what
it can and note what's missing in the Confidence Note. For best results, always include channel.

```
[Raw customer message here]
```
