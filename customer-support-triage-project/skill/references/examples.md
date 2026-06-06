# Example Interactions — Customer Support Triage Skill

---

## Example 1: Escalated Billing Complaint (Email)

**Input:**
```
CHANNEL: email
FROM: Priya Sharma
ACCOUNT: ACC-88421
MESSAGE:
I have now contacted your company THREE TIMES about the same issue and nobody has resolved it.
You charged me TWICE for my subscription in November — I have the bank statements to prove it.
I've been a customer for 6 years and this is absolutely unacceptable. If this is not fixed by
Friday I will be disputing the charge with my bank and posting about this on every review site
I can find. Absolutely disgusted.
```

**Output:**
```
─────────────────────────────────────────
TRIAGE REPORT
─────────────────────────────────────────
CATEGORY       : Billing & Payments → Incorrect charge / overcharge
URGENCY        : HIGH
EMOTIONAL STATE: ESCALATED
SENTIMENT SCORE: 1
RISK FLAGS     : REPEAT_CONTACT | CHURN_SIGNAL | MEDIA_RISK | FINANCIAL_DISPUTE
DUPLICATE CHECK: UNKNOWN (no prior ticket history provided — check ACC-88421)
─────────────────────────────────────────
KEY INFORMATION EXTRACTED
─────────────────────────────────────────
• Issue:        Double-charged for subscription in November
• Product/Area: Subscription billing
• Order/Ref:    Account ACC-88421
• Timeline:     Contacted 3 times previously; deadline stated: Friday
• Prior Contact: Yes — claims 3 prior contacts, unresolved
• Customer Ask: Refund of duplicate charge; expects resolution by Friday
─────────────────────────────────────────
SUMMARY
─────────────────────────────────────────
Long-term customer (6 years) claims duplicate subscription charge in November,
contacting for the third time without resolution. Threatening bank dispute and
public review posting. High churn and media risk. Requires urgent billing review
and senior agent ownership.
─────────────────────────────────────────
RECOMMENDED ACTIONS
─────────────────────────────────────────
1. Pull account ACC-88421 immediately — verify November billing records
2. Check prior ticket history — merge or reference existing cases
3. Assign to senior billing agent; do not leave in standard queue
4. If duplicate charge confirmed, process refund and notify customer same day
5. If refund policy allows, consider goodwill gesture (month credit) given tenure
─────────────────────────────────────────
DRAFT FIRST RESPONSE
─────────────────────────────────────────
Subject: Re: Your Recent Billing Concern — We're On It

Dear Priya,

I'm really sorry this has happened — and especially sorry that this is the third time
you've had to reach out about the same issue. That's not acceptable, and I take full
responsibility for making sure it gets resolved now.

I've flagged your account (ACC-88421) as a priority and our billing team will be
reviewing the November charges straight away. I'll personally ensure you receive an
update by [insert date — confirm with billing team before sending].

Thank you for your patience, and for being with us for six years — we don't take that
lightly.

[Agent Name]
[Team/Company]
─────────────────────────────────────────
CONFIDENCE NOTE
─────────────────────────────────────────
HIGH — Issue is clear. Draft response is intentionally non-committal on refund amount
and timeline; agent must confirm both with billing before sending. Do not send as-is.
─────────────────────────────────────────
```

---

## Example 2: Legal Threat (Chat)

**Input:**
```
CHANNEL: chat
FROM: User ID 9912
MESSAGE:
My personal data was shared with a third party without my consent. I have not agreed to this
in any terms I signed. My solicitor has advised me I have grounds to pursue this under GDPR.
I want all my data deleted and a full explanation of what was shared and with whom.
```

**Output:**
```
─────────────────────────────────────────
TRIAGE REPORT
─────────────────────────────────────────
CATEGORY       : Account Management → Data export / deletion (GDPR) + Complaints → Legal threat
URGENCY        : CRITICAL
EMOTIONAL STATE: FRUSTRATED
SENTIMENT SCORE: 2
RISK FLAGS     : LEGAL_THREAT | GDPR_DSAR | FRAUD_SUSPICION (unverified data sharing claim)
DUPLICATE CHECK: UNKNOWN
─────────────────────────────────────────
KEY INFORMATION EXTRACTED
─────────────────────────────────────────
• Issue:        Alleged unauthorized sharing of personal data with third party
• Product/Area: Data privacy / account
• Order/Ref:    User ID 9912
• Timeline:     Not specified — GDPR response clock begins at receipt
• Prior Contact: Not mentioned
• Customer Ask: Full data deletion + explanation of what was shared and with whom
─────────────────────────────────────────
SUMMARY
─────────────────────────────────────────
Customer alleges data was shared with a third party without consent and has engaged
a solicitor. This is a formal GDPR Subject Access + Erasure Request with an explicit
legal threat. CRITICAL priority. Must be handled by DPO or privacy-designated team.
GDPR response deadline: 30 days from today.
─────────────────────────────────────────
RECOMMENDED ACTIONS
─────────────────────────────────────────
1. DO NOT send standard response — escalate to DPO / privacy team immediately
2. Log as formal DSAR (Data Subject Access Request) + Erasure Request — start 30-day clock
3. Do not make any statements about whether data was or wasn't shared until investigated
4. Legal team should be notified of solicitor involvement
5. Acknowledge receipt to customer within the hour (use draft below — approved for this scenario only)
─────────────────────────────────────────
DRAFT FIRST RESPONSE (ACKNOWLEDGEMENT ONLY — do not address substance)
─────────────────────────────────────────
Hi,

Thank you for reaching out. I want to confirm that we've received your message and are treating
it as a formal data request under GDPR. Your concern has been escalated to our dedicated privacy
team, who will be in touch to handle this properly and within the required timeframe.

If you have a reference from your solicitor you'd like us to note, please share it here or
via [privacy contact email].

[Agent Name]
─────────────────────────────────────────
CONFIDENCE NOTE
─────────────────────────────────────────
HIGH — Categorization and escalation path are clear. Agent must NOT engage on the
data-sharing allegation substantively. Send acknowledgement only; all further
communication must go through privacy/legal team.
─────────────────────────────────────────
```

---

## Example 3: WhatsApp — Simple Order Inquiry (Low Urgency)

**Input:**
```
CHANNEL: whatsapp
FROM: +91 98XXX XXXXX
MESSAGE:
Hi! My order #ORD-44521 was supposed to arrive yesterday but it still hasn't come.
Can you check? Thanks
```

**Output:**
```
─────────────────────────────────────────
TRIAGE REPORT
─────────────────────────────────────────
CATEGORY       : Orders & Fulfillment → Delivery delay
URGENCY        : LOW
EMOTIONAL STATE: NEUTRAL
SENTIMENT SCORE: 4
RISK FLAGS     : NONE
DUPLICATE CHECK: UNKNOWN
─────────────────────────────────────────
KEY INFORMATION EXTRACTED
─────────────────────────────────────────
• Issue:        Order not arrived on expected delivery date
• Product/Area: Order fulfillment / logistics
• Order/Ref:    ORD-44521
• Timeline:     Expected yesterday, still pending
• Prior Contact: Not mentioned
• Customer Ask: Status check
─────────────────────────────────────────
SUMMARY
─────────────────────────────────────────
Standard delivery delay query. Customer is polite and first-contact.
Agent should check order tracking for ORD-44521 and reply with status.
─────────────────────────────────────────
RECOMMENDED ACTIONS
─────────────────────────────────────────
1. Look up ORD-44521 in order management system
2. Check courier tracking status
3. Reply with ETA or, if lost, initiate standard lost parcel process
─────────────────────────────────────────
DRAFT FIRST RESPONSE
─────────────────────────────────────────
Hi! Thanks for reaching out 😊 Sorry to hear your order hasn't arrived yet —
let me check on that for you right now.

[After checking: "Your order ORD-44521 is showing [status] and is expected to
arrive [date]. Apologies for the delay!" / or initiate lost parcel flow]
─────────────────────────────────────────
CONFIDENCE NOTE
─────────────────────────────────────────
HIGH — Straightforward inquiry. Draft includes a placeholder for agent to fill
in after checking the system. Do not send the bracketed placeholder text.
─────────────────────────────────────────
```

---

## Example 4: Social Media — Angry Public Post

**Input:**
```
CHANNEL: social
FROM: @angry_customer_99
MESSAGE:
@CompanyName your app has been broken for 3 days and your support team just keeps
closing my tickets without fixing anything!!! This is a JOKE. Never using you again.
```

**Output:**
```
─────────────────────────────────────────
TRIAGE REPORT
─────────────────────────────────────────
CATEGORY       : Technical Support → Product not working / bug + Complaints → Service quality
URGENCY        : HIGH
EMOTIONAL STATE: ESCALATED
SENTIMENT SCORE: 1
RISK FLAGS     : CHURN_SIGNAL | REPEAT_CONTACT | MEDIA_RISK
DUPLICATE CHECK: POSSIBLE DUPLICATE — check for open tickets under this handle/account
─────────────────────────────────────────
KEY INFORMATION EXTRACTED
─────────────────────────────────────────
• Issue:        App broken for 3 days; tickets being closed without resolution
• Product/Area: App / technical
• Order/Ref:    [UNKNOWN — no account reference]
• Timeline:     3 days ongoing
• Prior Contact: Yes — multiple tickets, reportedly closed by support
• Customer Ask: Fix the issue; implied public validation of frustration
─────────────────────────────────────────
SUMMARY
─────────────────────────────────────────
Public-facing escalation on social media. Customer has existing open/closed tickets
and is publicly signaling churn and dissatisfaction. Move to private channel fast
to avoid further public visibility. Internal review of ticket-closing behavior needed.
─────────────────────────────────────────
RECOMMENDED ACTIONS
─────────────────────────────────────────
1. Respond publicly within 30 minutes (use draft — brief, empathetic, move to DM)
2. In DM: collect account details and link to ticket history
3. Review why tickets were closed — escalate to team lead if premature closure confirmed
4. If app bug is real, check if it affects other customers — may require tech escalation
─────────────────────────────────────────
DRAFT FIRST RESPONSE (PUBLIC — keep brief)
─────────────────────────────────────────
Hi, we're really sorry to hear this — 3 days without a working app is not OK, and we
understand your frustration. Please DM us your account details and we'll make sure this
gets looked at properly by someone senior. We want to make this right.
─────────────────────────────────────────
CONFIDENCE NOTE
─────────────────────────────────────────
MEDIUM — No account ID available. Ticket-closing claim unverified. Public response
draft is intentionally vague until facts are confirmed in DM.
─────────────────────────────────────────
```

---

## Example 5: Low-Confidence / Ambiguous Input

**Input:**
```
CHANNEL: ticket
MESSAGE:
it keeps doing the thing again
```

**Output:**
```
─────────────────────────────────────────
TRIAGE REPORT
─────────────────────────────────────────
CATEGORY       : Unclassifiable
URGENCY        : UNKNOWN
EMOTIONAL STATE: NEUTRAL
SENTIMENT SCORE: 3
RISK FLAGS     : NONE
DUPLICATE CHECK: UNKNOWN
─────────────────────────────────────────
KEY INFORMATION EXTRACTED
─────────────────────────────────────────
• Issue:        [UNKNOWN — message too vague to determine]
• Product/Area: [UNKNOWN]
• Order/Ref:    [UNKNOWN]
• Timeline:     "again" implies prior occurrence — check ticket history
• Prior Contact: Likely yes ("again") — but no reference provided
• Customer Ask: [UNKNOWN]
─────────────────────────────────────────
SUMMARY
─────────────────────────────────────────
Message is too brief to triage meaningfully. Likely a follow-up to a prior interaction
("again" and "the thing" imply shared context). Check ticket history for this customer
before responding.
─────────────────────────────────────────
RECOMMENDED ACTIONS
─────────────────────────────────────────
1. Search helpdesk for prior tickets from this customer/account
2. If found, link and handle in context of existing issue
3. If not found, send clarification request (see draft)
─────────────────────────────────────────
DRAFT FIRST RESPONSE
─────────────────────────────────────────
Hi,

Thanks for reaching out! It sounds like you may have been in touch with us before about
this — could you give us a little more detail about what's happening so we can look into
it properly? For example:

- What is the issue you're seeing?
- When did it start / come back?
- Your account email or order number (if relevant)

We want to get this sorted for you quickly!

[Agent Name]
─────────────────────────────────────────
CONFIDENCE NOTE
─────────────────────────────────────────
INSUFFICIENT — Cannot determine issue, product, or intent from this message alone.
Do not assign category or urgency until more information is received.
Human review required before any action beyond clarification request.
─────────────────────────────────────────
```

---

## Example 6: Positive Feedback (Compliment)

**Input:**
```
CHANNEL: email
FROM: James Okafor
MESSAGE:
Just wanted to say — your support agent Nadia was absolutely fantastic yesterday.
She sorted out my whole issue in one call and even followed up the next morning to
check I was happy. That's rare. Please pass on my thanks.
```

**Output:**
```
─────────────────────────────────────────
TRIAGE REPORT
─────────────────────────────────────────
CATEGORY       : Other → Compliment / positive feedback
URGENCY        : LOW
EMOTIONAL STATE: POSITIVE
SENTIMENT SCORE: 5
RISK FLAGS     : NONE
DUPLICATE CHECK: NO MATCH
─────────────────────────────────────────
KEY INFORMATION EXTRACTED
─────────────────────────────────────────
• Issue:        N/A — positive feedback
• Product/Area: Customer support (agent Nadia)
• Order/Ref:    [UNKNOWN]
• Timeline:     Yesterday + follow-up same morning
• Prior Contact: Yes — resolved call with Nadia
• Customer Ask: Pass thanks to Nadia
─────────────────────────────────────────
SUMMARY
─────────────────────────────────────────
Unsolicited compliment for agent Nadia. Strong satisfaction signal. Recommend
logging for agent recognition and responding warmly.
─────────────────────────────────────────
RECOMMENDED ACTIONS
─────────────────────────────────────────
1. Forward compliment to Nadia's team lead for recognition
2. Log as positive CSAT data point
3. Reply warmly to James — takes 2 minutes, high goodwill value
─────────────────────────────────────────
DRAFT FIRST RESPONSE
─────────────────────────────────────────
Subject: Re: Your Kind Words

Dear James,

Thank you so much for taking the time to share this — it genuinely means a lot.
I'll make sure Nadia and her team know how much you appreciated the support.
It's always wonderful to hear when we've been able to help.

We look forward to serving you again!

Warm regards,
[Agent Name]
─────────────────────────────────────────
CONFIDENCE NOTE
─────────────────────────────────────────
HIGH — Clear intent. No issues to resolve. Response is low-stakes and ready to send.
─────────────────────────────────────────
```
