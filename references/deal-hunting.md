# Deal Hunting — search method, query templates, and THE freshness contract

This skill is **real-time-first**: pricing, promos and free-credit windows
change daily, so live search always wins over memory. Hit multiple sources in
parallel, and always record *when* each deal was verified.

---

## 0. Freshness contract — CANONICAL (the only full statement)

> Every other file must reference this section, not restate it.

- **F1 — Date every line.** Every deal shown carries `as-of {date}` and a
  real source link ({i18n:as_of}).
- **F2 — 24 h TTL.** Any figure older than 24 hours must be re-verified
  before display. Same session, >24 h since first check → re-search, don't
  reuse.
- **F3 — No stale confidence.** If a previously-hot vendor's current policy
  cannot be re-confirmed this run, print "{i18n:policy_changed}" — never the
  old number dressed up as current. But "unreachable" ≠ "changed": if the
  official page only *failed to load* this run, first run the degraded
  verification chain in §3.1 (docs subdomain → independent secondaries) and
  cap confidence accordingly; reserve "{i18n:policy_changed}" for when nothing
  corroborates.
- **F4 — Snapshots are not facts.** Numbers in `vendor-registry.md` or
  `assets/vendor-cache.md` are map/memory. Nothing from them may be printed
  without THIS run's live verification.
- **F5 — Estimates wear a label.** Any computed or converted figure starts
  with "~" and the line's confidence flag drops accordingly
  (`scoring.md` §2).
- **F2.5 — Graded re-verify (budget guard).** F2 full re-verification is
  mandatory for every figure the run actually PRINTS (cards, shortlist,
  best pick). Secondary/exploratory candidates that surfaced but did not make
  the cut may carry their cached figure only as ⚠ {i18n:badge_unverified}
  "not re-verified this run" — never ✓ or ~. If a printed candidate's
  verification cannot be completed within the mode's verify budget (≤5 hops),
  downgrade it per §3.1 in order; do not exceed the budget re-pinging
  (`{i18n:policy_changed}` remains the last resort). F2.5 relaxes effort for
  unprinted rows only — it never softens the ✓ badge's "official surface this
  run" requirement for anything shown.
- **F6 — Search failure ≠ empty class.** If a class query errors (503 /
  timeout), retry ONCE; still failing → the coverage line says "该类检索失败"
  (search failed) with the class named — never silently dropped, never
  dressed up as "no deals found".

---

## 1. Three hunt targets — three delivery forms, never mixed

The skill serves three distinct user needs. Detect which one the user means
(or cover all three — in SEPARATE modules, never blended in one card/line):

| Target | Delivery form | Who it serves | Example |
|---|---|---|---|
| **Free AI products** | Sign in and use — web / desktop / app, NO key | beginners ("怎么免费用AI") | DeepSeek 网页/App · 豆包 · 智谱清言 · Kimi · Copilot Free |
| **API access / tokens** | Register → API key → wire into a tool | developers / tinkerers | Groq free tier · OpenRouter `:free` · 硅基流动 · NVIDIA NIM |
| **AI membership plans** | Pay (possibly cross-region) for a subscription | heavy users of one product | ChatGPT Plus region price · Perplexity student plan |

**Delivery-form gate (non-negotiable).** Each form needs its OWN evidence —
never extrapolate across forms:

- A product's free **app/web** says NOTHING about its **API** being free.
  Canonical case (verified 2026-09-05, 新浪财经/apifox): DeepSeek 网页/App
  免费, but the **official DeepSeek API has no free tier** — free
  DeepSeek-model API access exists only via third-party platforms, each gated
  by §3.3.
- An API free tier says nothing about the consumer app; neither implies a
  membership discount.
- A line mixing forms ("免费拿 API Key：官网/App 直接用") is a **defect**.
  Render each form in its own module with its own verb: {i18n:get_use}
  (products) / {i18n:get_key} (API) / {i18n:membership} (plans).

**Modality detection:** the default target is LLM text models (the majority
ask). When the user says 画图/图片/生成视频/配音/语音/做音乐/3D, switch to
the matching modality: run §2.7 targeted queries, and remember most non-LLM
free offers live in module ③ (subscriptions) or module ② (consumer apps),
not module ①.

---

## 2. Query template library

Fire these in parallel. Replace `{model}` / `{region}` / `{year}` as needed.
Run both English and (for China-relevant results) Chinese variants.

> **Budget accounting:** a "hop" is one WebSearch or WebFetch call. Unless the
> mode router's row says otherwise, they share the per-mode budget, and
> "parallel" means issued together — not that fetches are free. (LIGHT's row
> exempts ≤2 verify fetches; FULL counts everything against its ≤18 ceiling,
> incl. the 2-hop retry reserve.)
> **Fetch priority:** when any fetch budget exists, the first attempt goes to
> an official surface for the run's top candidate (§3.1 rung 1) BEFORE
> third-party verification fetches — an official ✓ is worth more than two
> secondary ~s.

### 2.1 API free tiers & credits
- `{provider} free API tier {year}`
- `free LLM API key no credit card`
- `new user {provider} free credits`
- `best free AI API for developers`
- `cheapest gpt / claude / gemini api price per 1M tokens {year}`
- **GPU-cloud free credits (do not skip — AMD/NVIDIA live here):**
  `NVIDIA build.nvidia.com free credits NIM API` / `AMD inference cloud free
  tier LLM` / `cloud free tier LLM credits AWS Bedrock Azure Vertex`
- **Model × platform availability — fill the TEMPLATE, never hardcode a model
  name (models churn weekly, so the shape is fixed and the `{model}` / `{platform}`
  slots take THIS run's values):**
  `{platform} {model} free tier {year}` · `{platform} {model} :free` ·
  `{model} providers pricing` · `{platform} model catalog free`. This answers
  "which model is free, on which platform" — not merely "does a platform have
  any free tier". Every such claim must clear the §3.3 gate before it is
  printed.

### 2.2 Cheap API aggregators / resellers (🟡 — vet hard)
- `cheapest OpenAI-compatible API relay {year}`
- `{aggregator} review reddit trust`
- `api 中转 价格 对比` / `最便宜的GPT API 中转`
- `is {reseller} legit scam`

### 2.3 New-provider radar (full list in `discovery-sources.md` — every FULL hunt)
- `new free LLM API provider {year}` · `new AI inference startup free credits`
- Product Hunt / HN "Show/Ask" · OpenRouter recently-added feed

### 2.4 AI membership region deals (🟡/🔴 — risk label mandatory)
- `ChatGPT Plus price by country {year}`
- `Claude Pro Turkey price` / `Claude Pro India subscription cheaper`
- `Gemini Advanced cheaper region`
- `how to buy {product} subscription at cheaper region price risk`
- `土耳其区 ChatGPT 订阅` / `印度区 Claude 订阅 教程`
- `is region-priced AI subscription against ToS`

### 2.5 Community & trustworthy signal sources
- `site:reddit.com cheap AI api provider {year}`
- `HN cheap LLM api`
- official provider pricing pages (deepseek.com, openai.com/pricing,
  anthropic.com/pricing, ai.google.dev/pricing, groq.com, etc.)
- Chinese aggregator/relay discussion boards (beware: heavily gamed)

### 2.6 LIGHT-mode fixed source list (fast path)

For casual asks, query only these high-signal staples (review this list
quarterly; keep the whole list ≤5 queries). **The list is REGION-CONDITIONAL
(2.9.0)** — pick ONE set by the region resolved in SKILL.md (user statement
> saved preference > batched intake; never guess from language):

- **CN set** (region CN): 1. Google AI Studio (Gemini free tier) 2. Groq
  free tier 3. OpenRouter free models 4. 智谱 BigModel (GLM free tier)
  5. 硅基流动 SiliconFlow (free RPM tier)
- **Global set** (any other region): 1. Google AI Studio (Gemini free tier)
  2. Groq free tier 3. OpenRouter free models 4. Mistral La Plateforme
  (free tier) 5. Cloudflare Workers AI (free allocation)
- **Module-② ask** ("怎么免费用AI / free AI apps, no key"): replace the
  staples with the registry class **C7** top three consumer products + the
  radar slot below — the five API staples cannot answer a product question
  (the 2.7.0 fast-path blind spot).

If the region is genuinely unknown mid-LIGHT (no cache, no statement), use
the Global set — it is the no-assumption default.

**CN-unknown caveat (one line, no proxy framing):** when a zh-language user's
region is unknown and nothing else indicates it, the Global set still applies
— but the scope line must carry one plain note: "以下海外平台可能需要你自备相应
网络条件；如果你在中国大陆且无法访问，回复你的所在地区，我会切换为可直接使用的
清单" (or the matching en.json string when added). This informs without
assuming CN and without GFW vocabulary. Only zh input + unknown region
triggers it; it is never shown to users in other regions.

**Radar probe (one reserved slot — three-state delta, a time-point increment):**
whenever the budget allows ≥4 queries, this one slot probes "what changed in
the last 7 days", rotating by cache state with graceful fallback:

- **State A — promo probe:** `新出 免费AI 活动 促销 {month} {year}` / `new free
  AI promo {month} {year}` — time-boxed deals on existing platforms.
- **State B — change probe (fallback when State C finds no new platform):**
  `price drop / free tier increase {month} {year}` / `(降价 OR 免费额度扩大)
  {month} {year}` plus `new model released {month} {year}`. A *change* hit on
  a known vendor — verified per §3/§3.3 and cross-confirmed — may wear the
  UPDATED variant of the {i18n:new_badge} flag (same ≤7-day discovered_on
  discipline, `vendor-cache.md` schema 4).
- **State C — new-provider probe:** `new free LLM API provider {month}
  {year}` / `新出 免费AI 平台 {month} {year}`. Templates are self-contained
  (LIGHT never loads `discovery-sources.md`).
- **Order & fallback:** default A; if the cache has no new vendor in 7 days
  AND no promo hit, automatically run B; run C when B also comes back empty —
  all inside the SAME single slot, never extra queries. Every hit still
  passes the full gates (§3, §3.3); an unrankable hit lands in the
  disclosure line (`ranking-template.md` §8.1), never silently discarded. A
  cross-confirmed newcomer records `discovered_on` (schema 4) for future NEW
  badges. When ALL three states come back empty, say so plainly — the
  empty-state protocol is defined in `ranking-template.md` §8.1 (hot-alt
  fallback): verify the strongest cheap options fresh, state "no new
  platforms/promos/model changes in the last 7 days" with leaderboard as-of,
  and remind the user a later run may find more — never fabricate an
  increment.

### 2.7 Non-LLM modalities (image / video / audio / music / 3D)

Fire only on a modality ask (§1 detection):
- `free {modality} generation API {year}` · `免费{模态}生成 API 额度`
- `{Suno/Kling/可灵/即梦/ElevenLabs/Imagen/Meshy/Tripo} free tier {year}`
- `free image generation API no credit card {year}` · `video model free
  credits {year}` · `AI music free daily credits {year}`

Same freshness contract (§0) and tier rules apply; most results rank in
module ③ (subscriptions) or module ② (consumer apps).

### 2.8 Consumer AI products (module ② — per-surface, per-version)

Fire on a beginner ask ("怎么免费用AI") and in every FULL hunt:

- `{product} 网页版 免费 模型 {year}` · `{product} App 免费 额度 {year}`
- `{product} 电脑端 客户端 下载 免费 {year}` · `{product} desktop client free`
- `{product} 最新版本 免费 深度思考 联网 {year}` (which model VERSION is free NOW)

Every module-② card must state, **per surface** ({i18n:surface_web} /
{i18n:surface_pc} / {i18n:surface_app}): available? which model version is
free there — newest / highest 3rd-party-ranked first, each dated? any daily
cap? Surfaces differ (the app may lag the web version) — never merge them
into one claim, and never let a free-app finding leak into "free API"
wording (delivery-form gate, §1).

**Layering (FULL vs LIGHT):** the per-surface detail above is a FULL-card
obligation (`ranking-template.md` §4). A LIGHT compact card
(`ranking-template.md` §1 three-line grammar) carries a single surface
summary line — e.g. "网页/App 免费 · 最新免费模型 {X} · {date}" — never three
surface lines (2.7.0 grammar conflict).

---

## 3. Source triage, credibility & conflict rule

Rank sources before trusting them:

| Source type | Trust | Note |
|---|---|---|
| Official provider pricing/docs/status | High — ground truth | **Wins any conflict** |
| Reddit/HN/tech community (long-history accounts, cross-corroborated) | Medium | Good scam signal |
| Promo/aggregator listing sites | Low | Often paid placement — verify against official |
| Telegram/QQ reseller groups, "cheap key" forums | Very low | Highest scam/fraud rate |

**Conflict rule.** When sources disagree, rank the evidence:
official page > official status/docs > cross-corroborated community reports
> single community report.

**Cross-verify.** A deal is "confirmed" only if ≥2 independent sources agree
or it matches the official page. One sketchy source alone → mark
**{i18n:badge_unverified}** and demote in ranking.

### 3.1 Degraded verification chain (official page unreachable this run)

The rules above cover a source that *contradicts* the official page. This
covers the harder, very common case: the official page **cannot be opened at
all** this run. Official pricing pages frequently fail to fetch — **403**
(console / paywalled dashboards), **JS-rendered shells** (SPA pricing tabs
that return an empty page), or outright **network failure**.
`{i18n:policy_changed}` (F3) is the **last** resort, not the first: before
degrading to it, walk this chain **in order** and stop at the first rung that
yields the number.

1. **Official page, other surface.** If the marketing/pricing URL is blocked,
   try the official **docs** subdomain or a pricing/status sub-page
   (`docs.{vendor}`, `{vendor}.com/docs/pricing`, the status page). A figure
   reached on an official surface still counts as official → confidence may
   stay **✓**. (If a docs figure later conflicts with a reachable marketing
   page, the conflict rule above still decides.)
2. **≥2 independent secondaries, in agreement.** With no official surface
   reachable, corroboration must come from **two or more independent**
   community/listing/aggregator sources stating the *same* figure. **Cap at
   ~** — never ✓, because the official page was not verified this run.
3. **Single secondary only.** One second-hand source (even a reputable one) →
   **⚠**, label **{i18n:badge_unverified}**, and say the official page could not be
   opened this run.
4. **Nothing corroborates, or secondaries conflict.** Fall back to F3: print
   **{i18n:policy_changed}** (⚠) — never the old number dressed up as current.

> **Rule of thumb.** Official page unreachable this run ⇒ the deal **may not
> wear ✓**. Best case ~ (two agreeing secondaries); a single source ⇒ ⚠. In
> all these cases the line must state that the official page was unreachable,
> so the reader knows the number is second-hand.

> **"Confirmed" vs confidence — two axes, no contradiction.** Cross-verify's
> "confirmed" decides whether a deal may be ranked / cached at all (≥2
> agreeing sources or the official page). The confidence flag is a second,
> independent axis: how hard the evidence is THIS run. A deal can therefore
> be confirmed yet wear ~ when no official surface was reached this run — it
> still ranks, but with its second-hand badge on. Never trade one axis for
> the other, and never let "confirmed" upgrade a confidence flag.

**Known fetch pitfall (log it, don't fight it).** JS-rendered / bot-gated
pricing pages — e.g. BigModel `open.bigmodel.cn/pricing`, the Groq
`console.groq.com` dashboard, and Google `ai.google.dev/*` docs — commonly
return an empty shell, **403**, or a `fetch failed`. Try the docs subdomain
**once**, then degrade through the ladder above; do **not** burn the query
budget re-pinging the same blocked URL.

### 3.2 Reachability verdicts (per-platform, user's path)

Governs every reachability tag shown in rankings ({i18n:reach_direct} /
{i18n:reach_proxy}):

1. **Verdicts need evidence — two acceptable kinds:**
   a. **Live test in the user's real path** — direct succeeds ⇒
      "{i18n:reach_direct}"; direct fails but proxy succeeds ⇒
      "{i18n:reach_proxy}". The user's browser path is the judge; backend
      shell probes are clues only (`auto-register.md` §0.1 Gate 1).
   b. **Community feedback** — ≥2 independent recent reports (or one strong,
      dated write-up) stating the platform blocks direct access from the
      user's region ⇒ may label "{i18n:reach_proxy}", with as-of date +
      source. For ranking display this is usually cheaper than a live test —
      prefer it; the registration pre-flight will live-test before any
      signup effort anyway.
2. **No evidence → no tag.** Never print jargon like "reachability
   unverified" — general users can't read it, power users don't need it. An
   untagged platform simply means "not checked yet".
3. **Never infer — in either direction.** Reachability is a per-platform
   fact: "overseas" does not imply blocked (some overseas platforms connect
   fine from mainland China), and **"domestic" does not imply direct** either.
   Blanket labeling is forbidden — it guesses, and guesses cost user trust.
4. **Direct-reach filter:** for users with no working proxy, direct
   reachability becomes a FIRST-RANKING filter — direct-reachable candidates
   precede unreachable ones within the same tier (`ranking-template.md` §5).
5. **Region-conditional framing (the skill is global, the wall is not).**
   Proxy/GFW vocabulary — {i18n:reach_proxy}, exit-node advice, "需代理" —
   activates ONLY when region=CN or the user says they are behind a firewall.
   For every other region: skip proxy framing entirely; reachability notes
   concern the platform's own regional availability, and module ② emphasizes
   local official pricing and local payment methods instead of cross-region
   tricks.

### 3.3 Model × platform availability gate (never assert "free on P" blindly)

A claim that **a specific model M is free on a specific platform P** is a
per-platform catalog fact — a platform's *general* free-tier page does not
prove it. Verify it THIS run against one of:

- platform P's own model catalog / docs pricing (e.g. the build.nvidia.com
  model list, `{vendor}/docs/pricing`, the console's model picker), or
- the **OpenRouter model "providers" view** — one page listing every channel
  that serves model M with each price / `:free` flag (best single cross-check
  across several platforms), or
- **Artificial Analysis** model→providers→pricing tables.

**A model being free on one channel says NOTHING about another** — "GLM free
on OpenRouter" is not evidence of "GLM free on NVIDIA/AMD"; each pairing needs
its own sighting. No sighting ⇒ the "M free on P" claim goes to
`vendor-cache.md`'s `unverified_heard_of`, never into a card, the shortlist,
or a clickable link. This is the source the per-card "strongest free model"
field (`ranking-template.md` §4) and the §2.1 template both draw on.

---

## 4. Region-deal playbook (Turkey / India / Argentina etc.)

Region-priced AI memberships are the most volatile and most-abused category.
When covering them, always output this structure:

1. **What the deal is** (product + which region shows a lower local price).
2. **How people do it** (steps — described plainly; risk-labeled).
3. **Risk tier** per `safety.md` §1 — a **self-service** cross-region buy (own
   account + your own VPN + a payment method you legitimately hold) is **🟡
   (需谨慎)**; it is **🔴** only when it requires fabricated local identity /
   address / payment identity (a `safety.md` §2 red line → steps refused) or a
   paid third-party "setup / 代充" middleman.
4. **Failure modes**: store-account region lock, payment-card country
   mismatch, ban on the AI account, losing a "family/seat" reseller scam.
5. **Cheapest legit alternative**, if one exists (often a better call).

> The provider's own ToS and the app store's rules usually prohibit buying
> via another region's price. Show this caveat *before* the steps. The user
> decides; the skill informs.

**Red-line intersection:** if executing a region deal requires fabricated
local identity documents, addresses, or payment identities, that is identity
fraud — hard refusal per `safety.md` §2. Keep only the risk explanation,
never the steps.

---

## 5. Anti-gaming note (be neutral)

Aggregator/relay markets are full of paid shills. Do not rank by "who paid /
who's popular on a forum". Rank strictly by the neutral score from
`scoring.md` and by the 🟢/🟡/🔴 safety tier. If a source is sponsored, say
so and discount it.
