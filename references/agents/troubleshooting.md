# Troubleshooting — "I filled it in but it doesn't work"

Match the symptom → apply the fix. Explain in plain words in the user's
language. Never advise stealing/abusing keys to "fix" an auth error.

---

## Common error → cause → fix

| Symptom / code | Likely cause | Fix |
|---|---|---|
| **401 / 403 Invalid API key** | Wrong key, key expired, or key belongs to a different provider | Re-copy the key from the right dashboard; check trailing spaces; regenerate if unsure |
| **404 Not Found on base URL** | Wrong base URL (typo, missing `/v1`, wrong host) | Verify exact endpoint; add `/v1` if it's an OpenAI-compatible relay; use https |
| **Model not found / model doesn't exist** | Model name doesn't match provider's exact ID | Use the exact ID from the provider docs (case-sensitive) |
| **Timeout / connection refused** | Network path blocked (esp. CN→international), server down | Retry; for CN users, a stable path or a local/regional relay is usually needed (vet relay 🟡/🔴) |
| **429 / rate limited** | Over quota or too fast | Wait; raise plan/free-tier allowance; slow requests; check balance |
| **402 / insufficient balance** | Credits/funds depleted | Top up or switch to a free-tier provider |
| **Certificate / SSL error** | Wrong endpoint (http), MITM proxies | Use https; check corporate proxy/antivirus |
| **Key works in browser but not in app** | App cached an old key, or pasted with extra chars | Re-paste; restart the app; clear model cache |
| **Provider not listed in app** | App has no native slot | Use "OpenAI-compatible / Custom" slot with base URL + key |
| **Payment/card declined on signup** | Region/card mismatch | Use a virtual card or a local-payment-capable provider; never hand card to sketchy reseller |
| **"Can't use this model in this region"** | Geo-restriction on the product | This is a ToS/region matter — inform, don't route around via abuse |

---

## Region / proxy diagnostic ladders (registration flows)

**L1 — Homepage opens, but console/API returns Forbidden:**
1. Wrong browser or missing session? Re-check in the browser that actually
   holds the login session (`auto-register.md` Gate 2).
2. Still Forbidden in the logged-in browser ⇒ the proxy **exit node** is
   blocked → switch to a 美国/日本/新加坡 node (avoid 香港 / data-center
   IPs) and re-test once.
3. Every node fails ⇒ the whole route is blocked → stop retrying; back to
   the wall menu with the best reachable 🟢 alternative.

**L2 — Deep link (console path) returns Forbidden:**
Not a typo'd URL — an auth/region gate on an SPA route. Do not retype it:
enter via the front door (homepage → official entry), confirm the login
session, then navigate inside the app UI.

---

## 30-second self-check before asking for help

1. Key has no stray spaces and is the **right provider's** key.
2. Base URL is **https**, exact, includes `/v1` if OpenAI-compatible.
3. Model name is the **exact ID** the provider documents.
4. You're not already rate-limited or out of balance.
5. You clicked **Validate/Manage** and the app loaded the model list.
6. For CN→international, the network path is actually stable.

---

## Escalate rules

- If a fix requires something on the `safety.md` red lines (abusing a key,
  bypassing auth, sharing a stolen key) → **refuse** and offer the legitimate
  alternative.
- If the issue is a provider outage → check the provider's status page, don't
  blame the config.
- If truly stuck after the table → ask the user for the **exact error text**
  and the provider type they chose, then solve against that, rather than
  guessing.
