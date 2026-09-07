# Discovery Sources — how new free/low-cost token providers keep surfacing

The registry (`vendor-registry.md`) guarantees *known* vendors don't get
missed. This file guarantees **brand-new vendors** don't get missed either.
Static maps can't know about a provider launched this week — only live
discovery sources can. Run these **every FULL hunt, in parallel with the
registry coverage queries**.

> Why: new free-token platforms appear constantly. If we only ever search what
> we already know, we are blind to everything new. These queries are the
> "radar"; the registry is the "map".

---

## 1. New-provider radar queries (fire each FULL hunt)

English (parallel):
- `new free LLM API provider {year}`
- `new AI inference startup free credits launch`
- `new openai-compatible api free tier this month`
- `free GPU inference credits new provider`
- `HN new LLM api / ask hn cheap api`
- `site:news.ycombinator.com "Show HN" LLM API free {year}`
- `{provider} free tier announced {month} {year}`
- `new model free tier launch {month} {year}`
- `github new openai compatible inference server`
- `artificial analysis cheapest models {year}`
- `telecom cloud free LLM credits` · `operator cloud AI free quota`
- `AI coding agent free models {year}` (Copilot Free / Windsurf / Trae class)

For China-relevant:
- `新的免费大模型API 平台 {year}`
- `新出的AI推理平台 免费额度 注册送`
- `大模型api 新用户 免费token 送额度`
- `运营商云 大模型 免费额度`（天翼云 / 移动云 / 联通云）
- `魔搭 新模型 免费调用`
- `新 AI 编程工具 免费模型额度`
- `大模型 发布 免费开放 {month}`

Launch/curation channels to check (nine posts):
- Hacker News ("Show HN" + "Ask HN: cheap LLM api")
- Product Hunt (tags: api / developer tools / ai)
- r/LocalLLaMA, r/OpenAI, r/SideProject (weekly "new api" threads)
- OpenRouter model catalog "recently added" (aggregator as a discovery feed)
- Reddit r/ArtificialIntelligence deal threads (vet heavily)
- Hugging Face trending models / new Spaces
- GitHub trending (new inference servers & OpenAI-compatible projects)
- ModelScope 魔搭 community (new domestic models & free-call events)
- Artificial Analysis — quality/speed/price leaderboards (doubles as the
  evidence source for the free-strong-models shortlist, `ranking-template.md`
  §1.1)
- X.com — **best-effort only**: X content is largely closed to web search;
  catch what surfaces, never rely on it (launch news usually propagates to
  the other channels anyway)

---

## 2. How to tell a "real new vendor" from a scam/shill

New vendors are the highest scam-density category — the radar catches both.
Before ranking any discovery, apply:
1. **Official presence**: does it have a real official site/docs/pricing page?
   Aggregator "listings" or Telegram-only "deals" ⇒ not a vendor, treat
   as 🔴.
2. **Cross-check**: ≥2 independent sources or the official page confirms it.
3. **Paywall sanity**: "free" that needs a card + recurring auto-charge ⇒
   read the cancel path before calling it free; else mark 🔴 watch-out.
4. **No-history cloak**: no GitHub, no docs, no changelog, only hype ⇒ 🔴.
5. **Model × platform mapping**: to state *which specific model is free on
   which platform*, use the **OpenRouter model "providers" view** and
   **Artificial Analysis** model→pricing tables (both list every serving
   channel + its price / `:free` flag in one place), plus the platform's own
   catalog. Gated by `deal-hunting.md` §3.3 — never generalize one channel's
   free model onto another platform.

Use the 🟢/🟡/🔴 tier from `safety.md` — do not promote a discovery above a
verified 🟢 just because it's novel.

---

## 3. Feed back into the cache (回灌)

A discovery that passes §2 is seeded into **`assets/vendor-cache.md`** (the
fact layer), never into the registry itself:

```
New confirmed vendor → assign its class (GPU cloud C1 / inference C2 /
China C3 / frontier C4 / aggregator C5 / membership C6 / app-bundled C7)
→ stamp verified-on {date} + risk tier + source in the cache
→ keep in session cache; flag "NEW" in this run's ranking
```

Rules: one-snippet claims and pure promo never get seeded; only
cross-confirmed entries. When a previously-seeded vendor's deal expires or
turns out wrong, remove it next run and note the correction — do not hoard
stale rows (accuracy beats shelf count).

---

## 4. Freshness guard

Discovery adds *breadth*; it does not exempt anyone from *freshness*. Every
surfaced or re-surfaced deal follows the canonical freshness contract in
`deal-hunting.md` §0 (F1–F5): as-of date + source on every line; anything
that can't be re-confirmed prints "{i18n:policy_changed}", never a confident
stale number.
