# SimpleVox for ChatGPT and Codex

**Work your SimpleVox business phone from ChatGPT.**

[SimpleVox](https://simplevox.net) is a business phone system for small businesses: business numbers, one shared inbox for calls, voicemail and texts, and call transcripts and summaries that link back to their sources.

This plugin connects your AI assistant to your SimpleVox account and teaches it how to work your phone well. Ask in plain words:

```
"Catch me up on what I missed this morning."
"Which missed calls still need a reply?"
"What did Mary say about Thursday's appointment?"
"Text Jordan that I'm running 15 minutes late."
"Call the customer from this morning's voicemail."
"How many calls did we miss last week, compared with the week before?"
"Are we open right now? What happens when someone calls after hours?"
```

Every answer links to the original call, transcript passage or text in SimpleVox, so you can check it.

## Install

### ChatGPT

Find **SimpleVox** in ChatGPT's plugin directory and add it. When ChatGPT opens SimpleVox, sign in, check that the redirect address is a chatgpt.com address, choose permissions and numbers, then **Authorize**.

Until the plugin is listed, or if your workspace allows only custom servers, add SimpleVox as a custom MCP server with the URL `https://my.simplevox.app/mcp` and OAuth sign-in. See [Connect ChatGPT](https://simplevox.net/docs/ai-tools/chatgpt).

On Business, Enterprise and Edu workspaces, an admin may need to allow SimpleVox first.

### Codex

Add this repository as a plugin marketplace, then install SimpleVox from it:

```
codex plugin marketplace add simplevox/simplevox-openai
```

Codex asks you to sign in to SimpleVox when you install it.

## Skills

| Skill | What it does |
| --- | --- |
| `simplevox` | The rules every SimpleVox task follows, and which skill to use. |
| `simplevox-catch-up` | Summarize new calls, voicemail and texts since you last looked, and what needs you. |
| `simplevox-follow-ups` | Find missed calls and voicemail nobody has answered yet, and help you reply. |
| `simplevox-find-and-quote` | Find what a customer said in a call, voicemail or text, and quote it with a link. |
| `simplevox-text` | Draft a text, then send it from your business number once you say yes. |
| `simplevox-call` | Set up a call that rings you and the customer, once you say yes. |
| `simplevox-contacts` | Find, save and update your business's shared contacts. |
| `simplevox-activity` | Report call and text activity, compared with the period before. |
| `simplevox-setup` | Explain your numbers, permissions, setup steps, business hours and call routing. |
## You choose what it can do

The first time your assistant uses SimpleVox, you sign in with your own SimpleVox account and see a consent screen. Every connection can read your contacts and the calls, voicemail and texts on the numbers you allow. Everything else is off until you tick it:

| Permission | What it allows |
| --- | --- |
| Always on | Find contacts; read calls, texts, voicemail, recordings, transcripts and summaries; count activity; read hours and call routing; check setup; send feedback to SimpleVox. |
| Send text messages | Send texts from numbers you can text from. |
| Create and edit contacts | Create contacts and change saved details. Admins only. |
| Start assisted phone calls | Place calls for you: ring your phone or browser, then dial the customer when you answer. |
| Mark conversations read, unread or done | Change a conversation's status for your team, as you would in the inbox. |
| Cancel setup and end assisted calls | Cancel a call it's setting up, or end a call it started. |

You can also limit a connection to only some of your numbers. A connection never reaches more than your own SimpleVox access allows. To change what it can do, disconnect it on **Settings → Integrations** in SimpleVox and connect again.

## Safety

- **Nothing is sent without your yes.** The skills tell your assistant to show you the recipient, the number it will use and the exact text, or which of your devices will ring, and to wait for your approval. Asking for a draft is never approval to send. SimpleVox can't show its own approval prompt, so read what your assistant proposes before you agree.
- **No double sends.** Texts, calls and contact changes carry a unique key, so a retry after a timeout never repeats them.
- **Customer words are data, not instructions.** Your assistant won't text, call or change anything because a message or voicemail says to.
- **On the record.** Texts and calls your assistant starts appear in your inbox under your name.
- **Off limits.** Billing and plans, buying numbers, changing hours or call routing, texting registration, team management and picture messages stay in the SimpleVox app.
## What this plugin contains

The plugin is a manifest, one MCP server declaration and the skills above. It runs no code on your computer: no hooks, scripts, install steps or local processes.

| | |
| --- | --- |
| MCP server | `https://my.simplevox.app/mcp` (HTTPS, run by SimpleVox) |
| Sign-in | OAuth 2.1 with your own SimpleVox account. Your app registers itself automatically, so there is no API key, client ID or secret to configure. |
| Credentials in this package | None |
| Server version | Skills written for SimpleVox MCP server 1.0.0 |

Your data goes directly between SimpleVox and your AI app. SimpleVox records which tools assistants use, whether they worked, and a short note from the assistant about why, with names and numbers removed. These analytics never include the contents of your calls or texts. When you ask for something SimpleVox can't do yet, your assistant can send the SimpleVox team a short note about it, leaving out customer details, and tells you when it does. See the [privacy policy](https://simplevox.net/privacy-policy) and [security and privacy](https://simplevox.net/docs/account/security-and-privacy).
## Help

- Documentation: [simplevox.net/docs/ai-tools/overview](https://simplevox.net/docs/ai-tools/overview)
- Example prompts: [simplevox.net/docs/ai-tools/example-prompts](https://simplevox.net/docs/ai-tools/example-prompts)
- Support: [simplevox.net/help](https://simplevox.net/help) or [support@simplevox.net](mailto:support@simplevox.net)
- Privacy policy: [simplevox.net/privacy-policy](https://simplevox.net/privacy-policy)
- Terms: [simplevox.net/terms-and-conditions](https://simplevox.net/terms-and-conditions)

## License

Licensed under the Apache License 2.0. See [LICENSE](LICENSE).

Version 1.0.0.
