---
name: simplevox-activity
description: Report SimpleVox call and text activity over a period - totals, answered, missed, voicemail, texts sent - compared with the period before, using SimpleVox's own counts. Use for "how many calls did we miss last week", "call volume this month", "how did we do", "busiest day", "weekly report". Read-only; never estimates numbers SimpleVox didn't return.
---

# SimpleVox activity

## Goal

Answer "how are we doing on the phones" with SimpleVox's own counts and definitions, compared with the previous period, without inventing anything.

## When to use

- "How many calls did we miss last week?"
- "Give me a report for October."
- "Which day is busiest?" or "Which number gets the most calls?"

## Workflow

Follow [the SimpleVox activity report steps](references/activity-report-steps.md). They are the same steps the server's activity_report prompt uses.

- count_history covers at most 31 days per call. For a longer range, say so and report it in parts.
- Group by day, line, direction or outcome to match the question.
- Compare with the previous period of the same length by calling count_history again.

## Output

- **Headline:** the number they asked about, with the change from the previous period.
- **Breakdown:** a small table by day, line or outcome.
- **Caveats:** small numbers, partial periods and definitions that matter. Sent isn't delivered.
- **Next step:** offer to list the missed calls behind the numbers (simplevox-catch-up or simplevox-follow-ups).

## Rules

- Use only what count_history returns, and quote its definitions when they matter. Never estimate revenue, conversion or anything SimpleVox doesn't measure.
- Don't read a trend into a handful of calls.
- Answered means a verified connection, not just that someone picked up.
