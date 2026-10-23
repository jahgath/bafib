# 03 Conversation Design

## Model
**Scripted journeys + LLM follow-ups.** The script guarantees coverage and predictability. The LLM handles three jobs only: (1) rephrase and add empathy, (2) ask 0-2 adaptive follow-ups when an answer is vague or reveals a pain point, (3) extract structured data from free-form answers.

## Structure
1. **Intro/triage** (about 6 questions): business type, size, how long operating, main goal, biggest frustration, current tools.
2. **Topic modules** (each 4-8 questions, selected by relevance from triage):
   - Getting customers and leads
   - Taking orders / bookings
   - Delivering the service or product (operations, scheduling)
   - Inventory and suppliers
   - Staff and tasks
   - Invoicing, payments and cash flow
   - Customer communication and follow-up
   - Marketing and online presence
   - Record keeping and admin
3. **Wrap-up:** "Anything else that eats your time?", confirm the summary.

Not every user sees every module; irrelevant ones are skipped (e.g. no inventory for a consultant).

## Question schema
```yaml
id: ops_booking_01
module: operations
text: "When a customer wants to book, how do they usually do it?"
help: "For example: they call, message you on WhatsApp, or walk in."
answer_type: single_choice | multi_choice | free_text | number | scale
options: [Phone call, WhatsApp/messages, Walk-in, Website, Other]
extract: {field: booking_channels, type: list}
signals:                 # feeds bottleneck detection
  - if: booking_channels includes "WhatsApp/messages" and tool_booking == none
    flag: manual_booking
follow_up:
  trigger: answer_vague | pain_keyword | flag_raised
  max: 2
required: false
skip_if: business_type in [online_only]
```

## Follow-up rules
- Ask a follow-up only if it likely changes a recommendation.
- Max 2 per question, max about 25% of total questions overall.
- Prefer "how much / how often / how long" to quantify pain (e.g. "hours per week on this").
- Never ask for sensitive data (bank numbers, passwords, customer personal details).

## Sufficiency criteria
Move to the report when:
- Triage complete and all selected modules answered or skipped
- For each module, key fields filled (or marked unknown)
- At least 3 quantified pain points, or the user says "that's all"
A hard cap on conversation length (about 45 turns) prevents fatigue.

## Tone guide
Friendly, patient, plain words. Short sentences. Normalize problems ("Lots of salons struggle with this"). No jargon: say "customer list", not "CRM". Praise real strengths too.

## Sample dialogue
> **Bot:** How do customers usually book with you?
> **User:** mostly whatsapp, some call
> **Bot:** Got it. Roughly how many bookings a week come through WhatsApp?
> **User:** like 30, and i forget to reply sometimes
> **Bot:** Thanks for sharing that, it is very common. When a message slips through, what usually happens?
> *(extract: channel=WhatsApp, volume=30/wk, pain=missed_replies; flag=manual_booking, response_delay)*
