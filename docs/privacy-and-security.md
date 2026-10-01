# Privacy and security

## Your keys

- Stored encrypted in VS Code's Secret Storage: Windows Credential Manager, macOS Keychain or Linux Secret Service.
- Never uploaded to Codeloft or anyone else. Each key is sent only to the provider it belongs to, when you run a task.
- Never shown again after you save them.

## Your code and prompts

- **With your own keys**, sent only to the providers whose keys you add, directly from your editor. Their terms apply. Some free tiers may use requests to improve their models, so check a provider's data policy before working on sensitive code.
- **On the free trial**, before you add a key, requests go through FreeAgentCoder's server to a provider on the project's keys. They are passed through and not stored; only daily counts are kept, against a random id made for the trial alone. Turn the trial off with the `freeagentcoder.freeTrial` setting.
- Documents and the text in screenshots are read on your computer. The image reader is downloaded once, about 6 MB, from a public CDN and checked against a fixed checksum before it runs. Your image is never part of that download.
- Attachments are saved in your project's `.freeagentcoder/` folder, which is git-ignored automatically.
- Chat history is saved only if you agree, and only on your computer.
- Lessons from your corrections stay on your computer. **Settings → Memory** lists and deletes them.

## What is collected

**Nothing, unless you say yes.** After a few tasks the extension asks, once, whether it may send anonymous counts:

- how many keys you have, and which providers;
- how many tasks ran and how they ended;
- short causes for failures, such as `gemini:daily-limit`.

Never your code, prompts, file or project names, keys, or anything identifying you or your machine. The question is never asked if you have turned telemetry off in VS Code. **Free Agent Coder: Anonymous Usage Data** shows the exact text that would be sent, and lets you stop at any time.

## What the extension downloads

- **Specialist instructions,** once a day: how each kind of work is approached. A plain download that sends nothing about you. Turn it off with the `freeagentcoder.specialistUpdates` setting.
- **The Plans page** asks the website whether a paid tier exists, only when you open it.

## Safe by default

- Risky commands such as deleting files, `git push` or deploys always ask first, in every mode.
- Commands that could wipe a disk are always refused.
- Every task that changed files can be undone from the chat.
- **Copy diagnostics** in Settings → Logs removes API keys, tokens and your username from paths before copying, so a bug report is safe to share.

## Reporting a security problem

Please do not open a public issue. Open a [private security advisory](https://github.com/Prateek22672/FreeAgentCoder-Codeloft/security/advisories/new) instead.
