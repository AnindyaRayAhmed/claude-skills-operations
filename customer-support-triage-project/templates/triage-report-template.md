# Triage Report Template — Blank

Use this as a reference for expected output structure, or for manual triage by agents.

---

```
─────────────────────────────────────────
TRIAGE REPORT
─────────────────────────────────────────
CATEGORY       :
URGENCY        : [ CRITICAL | HIGH | MEDIUM | LOW ]
EMOTIONAL STATE: [ ESCALATED | FRUSTRATED | NEUTRAL | POSITIVE ]
SENTIMENT SCORE: [ 1 | 2 | 3 | 4 | 5 ]
RISK FLAGS     :
DUPLICATE CHECK:
─────────────────────────────────────────
KEY INFORMATION EXTRACTED
─────────────────────────────────────────
• Issue:
• Product/Area:
• Order/Ref:
• Timeline:
• Prior Contact:
• Customer Ask:
─────────────────────────────────────────
SUMMARY
─────────────────────────────────────────


─────────────────────────────────────────
RECOMMENDED ACTIONS
─────────────────────────────────────────
1.
2.
3.
─────────────────────────────────────────
DRAFT FIRST RESPONSE
─────────────────────────────────────────


─────────────────────────────────────────
CONFIDENCE NOTE
─────────────────────────────────────────

─────────────────────────────────────────
```

---

## Field Reference

| Field | Values | Notes |
|-------|--------|-------|
| CATEGORY | See category-taxonomy.json | Primary → Subcategory |
| URGENCY | CRITICAL / HIGH / MEDIUM / LOW | See urgency-rules.json |
| EMOTIONAL STATE | ESCALATED / FRUSTRATED / NEUTRAL / POSITIVE | |
| SENTIMENT SCORE | 1 (hostile) → 5 (positive) | |
| RISK FLAGS | See risk-flags.json | Comma-separated or NONE |
| DUPLICATE CHECK | POSSIBLE DUPLICATE of #ID / NO MATCH / UNKNOWN | |
| Issue | One line | What is happening |
| Product/Area | Free text | What product, feature, or service |
| Order/Ref | Free text or [UNKNOWN] | Any reference numbers |
| Timeline | Free text | When it started, any deadlines |
| Prior Contact | Yes/No + brief note | Has customer contacted before? |
| Customer Ask | Free text | What they want: refund / fix / explanation / other |
| Summary | 2–3 sentences | Operational brief for the agent |
| Recommended Actions | Numbered list | Immediate, follow-up, escalation |
| Draft First Response | Ready-to-edit text | Channel-appropriate |
| Confidence Note | HIGH / MEDIUM / LOW / INSUFFICIENT + explanation | Flag any assumptions |
