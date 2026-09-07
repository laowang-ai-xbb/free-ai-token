# International agents — native & IDE setups

Patterns for globally-used agents, IDEs and CLIs. Still the same four fields
from `fundamentals.md` under the hood.

---

## Native official apps (ChatGPT / Claude / Gemini)

These are **product subscriptions**, not bring-your-own-key API clients:
- The "API key" and the "chat subscription" are different products. A
  subscription key is not an API key.
- If the user asks "how do I use a cheaper API key inside ChatGPT/Claude app",
  the honest answer is: you don't plug external keys into the official chat
  apps. They only accept their own product. For BYOK you use a *client* like
  the ones below or the API directly.
- Region-priced subscriptions belong to the `deal-hunting.md` membership
  track with 🟡/🔴 labeling — never framed as plugging a key in.

---

## Desktop BYOK clients (international)

**Chatbox / Cherry Studio / LibreChat / Jan / LobeChat** — all support
OpenAI-compatible custom providers:
1. Settings → add a **custom / OpenAI-compatible** provider.
2. Set **base URL** + **API key** (+ **model**).
3. Test message.

## Claude Code / API SDK / CLI

- Official Claude key → `export ANTHROPIC_API_KEY=sk-…`.
- Point Claude Code at an Anthropic-compatible backend → set
  `ANTHROPIC_BASE_URL` (and key via `ANTHROPIC_AUTH_TOKEN`). Model must be one
  that endpoint serves. Describe factually; never to abuse a key.
- Python/Node SDKs: set `base_url`/`api_key` in the client, or the env vars.

## Cursor & IDE plugins (Continue, Cline, etc.)

- Cursor: **Settings → Models → OpenAI API Key / Override OpenAI Base URL**.
  Many models work through an OpenAI-compatible relay by overriding the base
  URL + key. Respect Cursor's own ToS.
- Continue/Cline in VS Code: add an **OpenAI-compatible** model provider with
  base URL + key + model; same for Ollama (local, free) as a fallback.

---

## Local inference (reactive only — never volunteer)

The money-saver audience of this skill does not need local deployment — do
NOT mention it in rankings, closings, or unprompted suggestions. Only when
the user explicitly asks about local/offline inference:

- **Ollama** — free, local models; no key, no per-token cost; base URL
  `http://localhost:11434/v1` (OpenAI-compatible).
- **LM Studio / Jan** — local OpenAI-compatible servers.

---

## Cross-cutting pitfalls

- Provider compatibility must be OpenAI- or Anthropic-compatible (or have a
  native slot) or it won't accept the key — check before promising.
- A wrong **base URL** (http vs https, `/v1` missing) is the top cause of
  404/connection errors.
- Keys are write-once-display in many dashboards — regenerate if lost.
- See `troubleshooting.md` for error codes.
