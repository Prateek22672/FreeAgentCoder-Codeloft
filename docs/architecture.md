# How it works

How a message in the chat panel becomes checked, working code.

```
 your message
     │
     ▼
 ┌──────────────────────────────────────────────────────┐
 │ Plan the turn                                        │
 │  what kind of task · which specialist · fast or deep │
 │  project checks · relevant files · lessons           │
 │  model chain · will it fit today's limits?           │
 └──────────────────────────────────────────────────────┘
     │
     ▼
 ┌──────────────────────────────────────────────────────┐
 │ The agent loop                                       │
 │  model call → tool calls → results → repeat          │
 │  permissions · context compaction · completion check │
 └──────────────────────────────────────────────────────┘
     │            ▲
     ▼            │ every model call goes through
 ┌──────────────────────────────────────────────────────┐
 │ The router: your keys, in order, with failover       │
 └──────────────────────────────────────────────────────┘
     │
     ▼
 checked result in the panel
```

It is built in two halves. **The engine** runs the agent loop, the tools and the router, and knows nothing about VS Code. **The extension** decides what kind of task this is, builds the prompt, picks the models and shows everything in the panel.

## One turn, end to end

1. **The request arrives.** The extension checks that a folder is open and a key can be used.
2. **The task is sized.** A quick question or a one-line fix is *fast*. Builds, debugging, corrections, tests and anything with an attachment are *deep*. Deep tasks get more of everything below.
3. **A specialist is chosen.** Each kind of work has its own method and its own finish line (see below).
4. **The model chain is built** from your keys for that size of task.
5. **The project's own checks are found**: your type check, lint, tests and build.
6. **The prompt is assembled**: the specialist's method, a map of your folders, lessons from earlier corrections, and the files most likely to matter.
7. **Today's limits are forecast.** If your keys look too small for the task, a warning appears before work starts.
8. **The agent loop runs** until the model stops calling tools.
9. **The completion check** can send it back to work.
10. **The turn is recorded**: usage, key health, and a lesson if you corrected it.

## Specialists

Before a task starts, the extension works out what kind of work it is and follows the method that suits it.

| Specialist | Method | Finish line |
| --- | --- | --- |
| Debugging | Reproduce the problem first, then fix it | A test that failed now passes |
| Refactoring | Run the tests before and after | Behaviour unchanged |
| Interface design | Match the project's existing components | Checked at phone width |
| Data and ML | Fixed seeds, held-out data, a baseline | A small smoke run, never a full training run |
| Building | End to end, nothing faked | The project's checks pass |
| Explaining | Answer from the code | Nothing changed |

Specialists are improved without a new release: once a day the extension downloads updated instructions. It is a plain download that sends nothing about you, and a setting turns it off.

## The agent loop

Each step is a model call. If the model asks for tools, they run, their results go back, and the next step starts.

| Tool | Purpose |
| --- | --- |
| Read, write and edit files | With a read-before-write rule, and checkpoints for undo |
| Find files and code | File patterns, text search, folder listings |
| Ranked code search | A local index of the project, no API quota used |
| Run commands | Including background jobs such as dev servers |
| Fetch a URL | Read documentation |
| Inspect the environment | See which SDKs exist before building |
| Plan | The live to-do list shown in the panel |

Guard rails: at most 80 model calls per turn, a nudge when the model announces an action without doing it, a stop when it repeats the same call three times, and very long tool output trimmed in the middle.

## Proving the work

> If a complex task changed code, it may not finish until one of the project's checks has passed **after its last edit**.

The extension reads your project and finds its real check commands, using its own package manager and virtualenv: npm, pnpm or yarn scripts, `pytest`, `ruff`, `mypy`, `flutter analyze`, `cargo`, `go test`, `dotnet`, Maven or Gradle. Edits and commands are numbered within the turn, so "after the last edit" is exact. A check that failed is reported back to the model with its output. A reply that plainly explains why no check can run is accepted, so it never loops forever.

## When something fails

| Layer | Handles | What happens |
| --- | --- | --- |
| Router | One model rate-limited or offline | It cools down and the next model takes over, invisibly |
| Router | Rate limit with nothing else to try | It waits in place when the wait is short |
| Loop | A request too large for every model | The conversation is compacted and the request retried |
| Turn | Everything failed at once | It waits 30 seconds, then 90, and resumes the task |
| Turn | A daily limit reached | That key is set aside until it resets; no pointless waiting |
| Panel | Nothing left to try | A plain explanation and the next step, with details folded away |

## Attachments

Screenshots, PDFs, Word, PowerPoint, Excel and long text are read before the task starts, so every model works from the same details even if it cannot see images. Documents and the text in screenshots are read on your computer. A vision model is used only when an image has little text, or when its layout and colours are what matter. Very long documents are summarised, with the full text saved in a git-ignored folder for the agent to read.

## Memory

After a correction, a fast model turns what you said into short, general lessons, such as *Use Riverpod for state, not setState*. Lessons are stored on your computer, cleaned of secrets, and the most relevant few are added to later tasks. Nothing is retrained.

## Project Brain and the Playground

The [website](https://brain-rho-roan.vercel.app) uses the same engine. **Project Brain** reads a public GitHub repository in memory, never running its code, and maps its stack, layers and the files a change would touch. **Work on this in VS Code** opens the extension with that plan written into the chat; nothing runs until you press Send. **The Playground** builds an app from a description and runs it inside your browser tab, so no code runs on any server.
