# inzpireu-coguru

Claude Code plugin for **Humentors / CoGuru**. It does not reimplement APIs. It wraps the existing remote MCP server on `inzpireu-server` and adds skills for how to use the tools.

## What you get

| Piece | Role |
|--------|------|
| Remote MCP | Live tools over HTTPS (`/mcp`) + OAuth |
| `.mcp.json` | Points Claude Code at that MCP URL |
| Skills | Teach Claude mentee invites and public booking |

MCP tools (from `inzpireu-server`): `health_check`, `whoami`, `list_public_mentors`, `get_available_slots`, `book_public_session`, `list_mentee_goals`, `list_mentors_for_goal`, `send_goal_invite`.

## Prerequisites

- Claude Code installed
- Public HTTPS MCP origin (staging default below)
- Server env: `MCP_PUBLIC_URL`, `BASE_WEBAPP_URL`, `FIREBASE_WEB_API_KEY`

Default MCP URL in `.mcp.json`:

`https://staging-server.humentors.org/mcp`

Change this to production before publishing.

## Install (local)

```bash
claude plugin validate ./inzpireu-coguru
claude --plugin-dir ./inzpireu-coguru
```

Then:

1. `/mcp` → authenticate **humentors** (browser OAuth / Humentors login)
2. `/inzpireu-coguru:connect-humentors`
3. `/inzpireu-coguru:mentee-goals` or `/inzpireu-coguru:book-public-session`

Reload after edits: `/reload-plugins`

## Skills

| Skill | Use |
|--------|-----|
| `/inzpireu-coguru:connect-humentors` | Connect + `health_check` + `whoami` |
| `/inzpireu-coguru:mentee-goals` | Goals → mentors → invite |
| `/inzpireu-coguru:book-public-session` | Public mentors → slots → checkout |

## This is not

- A Fastify plugin inside `inzpireu-server`
- Claude.ai Connectors Directory listing (searchable like Gmail/Drive)

Those use the same `/mcp` URL. This package is the Claude Code installable wrapper.

## License

ISC
