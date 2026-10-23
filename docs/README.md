# Business Helper (working title)

A chat and voice assistant that helps non-technical small business owners find what is slowing their business down, and fix it with cheap or free tools.

## Pitch
The owner talks (or types) through a friendly, guided conversation about how their business runs day to day. When the assistant knows enough, it produces a plain-language report: the top bottlenecks, why they matter, and simple steps and low-cost tools to fix them.

## Key decisions (draft v0.1)
| Area | Decision |
|---|---|
| Audience | Any micro/small business, any industry |
| Interaction | Chat and voice equal from day one, switchable anytime |
| Agent | Scripted journeys + LLM adaptive follow-ups and data extraction |
| Stack | Next.js PWA, Supabase (Postgres), Claude API |
| Accounts | Anonymous start, optional sign-up (magic link) to save |
| Languages | English only in v1, i18n-ready |
| Tool advice | Curated, tagged catalog; LLM matches and explains |
| Business model | Undecided (see [08](08-open-questions.md)) |

## Doc map
1. [Product vision](01-product-vision.md)
2. [User experience](02-user-experience.md)
3. [Conversation design](03-conversation-design.md)
4. [Analysis and report](04-analysis-and-report.md)
5. [Tools catalog](05-tools-catalog.md)
6. [Architecture](06-architecture.md)
7. [Roadmap and MVP](07-roadmap-and-mvp.md)
8. [Open questions](08-open-questions.md)
