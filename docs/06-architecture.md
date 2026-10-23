# 06 Architecture

## Overview
```
Browser (Next.js PWA)
  ├─ Chat UI + Voice UI (shared conversation state)
  ├─ Web Speech / MediaRecorder  ──► STT service
  └─ TTS playback  ◄── TTS service
        │ HTTPS / streaming
Next.js API routes
  ├─ /api/session      create anonymous session, resume
  ├─ /api/turn         submit answer → next question
  ├─ /api/report       generate + fetch report
  └─ /api/voice        STT/TTS proxy
        │
Conversation engine (state machine)
  ├─ Journey definitions (YAML/JSON, versioned)
  ├─ Claude API: rephrase, follow-up, extraction, scoring
  └─ Rules engine: signals → flags
        │
Supabase (Postgres + Auth + Storage)
```

## Conversation engine
- Deterministic state machine picks the next scripted question; the LLM never decides the flow alone.
- Each turn: (1) store the raw answer, (2) LLM extracts structured fields (JSON schema output), (3) rules engine updates flags, (4) engine decides next question or follow-up, (5) LLM rephrases it in the tone guide.
- Journey files are versioned and validated in CI.

## Voice pipeline
- STT: start with browser Web Speech API where available, with a cloud STT fallback (provider TBD).
- TTS: cloud TTS with caching of scripted questions (they repeat, so pre-generate to cut latency and cost).
- Barge-in supported; transcript always visible and editable.

## Data model (Postgres)
- `sessions` (id, anon_token, user_id nullable, status, journey_version, created_at)
- `turns` (id, session_id, question_id, raw_answer, extracted jsonb, mode text|voice, ts)
- `profiles` (session_id, profile jsonb, flags jsonb)
- `reports` (id, session_id, content jsonb, model, created_at, share_token)
- `catalog_tools` (see [05](05-tools-catalog.md))
- `feedback` (report_id, item, rating)
- Row-level security: a session is readable only via its anon token or owning user.

## Auth
Anonymous session token (httpOnly cookie) from the first click. Optional Supabase magic link or phone OTP links the session to a user.

## Privacy and security
- Collect minimum data; discourage sensitive inputs; no customer personal data.
- Encrypt in transit and at rest; short voice retention (delete audio after transcription).
- Clear delete-my-data control; privacy policy in plain language.
- Rate limiting and prompt-injection defenses on free-text answers; the LLM output is schema-validated.

## Cost notes
Main costs: LLM calls (extraction per turn, one scoring/report call), STT/TTS. Mitigate with pre-generated TTS, small models for extraction, a larger model only for the report, and prompt caching.

## Observability
Log turn latency, drop-off point per question, extraction failures, and report ratings. No raw content in analytics logs.
