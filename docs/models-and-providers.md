# Models and providers

Checked on 1 October 2026. Free tiers change often, so check each provider's own page before relying on a number.

## Which providers are free

| Provider | Free key, no card | Free limits | The catch |
| --- | --- | --- | --- |
| Google Gemini | Yes | Not published; AI Studio shows your key's | Free-tier prompts may be used to improve Google's models |
| Groq | Yes | 1,000 requests a day, 30 a minute | A small per-minute token cap, about 8,000 |
| Mistral | Optional | Not published | Free only after choosing its Experiment plan and verifying a phone number; otherwise refused |
| OpenRouter | Yes, free models | 50 requests a day, 20 a minute | 1,000 a day after a one-time $10 top-up |
| Cohere | Optional, trial key | 1,000 calls a month, 20 a minute | Personal, non-commercial use only |
| OpenAI | Paid | Set by your account | Used only when no free key can answer |
| Anthropic | Paid | Set by your account | Used only when no free key can answer |

## The free trial

Until you add a key, tasks run on Free Agent Coder's free trial: a daily allowance on the project's own keys, served through the project's site, which picks Groq for quick steps and Gemini for big ones. The allowance resets at 00:00 UTC. It is there so the first task works straight away; your own free key is faster, private, and has no daily cap of ours.

You can also point it at a model on your own machine through Ollama, with no limits and nothing leaving your computer.

## How a task is routed

Every task is sized first. Each size has its own order of providers, built from the keys you have:

| Size | Order | Why |
| --- | --- | --- |
| Fast | Groq → Gemini → Mistral → OpenRouter → Cohere | Groq answers in a second or two, and small requests fit its tier |
| Deep | Gemini → Mistral → OpenRouter → Cohere → Groq | Gemini's 1M-token context carries long, multi-file work |
| Paid | Anthropic → OpenAI | Only when no free key is active |

Within a provider, the key used least today goes first, so the load spreads across your keys. Cohere comes late because its monthly allowance runs out quickly. You can pin a model from the model menu at any time, and your other keys stay ready as fallbacks.

Some jobs need a particular ability. The screenshot reader and the scanned-PDF reader use vision-capable models only, and the lesson writer uses the fast chain. **Settings → Health** shows each job, the models serving it, and whether each key is working right now.

## What happens at a limit

The router walks the chain on every model call.

- **A model that errors** cools down for 15 to 60 seconds, doubling after each failure in a row, up to 5 minutes, while the next model answers.
- **A rate-limited model** is parked for as long as the provider asks, and the next one answers. With nothing else to try, a short wait is served in place.
- **A request too large for a free tier** teaches the router that model's real size for the rest of the session, and bigger requests go elsewhere.
- **A daily limit** sets that key aside until it resets. It recognises each provider's wording, such as Gemini's per-day quota and Groq's tokens-per-day limit.
- **If everything fails**, the panel lists each model and its reason in plain words.

## How limits are shown

Quota bars show only what a provider reports in its responses. Groq, Mistral, OpenRouter, OpenAI and Anthropic report theirs; Gemini does not, so Gemini keys show your own usage only. **Limits across your keys** adds each provider's reported limits together, and a warning appears when a key drops below 10% of its limit.

## One key per account

A second key from the same account shares that account's limits, so it adds nothing. Making extra accounts to multiply a free tier breaks the providers' terms, and those keys tend to be banned together. The extension never suggests it; it suggests a different provider instead.
