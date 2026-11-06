---
name: simplevox-find-and-quote
description: Find what a customer said in SimpleVox calls, voicemail or texts and quote it exactly with a link to the source. Use for "what did Mary say about", "find the text about Thursday", "did anyone mention a gate code", "summarize our calls with this customer", "play that voicemail", "what happened with this caller". Read-only.
---

# SimpleVox find and quote

## Goal

Answer "what was said" with the exact words and a link to the original call, transcript passage or text, so the person can check it.

## When to use

- "What did Mary say about the estimate?"
- "Find the text about Thursday's appointment."
- "Did anyone mention a gate code in the last two weeks?"
- "What's the history with this customer?"
- "Let me listen to that voicemail."

## Workflow

1. **Know the person.** If they name a customer, find them with search_contacts. Ask when more than one contact matches.
2. **Search or browse.**
   - For a word or phrase, use search_history with `q`, optionally narrowed with `contact_id`. Search finds the exact word or phrase (ignoring case), not similar meanings. It covers up to 31 days at a time, and the last 31 days by default.
   - For a customer's history, use list_history with `contact_id`.
3. **Open what matters** with get_history_items: up to 20 at a time, with summaries and recordings. Ask for `transcript` only when you need it, because transcripts are long.
4. **Quote exactly.** For a call, pass the `recording_id`, `transcript_version` and `segment_indices` from the search hit to get_call_transcript, and quote those segments word for word.
5. **Play it** only when the person wants to listen: get_playback_link gives a private link that expires within an hour. Give it to them, and don't save it.

## Search tips

- Start with one distinctive word: "gate", not "gate code for the back".
- If nothing matches, try another word the customer might have used, or a longer window, and say what you tried.
- Search results can change as transcripts are corrected. Search again rather than trusting an old result.

## Output

- The answer first, in one or two lines.
- Then the quote, word for word, with who said it, when, and the source link.
- If a summary and the transcript disagree, trust the transcript and say so.
- A recording or transcript that's pending, failed or deleted isn't evidence of what was said. Say it's unavailable.

See the [inbox guide](references/inbox.md) for citations and coverage.
