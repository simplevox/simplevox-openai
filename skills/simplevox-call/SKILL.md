---
name: simplevox-call
description: Place a SimpleVox call for the person - SimpleVox rings their own phone or browser first, says who it is calling when they answer, then dials the customer from the business number - and check on it or hang up. Use for "call Mary", "call them back", "set up a call with", "ring my phone and connect me to", "hang up", "is the call connected". No AI is on the call; it needs an explicit yes first.
---

# SimpleVox calls

## Goal

Place a call between the person and a customer from their business number, after they approve who, from which line and which of their devices rings. Then report honestly whether it connected. Read the [calling guide](references/calling.md) first: it's the same guide the server publishes.

## How the call works

1. SimpleVox rings one of the person's devices: the SimpleVox browser phone, or the SimpleVox mobile app. It shows as a call to the customer, not from them.
2. When the person answers, they hear who is being called and their private note, if any.
3. SimpleVox dials the customer from the business number. The person hears it ring, and they're connected when the customer picks up, or reach the customer's voicemail.

Nobody presses 1, and the customer hears the person, not a recording.

## When to use

- "Call Mary back."
- "Call the customer from this morning's voicemail, and ring my phone."
- "Is the call connected?" or "Hang up."

## Workflow

1. **Check readiness.** get_my_account must list at least one entry in `calling_devices` and show `start_call.available` on the line. If no device is listed, tell the person to turn on the browser phone in SimpleVox, or open the SimpleVox mobile app with calls allowed.
2. **Find the recipient** with search_contacts, or use the number the person gave, as E.164. Ask when more than one person matches.
3. **Confirm** the recipient's name and number, the line, and which device will ring: the one marked `default` unless the person asks for another. Offer a short private note (`purpose`) that only they hear.
4. **Start** with start_call: a new idempotency_key, the confirmed details, `user_endpoint_id` only if the person picked a device other than the default, and user_confirmed set to true.
5. **Watch it.** Check get_call_status about every 5 seconds until `setup_state` is terminal or `connection_state` is verified. Setup ends within 90 seconds.
6. **Report:** connected only when `connection_state` is verified, which can be the customer's voicemail. Otherwise say what happened from `outcome`, for example the line was busy or the person didn't answer their phone.

## Ending a call

- end_call cancels setup or hangs up. If it returns `connection_observed`, check get_call_status and call end_call again.
- Until `cleanup` is confirmed, say the hang-up was requested, not that the call ended.
- Closing the chat doesn't cancel a call.

## Rules

- Never dial without an explicit yes in this conversation.
- After a timeout, retry with the same idempotency_key and unchanged details. Never dial again with a new key.
- The line's recording setting applies to these calls. If it's on and the person asks, tell them the call will be recorded.
