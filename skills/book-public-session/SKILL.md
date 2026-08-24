---
name: book-public-session
description: Book a public Humentors mentor session. Use when the user wants to browse public mentors, see slots, or check out a public session.
---

# Book a public session

Requires a connected and authenticated Humentors MCP session.

## Flow

1. Call `health_check`, then `list_public_mentors` again. Do not reuse earlier mentor lists.
   - Use optional search, skills, page, and limit filters when helpful.
   - Prefer mentors with `allowPublicSessions=true` when the user wants to book.
   - Present a profile card: name, photo URL, tagline, skills, LinkedIn verification, public-session availability.
   - Keep `mentorRef` internal. Never print refs or UUIDs.
2. Call `get_available_slots` with the chosen `mentorRef` (and timezone if the user gave one).
   - Pass an IANA timezone such as `Asia/Kolkata` when known.
   - Show start/end times only and keep both values from the selected slot.
3. Call `book_public_session` with the mentor ref and the chosen `sessionStartAt` and `sessionEndAt`.
   - If the user just connected or reconnected, call `whoami` first and confirm `authenticated=true`.
   - The attendee name and email are taken from the authenticated Humentors account; never ask the user to provide them.
   - For a free session, confirm that booking succeeded.
   - For a paid session, always show the returned checkout URL so the user can complete payment.
   - Pass the timezone when known. Do not print internal IDs.

## Rules

- Booking order is always: list mentors → slots → book.
- Do not invent slot times or mentor refs.
- Pass the current ISO timestamp as `asOf` on every tool call.
- Always re-call tools after the user changes data in the Humentors app. Never reuse earlier tool results.
