---
name: simplevox-setup
description: Explain the person's SimpleVox setup - their numbers, timezone, what this connection may do, missing setup steps, business hours and call routing - and what to do next. Use for "what's my number", "why can't I send texts", "what can SimpleVox do here", "are we open right now", "what happens when someone calls after hours", "who gets the call". Read-only; changes happen in the SimpleVox app.
---

# SimpleVox setup, hours and routing

## Goal

Tell the person where their SimpleVox setup stands and what happens when someone calls, then point them to the exact next step.

## When to use

- "What's my business number?" or "What time zone is SimpleVox using?"
- "Why can't I send texts yet?" or "I just signed up. What now?"
- "What can you do in SimpleVox?"
- "Are we open right now?" or "What happens when someone calls after hours?"

## Setup and permissions

Call get_my_account.

- `setup.next_step` is the single most useful next step, with a link. Tell the person what it is before anything it blocks.
- `setup.line_status` is `active`, `not_provisioned` (number setup isn't finished) or `no_plan` (no plan yet).
- `setup.outbound_texting` says whether customer texting is ready. Texting needs an approved carrier registration with the number attached; receiving texts doesn't. Registration and billing are handled in the SimpleVox app, never through the assistant.
- Each line's `send_text` and `start_call` say whether this connection can text or call from it. `connection.missing` lists what the connection can't do, the tools that would add, and whether the person can turn it on by reconnecting (`reconnect`) or needs an admin first (`ask_admin`).
- Never mention plan prices, invoices or payment details. SimpleVox doesn't share them here.

## Hours and call routing

Call get_line_settings for every line, or just one.

- `open_now` and `business_hours` (per day, in the business timezone) say whether the line is open. Hours only change routing when `hours_affect_routing` is true.
- `routing` is the list of steps a call follows, starting at the first. `open`, `closed` and `next` name the step that comes after. Describe it in plain words, for example: "Weekdays 9 to 5, it rings Alex and Sam together for 20 seconds, then goes to voicemail. When you're closed, it goes straight to voicemail."
- `voicemail_greeting` is what callers hear before leaving a message.
- The assistant can't change any of this. Point the person to `manage_url`. `can_manage` says whether they can change it themselves or need a line owner or admin.

See the [inbox guide](references/inbox.md) for line settings and statuses.
