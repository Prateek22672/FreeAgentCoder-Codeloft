# Why it is efficient

Free tiers are small. Some cap a single request at about 6,500 tokens, and most count requests per day. A coding agent that wastes requests stops halfway through a task, so Free Agent Coder is built to do more with fewer, smaller calls.

## No model at all, for chores

**Fyx**, the built-in task engine, does everyday jobs without an AI model: zipping and unzipping, git (status, pull, push, commit with your message, branches, clone, fork), installing packages, running your project's scripts, and creating, moving or copying files. It plans the exact commands for your platform and shell and runs them through the same permission prompts. One measured request, zipping a project folder, took an AI model 4 minutes 36 seconds and 17,000 tokens; Fyx took 0.2 seconds and none. It learns: a short request the agent finishes with a single command is done by Fyx the next time.

## Fewer requests

- **Tasks are sized before they start.** A quick question gets a short, cheap path. Only builds, debugging and multi-file work get the full treatment.
- **Finding the right files costs nothing.** A local search index of your project, built from file names and identifiers, picks the files most likely to matter. Deep tasks start with them already listed, instead of spending requests exploring.
- **A map of your folders** is given at the start of a complex chat, so changes land in the right place first time.
- **No wasted retries on daily limits.** A key that hits its daily limit is set aside straight away, rather than retried every few seconds.
- **Attachments are read once, locally.** Documents and screenshot text are read on your computer before the task, not by a model on every call.

## Smaller requests

- **Compact instructions.** The standing instructions are short on purpose, because they are resent with every model call.
- **Two-stage compaction.** When a conversation grows past 70% of the limit, old tool output and bulky arguments are blanked out, with no model call. Only past the limit does a model summarise the older part, keeping the recent part word for word.
- **Learnt size limits.** When a provider rejects a request as too large, the router remembers that model's real limit and sends bigger requests elsewhere.

## The right model for each step

- **Fast models for fast work.** Small edits and questions go to Groq, which answers in a second or two.
- **Big context for big work.** Long, multi-file tasks go to Gemini and its 1M-token context.
- **Keys spread evenly.** The key used least today goes first.

## Knowing before it runs out

Before a task starts, it estimates how many requests the task will need, from your own history after a few tasks:

```
expected requests = your average for this size of task (else 3 fast, 12 deep)
                    × 1.5 for a build or a test run
                    + 2   with attachments
                    × 0.8 for a correction
```

That is compared with what your keys report is left today. Too little, and a warning card appears before the work begins, with a button to add a key.

## What you save

**Settings → Overview** prices the tokens your free keys used against a typical paid coding model, at $3 per million tokens in and $15 per million out. Paid keys are left out, because that money was really spent. The basis is shown next to the number, so it reads as the estimate it is.
