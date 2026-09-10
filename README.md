**# 6OAM Outbound Sales Voice Agent

An AI voice agent that makes outbound cold-calls on behalf of **6OAM**, an
all-in-one AI Growth Engine platform, to introduce the product, gauge
interest, and book a follow-up demo — entirely over a live phone call.

Built on **Samvaad**, a voice-agent platform for designing and deploying
production phone-call agents (speech-to-text, LLM reasoning, text-to-speech,
telephony, and call analytics in one pipeline).

## What it does

- Places outbound calls to leads from an outreach list and opens the
  conversation the instant the call connects — no dead air, no waiting on
  the caller to speak first.
- Confirms who it's speaking to, addressing them respectfully (`Mr.` / `Ms.`
  based on known gender), and checks language preference (English or Hindi)
  before pitching.
- Delivers a short, energetic pitch tailored to the lead's company/industry,
  using real proof points (businesses served, tools replaced, cost savings).
- Handles common sales objections (existing tools, pricing questions, "not
  the right time", "is this AI?") with quick, natural reactions rather than
  scripted rebuttals.
- Converts interest into a booked follow-up: instead of negotiating a
  meeting time on the call (which creates friction and back-and-forth), the
  agent simply confirms a calendar link will be sent to the lead's WhatsApp
  so they can pick their own convenient slot.
- Every agent turn ends with a specific question or a clear next action —
  never a flat, open-ended statement that leaves the caller hanging.
- Classifies every call into a clean outcome (`meeting_booked`,
  `interested_callback`, `not_interested`, `wrong_person`, `busy`,
  `voicemail`, `dnd`, `hostile`, `call_disconnected`) and pushes the result
  to a Google Sheet automatically when the call ends.
- Gracefully exits on hostility, do-not-call requests, or wrong numbers —
  no argument, no pushing, no repeated pitching.

## Why this design

- **Calendar-link scheduling over live time negotiation.** Asking a cold
  lead to commit to a day/time mid-call is a common drop-off point. Handing
  scheduling control to the lead via a link (sent where they already are —
  WhatsApp) removes friction and avoids awkward back-and-forth.
- **Always-forward conversation turns.** Voice conversations stall when a
  turn ends on a flat statement. The agent is designed so every line either
  asks something concrete or moves straight into the next action.
- **Respectful, minimal-friction identity check.** Title and name are
  confirmed once, briefly, and never re-litigated later in the call — real
  callers don't want to be re-verified three times in five minutes.
- **Objection handling with a cap.** Objections are addressed at most twice;
  after that, the lead's stance is accepted as final. This avoids the agent
  sounding pushy or scripted.

## Architecture

- **Voice runtime:** Samvaad (speech-to-text → LLM → text-to-speech,
  telephony-integrated)
- **Languages:** English and Hindi, with automatic language detection/switch
  mid-call
- **Outcome capture:** post-call variables (call disposition, WhatsApp
  number, meeting outcome, call summary) extracted automatically after each
  call
- **Integration:** a webhook fires at call end, pushing structured call data
  to a Google Sheet via Apps Script — no manual logging

## Sample call flow

1. Agent opens immediately: introduces itself and 6OAM, confirms who it's
   speaking with.
2. Confirms language preference.
3. Delivers a short value pitch relevant to the lead's business.
4. Gauges interest; handles any objections naturally.
5. If interested: explains a calendar link is coming to WhatsApp, collects
   the number, confirms, and closes — no time negotiation on the call.
6. If not interested, busy, hostile, or the wrong contact: exits gracefully
   with the appropriate outcome logged.

## Status

Prototype / internal demo — built and iterated using Samvaad's voice-agent
authoring tools.
**
