# 02 User Experience

## Flow
Landing → Start (no sign-up) → Pick mode (Talk / Type, switchable) → Intro questions → Topic journeys → "Anything else?" wrap-up → Report generation → Report view → Save / share / download.

## Screens
1. **Landing:** one sentence of value, one big "Start" button, a "How it works" 3-step strip, a privacy note.
2. **Mode choice:** two large buttons, "Talk to me" and "I'll type". A mic/keyboard toggle stays visible throughout.
3. **Conversation:**
   - One question at a time, shown as large text and spoken aloud in voice mode.
   - Quick-reply buttons for common answers plus free input (voice or text).
   - Progress bar in plain terms ("About halfway").
   - Always-visible: Skip, Go back, Pause and save, Help ("what does this mean?").
4. **Wrap-up:** summary of what we understood ("Here is what I heard") for the user to confirm or correct before the report.
5. **Report:** see [04](04-analysis-and-report.md). Top 3 first, expandable details, share via WhatsApp/email, download PDF.
6. **Save prompt:** after the report, or when the user pauses, offer magic-link sign-up (email or phone) to keep the session.

## Chat and voice behavior
- Both share one conversation state, so a user can switch mid-way.
- Voice: tap-to-talk plus an auto-listen option, live transcript shown, tap to correct the transcript, speech output with a mute toggle.
- If the mic is denied or noisy, fall back to text without losing progress.
- The user can interrupt the bot while it speaks.

## Accessibility requirements
- WCAG 2.2 AA minimum; base font 18px+, high contrast, scalable text
- Reading level around grade 6; no jargon, define any term in-line
- Touch targets 48px+, works one-handed on a phone
- Screen reader support, captions for all spoken output
- Works on low bandwidth: lightweight PWA, resumable sessions, offline-tolerant answer queue
- Warm, human tone; optional gentle encouragement every few questions

## Edge cases
- User gives vague or one-word answers → bot offers examples or buttons
- User goes off-topic → acknowledge, gently steer back, store the note
- User abandons → auto-save locally and server-side (anonymous id), offer resume link
- User unsure ("I don't know") → valid answer, recorded as unknown, not pushed
