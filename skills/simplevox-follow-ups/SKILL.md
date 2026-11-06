---
name: simplevox-follow-ups
description: Find SimpleVox missed calls and voicemails nobody has answered, work out what each caller wanted, draft one reply per caller, and send only the drafts the person approves. Use for "who needs a call back", "follow up on missed calls", "go through the voicemails", "draft replies to everyone who called", "clear the voicemail inbox". Drafts are always shown first.
---

# SimpleVox follow-ups

## Goal

Turn the missed calls and voicemails nobody has answered into a short list of replies the person can approve, then send exactly what they approved and mark the handled conversations done.

## When to use

- "Who still needs a call back?"
- "Go through yesterday's voicemails and draft replies."
- "Follow up with everyone who called while we were closed."

## Workflow

Follow [the SimpleVox follow-up steps](references/follow-ups-steps.md) in order. They are the same steps the server's follow_ups prompt uses. Before sending, read the [texting guide](references/texting.md). Before marking anything, read the [inbox guide](references/inbox.md).

## Deciding what each caller needs

- **The caller's own words drive the reply.** Answer what they asked about. Never guess what someone wanted from context alone.
- **Put the urgent ones first:** a deadline today, safety or emergency words, a cancellation, a billing dispute, or someone who called several times.
- **Respect the channel they asked for.** If they asked for a call back, draft a short text saying the person will call, and offer to set up the call with simplevox-call.
- **Already handled is handled.** `unresponded` already leaves out callers who got a connected callback or a text from a person. Don't draft for them.
- **Leave out** the business's own numbers, robocalls and sales pitches. Say how many you left out.
- **Use the contact record's name**, or no name. Never use a name heard in the voicemail.

## Approval and sending

- Show every draft with its recipient, the line it goes from and the exact text, as a numbered list.
- Send only the drafts the person approves, one send_text call per approved text, each with user_confirmed set to true and its own idempotency_key.
- If the person edits a draft, show the final text again before sending it.
- Outside about 8 am to 9 pm in the recipient's local time, suggest waiting unless the person says it's urgent.
- Report what was sent, the state SimpleVox returned for each, and anything that failed.

## Afterwards

Once the person has dealt with a conversation, offer to mark it done with mark_conversations, passing the `revision` and `activity_through` from the history you showed. Mark only conversations they confirm.
