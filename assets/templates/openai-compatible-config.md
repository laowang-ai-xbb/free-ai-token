# OpenAI-compatible provider config template

Ready-to-fill template for agents that accept an **OpenAI-compatible** custom
provider. The skill can generate this filled-in for the user when asked, so
they only paste it. Keys are placeholders here — never ship a real key.

## Minimal fields

| Field | Value (fill me) | Example |
|---|---|---|
| provider_type | `openai-compatible` | |
| base_url | `{your provider endpoint, https, usually ends in /v1}` | `https://api.deepseek.com/v1` |
| api_key | `{your key, keep private}` | `sk-…` |
| model | `{exact model id}` | `deepseek-chat` |

## .env style (for SDKs / CLI)

```bash
# OpenAI-compatible via relay
export OPENAI_API_KEY="sk-your-key"
export OPENAI_BASE_URL="https://your-endpoint/v1"

# Anthropic-compatible (Claude Code etc.)
export ANTHROPIC_API_KEY="sk-ant-your-key"
export ANTHROPIC_BASE_URL="https://your-anthropic-endpoint"
```

## JSON provider preset (Cherry Studio / LibreChat style)

```json
{
  "provider": "custom-openai",
  "type": "openai",
  "api": { "base_url": "https://your-endpoint/v1", "key": "sk-your-key" },
  "models": [{ "name": "your-model-id" }]
}
```

## Rules

- base_url must be **https** and include `/v1` for OpenAI-compatible relays.
- Never paste a real key into a chat/shared file. Fill it only in your own
  env/password manager.
- Verify the model id against the provider's docs before saving.
