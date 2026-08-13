---
name: book-public-session
description: Book a public Humentors mentor session. Use when the user wants to browse public mentors, see slots, or check out a public session.
---

# Book a public session

Requires the connected Humentors MCP server. Public directory tools can work before mentee persona; checkout still needs a valid Connect session when the server requires it.

## Flow

1. Call `health_check`, then `list_public_mentors`.
   - Prefer mentors with `allowPublicSessions=true` when the user wants to book.
   - Present a profile card: name, photo URL, tagline, skills, LinkedIn verification, public-session availability.
   - Keep `mentorRef` internal. Never print refs or UUIDs.
2. Call `get_available_slots` with the chosen `mentorRef` (and timezone if the user gave one).
   - Show start/end times only.
3. Call `book_public_session` with mentor ref, attendee name/email, and chosen `sessionStartAt`.
   - Return checkout URL / success message. Do not print internal IDs.

## Rules

- Booking order is always: list mentors → slots → book.
- Do not invent slot times or mentor refs.
