# Eval Checklist — Manual QA for Human Reviewers

Use this checklist when spot-checking triage outputs. Recommended frequency: 10–20 tickets
per week, sampled across urgency levels and channels.

---

## Section 1: Categorization Accuracy

- [ ] Is the primary category correct?
- [ ] Is the subcategory correct or the closest available match?
- [ ] If multiple categories apply, is the primary one the most operationally useful?
- [ ] Does the category match what the customer actually needs — not just what they said?

**Override rate target:** <10% of checked tickets
**If override rate is higher:** Review category taxonomy for missing subcategories

---

## Section 2: Urgency Accuracy

- [ ] Is the urgency level appropriate for the actual risk and business impact?
- [ ] If CRITICAL was assigned, is there a clear documented trigger (legal, safety, etc.)?
- [ ] If CRITICAL was NOT assigned, could the message have warranted it?
- [ ] Was urgency over-inflated (e.g., LOW assigned as HIGH)?
- [ ] Was urgency under-inflated (e.g., CRITICAL missed)?

**False CRITICAL rate target:** <5%
**Missed CRITICAL rate target:** 0% — review all misses in team meeting

---

## Section 3: Risk Flag Accuracy

- [ ] Were all applicable risk flags detected?
- [ ] Were any false-positive flags raised (flags with no evidence in the message)?
- [ ] If GDPR_DSAR was flagged, was the 30-day clock noted?
- [ ] If SAFETY_CONCERN was flagged, was escalation immediate and human-routed?

---

## Section 4: Key Information Extraction

- [ ] Was the core issue correctly identified in one line?
- [ ] Were order/account references correctly extracted?
- [ ] Was the customer's actual ask (refund / fix / explanation) correctly identified?
- [ ] Were prior contact signals ("again," "third time") detected and flagged?
- [ ] Was any [UNKNOWN] placeholder appropriate — or should the information have been found?

---

## Section 5: Draft Response Quality

- [ ] Is the tone appropriate for the channel (formal email vs. casual WhatsApp)?
- [ ] Does the response open with empathy for ESCALATED customers?
- [ ] Does the response avoid making unauthorized commitments?
- [ ] Are any placeholders clearly marked for agent completion?
- [ ] Would you be comfortable sending this response with minor edits?
- [ ] Does the response address the customer's actual ask?

**Draft adoption rate target:** >60% (agent sends with <20% edits)
**If adoption rate is low:** Review response templates and tone guidelines

---

## Section 6: Confidence Handling

- [ ] For LOW or INSUFFICIENT confidence outputs, was the flag clear and specific?
- [ ] Did LOW confidence outputs avoid false precision (e.g., specific category with low evidence)?
- [ ] Were clarification-request drafts generated for INSUFFICIENT confidence cases?

---

## Section 7: Recommended Actions

- [ ] Is action 1 truly the most immediate step?
- [ ] Are actions specific and operational (not vague like "look into it")?
- [ ] Is escalation recommended where it should be?
- [ ] Are actions in the right order of priority?

---

## Section 8: Edge Case Flags

Check these specific scenarios at least monthly:

- [ ] Very short message (<10 words): Was INSUFFICIENT confidence returned?
- [ ] Non-English message: Was language detected and noted?
- [ ] Positive feedback: Was urgency correctly assigned LOW?
- [ ] Safety concern keywords: Was CRITICAL + immediate escalation triggered?
- [ ] Legal threat phrases: Was CRITICAL + no-draft-response rule followed?
- [ ] Duplicate/repeat contact: Was prior contact flagged and ticket merge recommended?

---

## Monthly Review Meeting Agenda

1. Review false CRITICAL misses (target: 0)
2. Review urgency override log (target: <15%)
3. Review draft adoption rate (target: >60%)
4. Identify new trigger phrases to add to urgency-rules.json
5. Identify new subcategories to add to category-taxonomy.json
6. Flag any edge cases not covered by current rules

---

## Signing Off

Reviewer name: ___________________________
Tickets reviewed: ______  Period: __________
Overall accuracy rating (1–5): _____________
Notes: ____________________________________
