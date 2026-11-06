# Assisted calls with SimpleVox

start_call places a call for the person. SimpleVox rings their own device first. When they answer, it says who it is calling, then dials the customer from the business line. The customer hears the person, as on any call from that number. Nobody presses 1, and no AI is on the call.

## Before calling

- get_my_account must list a calling device under calling_devices and show start_call.available on the line. A calling device is a browser with the SimpleVox browser phone on, or the SimpleVox phone app with calls allowed. If none is listed, tell the person to turn one on.
- One device rings: the one marked default unless the person picks another. Confirm the recipient's name and number, the line, and which device will ring. Then call start_call with user_confirmed set to true.
- purpose is a private note SimpleVox reads to the person when they answer. The customer never hears it, so never put anything meant for the customer there.

## While it connects

- Check get_call_status about every 5 seconds until setup_state is terminal or connection_state is verified. The person's device rings for up to 20 seconds, the customer's phone for up to 30 seconds, and setup ends within 90 seconds.
- connection_state verified means the customer's line answered and the two calls are joined. That can be the customer's voicemail; the person hears which and can leave a message.
- If the customer isn't reached, SimpleVox tells the person why on their call, for example that the line was busy. Report the outcome from get_call_status.
- Closing the chat doesn't cancel a call.
- The line's recording setting applies to assisted calls.

## Ending

- end_call cancels setup or hangs up. It returns action cancel_setup, end_call, already_ended or connection_observed. For connection_observed, check get_call_status and call end_call again.
- cleanup stays pending until both sides are confirmed ended. Say so rather than claiming the call ended.

## Retries

- After a timeout, retry start_call with the same idempotency_key and unchanged details. Never dial again with a new key when you aren't sure the first call started.
