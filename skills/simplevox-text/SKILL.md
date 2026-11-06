---
name: simplevox-text
description: Draft or send a text from the person's SimpleVox business number, with the recipient, line and exact text confirmed first. Use for "text Mary", "send a text to", "reply to that text", "let the customer know", "draft a text". Drafting never sends; sending needs an explicit yes.
---

# SimpleVox texting

## Goal

Send one text the person approved, from a number they're allowed to text from, to exactly the person they meant, and report honestly what happened. Read the [texting guide](references/texting.md) first: it's the same guide the server publishes.

## When to use

- "Text Mary that I'll be there at 10."
- "Reply to Sam's text and say Thursday works."
- "Draft a text to everyone who called about the leak." Draft only.

## Workflow

1. **Draft or send?** "Draft", "write" or "suggest" means show the text and stop. Only "send", "text them" or a clear yes moves on to sending.
2. **Find the recipient.** Use search_contacts for a name, and ask when more than one person matches. Use a number the person gave as E.164, such as +12025550123. Never guess a number.
3. **Choose the line.** get_my_account lists each line and whether it can send texts (`send_text.available` and `reason`).
   - If exactly one line can text, use it.
   - If several can, ask which one. Offer them as choices if your app supports that, otherwise as a short numbered list.
   - If none can, explain why from `setup.outbound_texting` or the line's `reason`, and stop.
4. **Write it.** Keep the person's meaning and tone. Don't add a signature or anything they didn't ask for. Texts are text only.
5. **Confirm.** Show the recipient's name and number, the line and the exact text. Wait for an explicit yes.
6. **Send** with send_text: a new idempotency_key, the confirmed `to`, `from` and `body`, and user_confirmed set to true.
7. **Report** who it went to, from which line, and the state SimpleVox returned. Sent isn't delivered.

## Several recipients

Write one text per person and list every recipient and text. Send only the ones the person approves, one call each. Never send to a group on a single vague approval.

## If something goes wrong

- If the recipient replied STOP, SimpleVox refuses the text. Suggest a call instead.
- After a timeout, retry with the same idempotency_key and unchanged text. Don't send again with a new key.
- If the text failed or was undelivered, say so, and offer a call.
