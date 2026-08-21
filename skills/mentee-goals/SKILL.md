---
name: mentee-goals
description: Help a Humentors mentee review goals and mentorship invitation statuses, find mentors, and send a goal invite.
---

# Mentee goals and invites

Requires a connected Humentors MCP session and **MENTEE** or **MENTEE_AND_MENTOR** persona. Always call tools again; do not reuse earlier results after the user changes data in the app.

## Flow

1. Call `whoami` again for the **currently connected** account (never reuse an earlier whoami).
   - If not authenticated, use `/humentors-coguru:connect-humentors`.
   - If the user is neither MENTEE nor MENTEE_AND_MENTOR, stop and explain. Do not call mentee-only tools.
2. Call `list_mentee_goals` again using only refs from this `whoami`. Do not reuse goals from a previous account or earlier turn.
   - Use `goalView=active` by default. Use `goalView=archived` only when the user asks for archived goals.
   - Use `goalView=all` only when the user explicitly asks for both active and archived goals.
   - Mention whether each goal's type is Self-paced or Normal.
   - Present goals in user-friendly sections: Self-paced, Normal, Invite sent, Mentor accepted, and Archived when requested.
   - Do not show raw goal status values.
   - If invitations exist, show the mentor name and say Accepted, Awaiting response, or Not accepted.
   - Keep `goalRef` / `programRef` / `orgRef` internal. Never print refs or UUIDs.
3. Call `list_mentors_for_goal` with `searchTerm` from the goal title/keywords.
   - Pass the goal's `programRef` when present.
   - Present only mentor name, service, category, tagline.
   - Keep `mentorRef` / `serviceRef` internal.
4. After the user picks a mentor/service, call `send_goal_invite` with `goalRef`, `mentorRef`, `serviceRef`.
   - Only invite when the latest goal result has `canInviteMentor=true`.
   - Default `menteeStatus=INVITED`, `isConfirmed=true`.
   - Pass `selfIntroduction` when the user provides an optional introduction.
   - Confirm success in plain language. Do not dump raw API JSON or IDs.

## Rules

- Never invent refs. Only reuse refs from the **latest** tool JSON in this turn.
- Pass the current ISO timestamp as `asOf` on every tool call.
- Never show emails, phones, passwords, or raw IDs.
