# 04 Analysis and Report

## Pipeline
Answers → structured business profile (JSON) → signal flags → bottleneck scoring → recommendation matching → report.

## Business profile (extracted)
```json
{
  "business_type": "salon", "staff_count": 3,
  "channels": ["WhatsApp", "phone"],
  "tools_in_use": ["paper diary", "WhatsApp"],
  "pains": [{"area": "booking", "detail": "forgets to reply", "hours_per_week": 5}],
  "unknowns": ["monthly_revenue"]
}
```

## Bottleneck detection
1. **Rules:** question `signals` raise flags (e.g. `manual_booking`, `no_followup`, `late_invoicing`, `paper_inventory`).
2. **LLM scoring:** given profile + flags, the LLM groups flags into bottlenecks and scores each:
   - **Impact** (1-5): time lost, money lost, customer experience
   - **Effort to fix** (1-5): low for a free tool, high for process change
   - **Confidence** (low/med/high): based on how well the user quantified it
3. **Priority** = impact ÷ effort, ties broken by confidence. Top 3 become "start here".
4. The LLM must cite which user answers support each bottleneck, to avoid invented issues.

## Report structure
1. **Summary** (3-4 sentences): what you do well, the biggest opportunity.
2. **Start here:** top 3 bottlenecks, each with:
   - What's happening (in the user's own words)
   - Why it costs you (time/money estimate, flagged as rough)
   - Fix in 3 simple steps
   - Recommended tools (1-2, with cost; see [05](05-tools-catalog.md))
3. **Quick wins:** things doable today with no new tool.
4. **Later:** lower-priority bottlenecks.
5. **Your 30-day plan:** week-by-week checklist.
6. **Things we weren't sure about:** unknowns and what to check.

## Format and sharing
In-app page, printable PDF, share link, and a WhatsApp-friendly short summary. Plain language, short paragraphs, icons, grade-6 reading level.

## Guardrails
- Mark estimates as estimates; no precise financial claims.
- No legal, tax or medical advice; suggest a professional where relevant.
- Recommend only tools present in the catalog.
- Users can give a thumbs up or down on each recommendation, feeding quality review.
