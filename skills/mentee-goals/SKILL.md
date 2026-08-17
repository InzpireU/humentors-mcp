---
name: mentee-goals
description: Help a Humentors mentee list inviteable goals, find mentors, and send a goal invite. Use when the user wants goals, mentor matching, or inviting a mentor.
---

# Mentee goals and invites

Requires a connected Humentors MCP session and **MENTEE** persona. Always call tools again; do not reuse earlier results after the user changes data in the app.

## Flow

1. Call `whoami` again (never reuse an earlier whoami).
   - If not authenticated, use `/humentors-coguru:connect-humentors`.
   - If the user is not MENTEE, stop and explain. Do not call mentee-only tools.
2. Call `list_mentee_goals` again (optional `orgRef` from this `whoami` JSON). Do not reuse earlier goals.
   - Present only title, type, status, description.
   - ACTIVE = self-paced; INITIATED = normal.
   - Keep `goalRef` / `programRef` / `orgRef` internal. Never print refs or UUIDs.
3. Call `list_mentors_for_goal` with `searchTerm` from the goal title/keywords.
   - Present only mentor name, service, category, tagline.
   - Keep `mentorRef` / `serviceRef` internal.
4. After the user picks a mentor/service, call `send_goal_invite` with `goalRef`, `mentorRef`, `serviceRef`.
   - Default `menteeStatus=INVITED`, `isConfirmed=true`.
   - Confirm success in plain language. Do not dump raw API JSON or IDs.

## Rules

- Never invent refs. Only reuse refs from the **latest** tool JSON in this turn.
- Never show emails, phones, passwords, or raw IDs.
