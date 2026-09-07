# Agent config fundamentals — the 2 concepts that unlock everything

Almost every agent config boils down to **two fields**. Explain them in plain
words before touching any specific app:

- **API key** = a private "key" that proves who you are / that you paid. Like
  the key to your house — don't hand it out, don't paste it publicly.
- **Base URL (or API host / 接口地址)** = the *address* of the door the key
  opens. For an official provider it's their endpoint; for a relay/reseller it
  is the relay's own endpoint that speaks the same protocol.

> Most "my key doesn't work" cases are a wrong base URL or a provider mismatch,
> not a bad key.

---

## 1. OpenAI-compatible = the lingua franca

The huge majority of agents accept an **"OpenAI-compatible"** provider
because it's the de-facto standard. If an agent lists only "OpenAI" as a type,
you can still plug in many other models by:

1. Setting the provider type to **OpenAI-compatible / Custom / 自定义**.
2. Pasting the **base URL** of your actual provider (DeepSeek, a relay, etc.).
3. Pasting the **API key**.
4. Typing the **model name** exactly as your provider names it.

That's it. The same 4 fields cover DeepSeek, a Chinese relay, Groq, etc. in
most agents.

---

## 2. Anthropic / Claude & Google / Gemini

Some agents have first-class native sections for Claude or Gemini:

- If an agent has a native **Anthropic** type and you're using a real Claude
  key → just paste the key; base URL is defaulted.
- If you're using an **Anthropic-compatible relay** → switch to "custom",
  set the relay base URL + key.
- **Gemini**: many agents accept a Gemini API key directly, or via an
  OpenAI-compatible shim. Check the agent's provider dropdown first.

---

## 3. Anthropic-compatible & proxies (Claude Code / SDKs)

For SDKs/CLIs that speak Anthropic's protocol but you want to point them at a
relay or another backend:
- Set env `ANTHROPIC_BASE_URL` to the endpoint.
- Set env `ANTHROPIC_AUTH_TOKEN` / `ANTHROPIC_API_KEY` to the key.
- Model must be one the endpoint serves.

> A relay that "speaks Anthropic protocol" can be used anywhere Anthropic's
> protocol is expected, just by overriding the base URL. This is exactly how
> people point Claude Code at cheaper backends — describe it plainly, never as
> a way to abuse an official key.

---

## 4. Common field names across apps

| Concept | Cherry Studio | Chatbox | NextChat | LobeChat | Dify | OpenAI-compatible generic |
|---|---|---|---|---|---|---|
| Provider type | Model provider → 添加 | Settings → Provider | 设置 → 模型服务商 | 模型提供商 | 模型供应商 | — |
| Base URL | API 地址 / Base URL | API Host | 接口地址 | API 代理地址 | API Base | base_url |
| Key | API Key | API Key | API Key | API Key | API 密钥 | api_key |
| Model name | 模型名 | Model | 模型 | 模型 | 模型名称 | model |

(Exact labels drift with versions; if a label differs, the user can search the
app's own docs — the *concept* is always the same four fields.)

---

## 5. Sanity rules

1. Confirm the provider is **OpenAI-compatible, Anthropic-compatible, or has
   a native section** in the agent *before* promising it will work.
2. For Chinese users hitting international providers, mention (factually) that
   a stable network path is needed and that **an OpenAI-compatible relay's
   local endpoint** is often how it's done — with the 🟡/🔴 vetting from
   `references/safety.md`.
3. Never advise stealing keys or scraping a provider to bypass auth.
4. If config still fails, go to `references/agents/troubleshooting.md`.
