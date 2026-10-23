# 05 Tools Catalog

A curated, tagged list of cheap or free tools. The LLM selects from the catalog and explains fit; it never invents tools.

## Schema
```yaml
id: wa-business
name: WhatsApp Business
category: messaging
summary: "Free app with quick replies, labels and a catalog."
price_tier: free | under_10 | under_30 | over_30   # USD/month
price_note: "Free; paid API tier optional"
solves: [missed_replies, manual_booking, no_followup]   # bottleneck tags
skill_level: beginner | intermediate
setup_time: "30 minutes"
platforms: [android, ios, web]
works_with: [google-calendar]
best_for: [salon, retail, services]
setup_url: https://...
last_verified: 2026-10-01
```

## Seed categories (examples, to be verified before launch)
| Category | Examples | Solves |
|---|---|---|
| Messaging | WhatsApp Business | missed replies, quick answers |
| Booking/scheduling | Google Calendar appointment schedules, Calendly free tier, Square Appointments free | double booking, no-shows |
| Invoicing/payments | Wave, Zoho Invoice, Square | late invoicing, chasing payments |
| Accounting | Wave, Zoho Books (free tier) | record keeping |
| Customer list/CRM | HubSpot free, Google Sheets template | lost leads, no follow-up |
| Inventory | Zoho Inventory free tier, Google Sheets template | stock-outs, overordering |
| Staff/tasks | Trello, Google Sheets | unclear tasks, rosters |
| Marketing | Canva free, Google Business Profile, Mailchimp free | low visibility |
| Automation | Zapier free tier, Make free tier | repeated manual work |

## Selection rules
1. Match `solves` tags to bottleneck flags.
2. Filter by the user's skill level (default beginner) and budget (default free to under_10).
3. Prefer tools the user already has (e.g. suggest WhatsApp Business before a new app).
4. Return at most 2 tools per bottleneck, with one reason each.
5. Always include a no-tool option when it is good enough (e.g. a paper checklist or a Sheets template).

## Maintenance
- Each entry carries `last_verified`; flag entries over 90 days old.
- Quarterly review of pricing and free-tier limits (free tiers change often).
- Owner of the catalog: TBD (see [08](08-open-questions.md)).
- Affiliate links, if any, must be disclosed and must never influence ranking.
