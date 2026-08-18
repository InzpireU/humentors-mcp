# Humentors for Claude

Connect Claude to your Humentors account so you can check your role, work with mentee goals, invite mentors, and book public mentor sessions.

## Claude.ai

1. Open **Settings** → **Connectors**.
2. Add a custom connector.
3. Paste this URL:

   `https://staging-server.humentors.org/connector`

4. Click **Connect** and sign in to Humentors.
5. Approve access, then return to Claude.

You can disconnect anytime from the same Connectors page.

## Claude Code

1. Install this plugin, or point Claude Code at this folder.
2. Run `/mcp` and select **humentors**.
3. Complete the browser login and allow access.

After you are connected:

- `/humentors-coguru:connect-humentors` — confirm you are signed in
- `/humentors-coguru:mentee-goals` — list goals, find mentors, send an invite
- `/humentors-coguru:book-public-session` — browse public mentors and book a session

If Claude says you are not connected, run `/mcp` and connect **humentors** again.
