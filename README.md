# Humentors for Claude

Connect Claude to your Humentors account so you can check your role, work with mentee goals, invite mentors, and book public mentor sessions.

## Claude.ai

1. Open **Settings** → **Connectors**.
2. Add a custom connector.
3. Paste this URL:

   `https://ai-stg.humentors.org/connector`

4. Click **Connect** and sign in to Humentors.
5. Approve access, then return to Claude.

All Humentors tools require this connected account. You can disconnect anytime from the same Connectors page.

## Claude Code

1. Install this plugin, or point Claude Code at this folder.
2. Run `/mcp` and select **Humentors**.
3. Complete the browser login and allow access.

After you are connected:

- `/humentors-coguru:connect-humentors` — confirm you are signed in
- `/humentors-coguru:mentee-goals` — list goals, find mentors, send an invite
- `/humentors-coguru:book-public-session` — browse public mentors and book a session

Humentors data is fetched again for each request, so changes made in the app appear in the next tool result. After connecting or reconnecting, run `/humentors-coguru:connect-humentors` to verify the current account before using goals or booking.

If Claude says you are not connected, run `/mcp`, connect **Humentors** again, and verify the account.
