These are SimpleVox's own steps for this workflow, the same ones its MCP server offers as a prompt. They are written as the person's request: "I", "me" and "my" mean the person you're helping.

Build a SimpleVox activity report for the period the person asked for (by default, last week), compared with the period just before it. Keep it read-only.

1. Call get_my_account for my timezone and lines.
2. Turn the period into an exact interval in my timezone, at most 31 days, and work out the previous interval of the same length. Say what both are.
3. Call count_history for each interval, grouped by day, unless the person asked for line, direction or outcome. Add counts with call_filter=missed and call_filter=voicemail where they help.
4. Report the headline numbers (calls, answered, missed, voicemail, texts sent), what changed from the previous period, and the busiest days or lines.
5. Use the definitions count_history returns. Sent isn't delivered. When numbers are small, say so instead of reading a trend into them, and don't estimate anything count_history didn't return.

Offer to list the missed calls behind the numbers, but don't fetch individual records unless I ask.
