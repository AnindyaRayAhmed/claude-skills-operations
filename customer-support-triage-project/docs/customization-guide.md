# Customization Guide — Adapting the Skill for Your Business

This skill is designed to be a starting point, not a locked configuration. Here's how to
adapt each component for your specific context.

---

## 1. Category Taxonomy

**File:** `config/category-taxonomy.json`

Add subcategories relevant to your business. Examples:

**SaaS product:**
```json
{ "id": "technical.onboarding", "label": "Onboarding / setup issue" },
{ "id": "technical.mobile_app", "label": "Mobile app issue" },
{ "id": "billing.seat_management", "label": "User seat / license management" }
```

**E-commerce:**
```json
{ "id": "orders.gift_wrapping", "label": "Gift wrapping / special packaging" },
{ "id": "orders.customs_duty", "label": "Customs / import duties" }
```

**Financial services:**
```json
{ "id": "account.kyc_verification", "label": "KYC / identity verification" },
{ "id": "billing.wire_transfer", "label": "Wire transfer issue" }
```

After editing taxonomy, update the category examples in `skill/SKILL.md` to match.

---

## 2. Urgency Thresholds

**File:** `config/urgency-rules.json`

Adjust the financial threshold for HIGH urgency:
```json
"criteria": [
  "Significant financial impact (threshold: >[YOUR AMOUNT] or business-critical)"
]
```

Add industry-specific CRITICAL triggers:
```json
"trigger_phrase_overrides": {
  "phrases": [
    "... existing phrases ...",
    "FSA",           // UK financial regulator
    "FCA",           // UK Financial Conduct Authority
    "ASIC",          // Australian Securities regulator
    "patient data",  // Healthcare
    "medication"     // Healthcare
  ]
}
```

---

## 3. Response Time Targets

**File:** `prompts/system-prompt.md`

Update the SLA targets to match your support contracts:
```
Standard response time targets:
CRITICAL = [your SLA — e.g., 30 minutes]
HIGH     = [your SLA — e.g., 2 hours]
MEDIUM   = [your SLA — e.g., 8 hours]
LOW      = [your SLA — e.g., 48 hours]
```

---

## 4. Refund and Policy Authority

**File:** `prompts/system-prompt.md`

Be specific about what agents can offer without escalation:
```
First-line refund authority: Up to $50 or within 14 days of purchase, no questions asked.
Exception authority (team lead): Up to $200 or within 90 days.
Policy exceptions beyond this: Director approval required.
```

This prevents the skill from drafting commitments beyond what agents are authorized to offer.

---

## 5. Response Templates

**File:** `templates/response-templates.md`

Customize the sign-off to match your brand voice:

**Formal / enterprise:**
```
Yours sincerely,
[Agent Name]
[Company] Customer Relations
[Phone] | [Email]
```

**Friendly / consumer:**
```
Talk soon,
[Agent Name] from the [Company] team 👋
```

Add templates for your most common scenarios. For example, if subscription cancellations
are common, add a dedicated retention template.

---

## 6. Risk Flags

**File:** `config/risk-flags.json`

Add industry-specific flags:

**Healthcare:**
```json
{
  "id": "HIPAA_CONCERN",
  "label": "HIPAA / Patient Privacy Concern",
  "trigger_phrases": ["patient record", "medical history", "HIPAA", "health information"],
  "urgency_override": "CRITICAL",
  "auto_escalate": true,
  "action": "Route to compliance officer immediately."
}
```

**Financial services:**
```json
{
  "id": "REGULATORY_BREACH",
  "label": "Potential Regulatory Breach",
  "trigger_phrases": ["FCA", "FSA", "ASIC", "SEC", "complaint to regulator"],
  "urgency_override": "CRITICAL",
  "auto_escalate": true,
  "action": "Notify compliance team within 1 hour."
}
```

---

## 7. Channel Configuration

If you don't use certain channels, remove them from the tone table in `skill/SKILL.md`
to reduce noise. If you add new channels (e.g., in-app messaging, SMS), add them with
appropriate tone guidelines.

---

## 8. Multi-Brand or Multi-Product Deployments

If you support multiple brands or product lines, create a separate `system-prompt.md`
per brand with the relevant context. The core skill files stay the same — only the
system prompt changes per deployment.

```
prompts/
  system-prompt-brandA.md
  system-prompt-brandB.md
  input-templates.md        ← shared
```

---

## 9. Language and Region

For non-English markets, add to the system prompt:
```
Primary support language: [French / Spanish / Portuguese / etc.]
If customer writes in English, respond in English.
If customer writes in [primary language], respond in [primary language].
Always triage report in English for internal consistency.
```

Add region-specific regulatory triggers to `urgency-rules.json` as appropriate.
