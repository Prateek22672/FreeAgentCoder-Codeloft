# Getting started

Five minutes from nothing to a working agent.

## 1. Install

Search for **Free Agent Coder** in the VS Code Extensions view and click Install. A **Get started** guide opens by itself. Free Agent Coder lives in the **right side bar**, next to your code. Open it any time with **Free Agent Coder: Open Chat** from the Command Palette (`Ctrl+Shift+P`).

You need VS Code 1.137 or newer and a project folder open.

## 2. Try it, then add a free key

With no key yet, your first tasks run on the **free trial**: a daily allowance on the project's keys, enough for two or three real tasks. When you want more, open **Settings → API Keys** in the panel. Each provider has a direct link. None of these asks for a card:

| Provider | Get a key | Good for |
| --- | --- | --- |
| Google Gemini | [aistudio.google.com/apikey](https://aistudio.google.com/apikey) | Big projects and complex builds: a 1M-token context |
| Groq | [console.groq.com/keys](https://console.groq.com/keys) | Very fast answers and small edits |
| Mistral | [console.mistral.ai/api-keys](https://console.mistral.ai/api-keys) | A solid all-rounder; needs a phone number |
| OpenRouter | [openrouter.ai/keys](https://openrouter.ai/keys) | Free models from several makers behind one key |
| Cohere | [dashboard.cohere.com/api-keys](https://dashboard.cohere.com/api-keys) | A last backup: 1,000 calls a month, personal use only |

Paste the key. The extension recognises most providers from the key itself. Keys are stored encrypted in VS Code's Secret Storage on your computer.

**The best setup is one key from each provider.** A second key from the same account shares that account's limits, so it adds nothing. Provider terms do not allow making extra accounts to get around limits.

You can also add a paid OpenAI or Anthropic key. Paid keys are used only when no free key can answer, so there are no surprise bills.

## 3. Ask

Describe what you want in plain words, for example:

- *Explain how this project is structured and how to run it.*
- *Add a dark mode toggle to the settings page.*
- *The checkout test fails. Find out why and fix it.*

Or click **Test my project**. It runs your project's own checks (type check, lint, tests, build) and explains every failure with a fix, changing nothing.

## 4. Choose how much it may do

| Mode | Does without asking |
| --- | --- |
| Manual | Reads files |
| Auto-edit (default) | Reads and edits files |
| Auto | Reads and edits files, runs commands |

Risky commands such as deleting files, `git push` or deploys always ask first. Commands that could wipe a disk are always blocked. Any task that changed files can be undone from the chat.

## Useful commands

- **Free Agent Coder: Open Chat**
- **Free Agent Coder: New Chat**
- **Free Agent Coder: Manage API Keys**
- **Free Agent Coder: Show Usage**
- **Free Agent Coder: Test My Project**
- **Free Agent Coder: Stop Current Task**

In the chat box, **Enter** sends, **Shift+Enter** adds a line, **Esc** stops the task, and **↑** brings back your last prompt.

## Teach it your conventions

It follows `AGENTS.md`, `CLAUDE.md`, `.github/copilot-instructions.md` or `.cursorrules` if your project has one. After you correct it, it saves a short lesson and follows it next time. Type *remember that …* to teach it directly. **Settings → Memory** lists and deletes lessons.
