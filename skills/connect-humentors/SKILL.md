---
name: connect-humentors
description: Connect and verify the Humentors / CoGuru MCP connector. Use when auth fails, the user asks to connect Humentors, or before other Humentors tools.
---

# Connect Humentors

The live tools come from the remote MCP server `humentors` (`/mcp` + OAuth). Do not invent personas or call mentee/booking tools until auth works.

## Steps

1. If tools return unauthorized / invalid token / “reconnect”, tell the user to Connect:
   - In Claude Code: run `/mcp`, select **humentors**, complete browser login/consent.
   - In Claude.ai: Customize → Connectors → Humentors / custom URL `{MCP}/mcp`.
2. Call `health_check`. Expect `status: ok`.
3. Call `whoami` again for the current app state. Do not reuse an earlier whoami.
   - If `authenticated` is false, stop and ask the user to Connect again.
   - Read `primaryPersona` / roles. Do not guess MENTEE vs MENTOR.
4. Never print `orgRef` or other refs/IDs to the user. Keep them only for later tool calls.

## After connect

- MENTEE goal invite flow → skill `/humentors-coguru:mentee-goals`
- Public mentor booking → skill `/humentors-coguru:book-public-session`
