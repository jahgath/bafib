# 07 Roadmap and MVP

## MVP scope
- Landing, anonymous session, chat and voice with switching
- Triage + 4 core modules: customers/leads, bookings/orders, invoicing/payments, customer follow-up
- Extraction, rules, bottleneck scoring, in-app report + PDF
- Catalog of about 40 verified tools
- Optional magic-link save
- Basic feedback (thumbs, 1-5 rating)

## Phases
| Phase | Focus | Output |
|---|---|---|
| 0. Discovery (1-2 wks) | Interview 8-10 owners across industries | Validated question lists, real pains |
| 1. Prototype (2-3 wks) | Chat-only flow, 2 modules, hand-checked report | Testable demo |
| 2. Voice + accessibility (2-3 wks) | STT/TTS, switching, a11y audit | Both modes working |
| 3. Full MVP (3-4 wks) | All MVP modules, catalog, PDF, save | Private beta |
| 4. Beta (4 wks) | 30-50 real owners, iterate | Metrics vs goals |
| 5. Post-MVP | More modules, languages, check-ins, monetization | See below |

## Testing
- Usability sessions with real non-technical owners at each phase
- Golden-set conversations (10-20 fictional businesses) with expected bottlenecks, run on every prompt or journey change
- Voice testing with accents, background noise and slow connections
- Report review by a human advisor before beta

## Risks
| Risk | Mitigation |
|---|---|
| Generic or wrong advice | Evidence-cited bottlenecks, catalog-only tools, golden-set evals |
| Voice quality varies | Text fallback, transcript editing |
| Users quit mid-way | Short journeys, progress, save and resume |
| Free tiers change | Catalog freshness process |
| Trust and privacy concerns | Plain-language policy, minimal data, delete control |
| LLM cost creep | Caching, smaller models, turn cap |

## Post-MVP ideas
Multi-language, follow-up check-ins ("did the fix work?"), industry-specific journeys, setup guides and videos, WhatsApp channel, re-assessment every 6 months, team sharing.

## Monetization options (undecided)
Free + affiliate (disclosed); freemium deep-dive plan; pay per report or subscription; B2B2C through banks, chambers of commerce or NGOs. Decision tracked in [08](08-open-questions.md).
