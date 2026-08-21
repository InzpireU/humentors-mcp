---
name: connect-humentors
description: Connect and verify the Humentors MCP connector. Use when auth fails, the user asks to connect Humentors, or before other Humentors tools.
---

# Connect Humentors

The live tools come from the remote MCP server `humentors` (`/connector` + OAuth). Do not invent personas or call mentee/booking tools until auth works.

## Steps

1. If tools return unauthorized / invalid token / “reconnect”, tell the user to Connect:
   - In Claude Code: run `/mcp`, select **Humentors**, complete browser login/consent.
   - In Claude.ai: Customize → Connectors → Humentors / custom URL `{MCP}/connector`.
2. Call `health_check`. Expect `status: ok`.
3. Call `whoami` again for the current app state. Do not reuse an earlier whoami.
   - If `authenticated` is false, stop and ask the user to Connect again.
   - Read `primaryPersona` / roles. Possible personas include MENTEE, MENTOR, MENTEE_AND_MENTOR, ADMIN, and NO_ROLE.
   - Treat MENTEE_AND_MENTOR as eligible for mentee flows.
4. Never print `orgRef` or other refs/IDs to the user. Keep them only for later tool calls.

## Live data rules

- Pass the current ISO timestamp as `asOf` on every tool call.
- Call the relevant tool again for every request. Never reuse earlier results, refs, roles, goals, mentors, or slots.
- After a connect or reconnect, call `whoami` before any account-specific tool.
- Never ask for an attendee name or email when booking; the API gets both from the authenticated account.
- If login expired or the account changed during Connect, ask the user to disconnect, sign in to the intended Humentors account, and reconnect.

## After connect

- MENTEE goal invite flow → skill `/humentors-coguru:mentee-goals`
- Public mentor booking → skill `/humentors-coguru:book-public-session`
