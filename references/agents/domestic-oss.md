# Domestic & open-source agents — wire in a key in 2 steps

These are the apps most Chinese users and many global self-hosters use. For
each, the pattern is the same four fields from `fundamentals.md`. Exact UI
labels drift with versions — if a label differs, search the app's own docs;
the concept is unchanged. Write instructions in the user's language.

---

## Cherry Studio (Windows/macOS/Linux desktop)

1. **设置 (Settings) → 模型服务 (Model Provider) → 添加 (Add)** or pick a
   provider.
2. Choose **"OpenAI 兼容 / OpenAI-compatible"** as the type when the provider
   isn't natively listed.
3. **API 地址 / Base URL** = your provider endpoint.
4. **API Key** = paste key.
5. **模型名 / Model** = exactly what the provider calls it.
6. Click **管理 (Manage)** to confirm the model list loads → then chat.

## Chatbox (desktop/web)

1. **设置 (Settings) → AI 模型提供方 (Provider)**.
2. Add a provider or choose existing; set **API 域名 / API Host** + **API Key**
   + **Model**.
3. Save, then send a test message.

## NextChat (Vercel/self-hosted web)

1. **设置 (Settings) → 模型服务商 (Provider)**.
2. Pick **OpenAI** (or **自定义接口**), set **接口地址 / Base URL** and **API
   Key**.
3. Add the model name under models. Deploy env vars `OPENAI_API_KEY` and
   optionally `BASE_URL` if self-hosted.

## LobeChat (web/desktop)

1. **设置 (Settings) → 语言模型 (Language Models) → 添加自定义模型提供商 /
   OpenAI**.
2. **API 代理地址 (Base URL)** + **API Key** + enable the model.
3. Refresh model list and pick it in a new session.

## Dify (self-hosted LLM app platform)

1. **设置 → 模型供应商 (Model Provider)**.
2. For OpenAI-compatible: add provider with **API Base** + **API Key**, or use
   a provider that exposes a Dify "Access Token".
3. Validate the connection, then assign the model in an app's settings.

## FastGPT / Open WebUI / one-api-style gateways

- All follow the same shape: **Base URL + Key (+ model)** under their provider
  settings. one-api/new-api style panels let you *add* many upstream channels
  behind one key — describe the concept, warn about 🟡/🔴 relay risk per
  `references/safety.md`.

---

## Universal 2-step fallback (if the app supports OpenAI-compatible custom)

```
Step 1  Provider type = "OpenAI-compatible" / "Custom" / "自定义"
Step 2  Base URL = {endpoint}   ·   API Key = {key}   ·   Model = {model}
```

If the app has **only** a native OpenAI/Anthropic/Gemini slot, then:
- Use OpenAI slot + relay base URL if you want a non-OpenAI model (relay must
  be OpenAI-compatible), OR
- Use the native slot only if you actually have that provider's key.

---

## Pitfalls specific to these apps

- **Model name mismatch** is the #1 silent failure (e.g. provider ships
  `deepseek-chat` but you typed `DeepSeek-V3`). Use the exact ID the provider
  documents.
- Some apps need you to click **Manage / Validate / 刷新模型列表** before the
  model is usable.
- Proxy/gateway keys (one-api) are OpenAI-compatible → they slot into any of
  the above via base URL.
- Never enable "unlimited context" tricks that just fail; set the context the
  model truly supports.
- If it still won't connect → `references/agents/troubleshooting.md`.
