---
name: free-ai-token
description: "Global AI money-saver: find FREE or cheap LLM API tokens/keys, free AI apps (no key), and low-cost AI memberships (region deals for Claude/OpenAI/Gemini; Turkey/India/Argentina subscriptions); auto-registers accounts and wires keys into agents (Cherry Studio/Chatbox/NextChat/LobeChat/Dify); scheduled scans via /deals /scan. 免费token · 白嫖AI · 低价API · 便宜AI会员 · 怎么免费用AI · 免费AI产品 · cheapest API · free API key · AI membership deal · cheap AI subscription. NOT for general AI pricing questions or ordinary chat/translation."
version: "2.9.5"
---

# Free AI Token — Global AI Money Saver

_(v2.9.5 · updated 2026-09-07 · scenario→pick table + 6 new radar vendors · requires the 2.8.0 debt release)_

## Execution principle — 先看清，再动手 (observe before you act)

Three iron rules for every action this skill takes:

1. **看到了才算数.** After every navigation or typing action, read back the
   scene (address bar, tab title, the intended UI element). Never assume a
   pressed Enter arrived. `Forbidden` / error JSON / blank shell on screen =
   navigation FAILED (`auto-register.md` §2.0, `agents/troubleshooting.md`).
2. **在用户真实的路径上验证.** Network reachability is judged by the user's
   own browser path — backend shell probes are clues, never verdicts
   (`deal-hunting.md` §3.2, `auto-register.md` §0.1).
3. **禁止一刀切假设.** 海外 ≠ 需代理; "I know this URL" ≠ the URL opens.
   Labels need evidence; no evidence → no label.

**Live-audit rules** (codified from the last hands-on run; they bind exactly
like the three iron rules above):

4. **用户给了路径，就先跑那条路径.** When the user supplies a concrete path,
   execute *that* path first. If your prior conclusion and what you actually
   observe disagree, the observation wins — state the conflicting conclusion's
   source and date, never silently restate it.
5. **判断前先扫一遍页内 AI 助手.** On any page, look for an embedded AI
   assistant before concluding. Before marking a page "非对话页 ⇒ 不可测试",
   check the URL parameters, the history / conversation list, and any
   login-state differences.
6. **帮用户办事，不当流程审查员.** Stay goal-driven (finish the user's
   register / claim / withdraw). At a gate, report only the credentials it
   genuinely blocks on right now (e.g. a phone number); do not escalate
   optional or later-stage ones (e.g. an ID upload the gate doesn't require).
7. **流程知识进技能，不进聊天记录.** Reusable procedure knowledge belongs in
   this skill's files. IM (e.g. 小Q) is a delivery channel, not the home of a
   workflow — a process that lives only in chat is lost.

Find the **safest free / low-cost** ways to use AI worldwide, across **three
delivery forms kept strictly separate** — free AI products (sign in and use,
no key) · API tokens/keys (register → wire into a tool) · membership plans
(incl. region deals) — score them neutrally, and get the user set up
(registering, buying, configuring) with as little manual work as possible.
Never blend the forms in one line or card (`deal-hunting.md` §1 gate).

> **①②③ are module IDs ONLY** — ① API tokens · ② free AI products ·
> ③ memberships (`ranking-template.md` §2) — one meaning in every file.
> Never repurpose them as generic enumeration (the 2.7.0 preamble defect).

Work in the **user's language** (auto-detect English / Chinese from the
message; default English when ambiguous). All deliverable output uses that
language; display labels come from `references/i18n/<lang>.json`.

## Core behavior — "Act now, don't chat"

On trigger, **no introductory questions and no small talk.** Run the hunt,
return a concrete ranked result. Ask only when an essential input is truly
missing (region / model / budget) — and then as ONE batched question with
sensible defaults the user can accept by not answering. Prefer defaults over
stalling.

**Bare invocation** (the skill is @-mentioned with no task text): don't ask
what to do — run LIGHT in the cached region/language (no cache → en + the
user's apparent locale). A fast useful scan beats a clarifying question.

## Trigger keywords (any of these ⇒ use this skill)

English: free tokens · cheap api key · low cost llm · affordable model access ·
ai membership deal · subscription discount · Turkey/India/Argentina AI plan ·
compare pricing · cheaper ChatGPT/Claude/Gemini · get api key free · any
command defined in `references/commands.md` (`/deals` `/keys` `/eval`
`/compare` `/config` `/register` `/buy` `/specs` `/simple` `/pro` `/scan`
`/estimate` `/safe` `/lang` `/help`)

Chinese: 免费token · 免费/低价API · 便宜AI会员 · 土耳其/印度/阿根廷区订阅 ·
怎么省AI钱 · 白嫖AI · 低价大模型 · 比价 · 配置api key到某某工具 · 定时扫描省钱 ·
怎么免费用AI · 免费AI产品/软件/App · 不用API直接聊天

Platform/product names are fuzzy-matched (grop → Groq): echo the canonical
name once to confirm, never interrogate the typo.

## Mode router — read this first

Pick exactly one mode. **Never load files the chosen mode does not list.**
Loading extra files "just in case" is a contract violation even when harmless
— it burns context and blurs mode boundaries. **Carve-out:**
`assets/vendor-cache.md` is this run's own writable fact/cache layer, not a
methodology doc — it may always be read per workflow §1 and is exempt from the
"load exactly" rule. **Carve-out 2 (output-contract dependencies):** the
files the chosen output contract cannot render without — `scoring.md` §2
(totals & badges), the `vendor-registry.md` official-link column (card links),
and `references/i18n/<lang>.json` (labels) — may always be loaded,
section-scoped where the host supports targeted reads.

| User signal | Mode | Load exactly | Query budget | Output budget |
|---|---|---|---|---|
| Casual "any free/cheap AI api?" · bare `@[skill]` invocation with no task text | **LIGHT** | `deal-hunting.md` §0+§2 · `safety.md` §1 · `ranking-template.md` §1 · `scoring.md` §2 · `vendor-registry.md` (official-link column) · `assets/vendor-cache.md` (read-only ctx) · i18n | 3–5 WebSearch — **one slot reserved for the promo mini-radar** (`deal-hunting.md` §2.6) — + ≤2 verify fetches | ≤22 content lines (shortlist incl.; blank separators don't count), labeled quick-scan |
| `/deals` · "全面比价 / compare everything" · "再多找几家 / find me more options" · scheduled run | **FULL** | LIGHT set (incl. the read-only cache) + `vendor-registry.md` + `discovery-sources.md` + `scoring.md` + i18n; render per `ranking-template.md` §2 | ≤18 total tool-hops (WebSearch+WebFetch combined): 7 classes ×≥1 (stop a class once ≥2 cross-confirmed) + module-② products ×≥2 (`deal-hunting.md` §2.8) + radar ≤2 + verify ≤5 + retry reserve 2; hard stop at 18 | three-module FULL → one-page HTML report (default); plain-text hosts reuse the §1 compact-card grammar, ≤80 content lines |
| `/keys <model>` · `/compare <model>` | **COMPARE** | `scoring.md` · `deal-hunting.md` §2.1 | 4–8 | one table per model |
| `/eval <platform>` | **EVAL** | `scoring.md` · `safety.md` | 4–8 | scorecard + tier + verdict |
| `/config <agent>` | **CONFIG** | the matching `references/agents/*` doc | 0 | ≤4 steps |
| `/register <platform>` · "register me on X" | **REGISTER** | `capability-check.md` · `auto-register.md` | 0–1 | graded automation or hand-holding |
| `/buy <product>` · "帮我买/开通 XX 会员" · user picks a module-③ card | **BUY** | `buy-membership.md` · `safety.md` §4–§5 · `capability-check.md` (browser probe) | 0–1 | graded purchase guidance; **payment never automated** |
| `/estimate` · "每月大概花多少钱" | **ESTIMATE** | `scoring.md` §0–§1 · `commands.md` §3 | 2–4 | usage × option cost table |
| `/safe` · `/help` · `/lang` | **UTILITY** | `commands.md` (+ `safety.md` for `/safe`) | 0 | direct answer |

**Stop condition (all hunt modes):** once a class has ≥2 candidates that
passed cross-confirmation, stop querying that class. Never spend the whole
budget for completeness' sake. If the entire hunt yields zero cross-confirmed
deals, output `{i18n:empty_result}` instead of an empty ranking.

**Natural-language triggers (no commands to teach):** "怎么免费用AI / 免费AI
产品 / 不用API直接聊天" → LIGHT, **beginner persona, module ② first**
(`ranking-template.md` §0.5); "再多找几家 / find me more options" → FULL;
"便宜会员 / 低价订阅 / cheap memberships" → FULL focused on module ③
(any-AI-subscription scope, incl. media & carrier bundles); "帮我买/开通 XX
会员 / get me XX Plus cheaper" → **BUY** (`buy-membership.md`); modality
words (画图/图片/生成视频/配音/语音/做音乐/3D) → modality hunt
(`deal-hunting.md` §2.7).

## Language auto-detection

0. **Saved preference first:** the cache `preferences.lang` (when set) wins
   over the ambiguous-input default below.
1. Chinese characters in the message → reply in Chinese (zh).
2. Clearly English → reply in English (en).
3. **Romanized Chinese (pinyin**, e.g. "woyaozuixinzuiquande"**)** recognized
   from vocabulary/context → treat as zh.
4. Still ambiguous → default English, add `{i18n:lang_hint}` once.
5. `/lang en|zh` overrides everything. Other languages: note that structured
   labels ship only in en/zh, fall back to English.

Mixed audience: give model and platform names in original script with a short
translation in parentheses.

## Region inference (governs proxy framing & ranking filters)

Resolve the user's region BEFORE any 需代理/直连 framing or direct-reach
filtering, in this order:

1. **User's explicit statement** in the message (wins outright).
2. **Saved `preferences.region`** in `assets/vendor-cache.md`.
3. **Unknown** → fold the region question into the ONE batched intake; on a
   LIGHT run with no intake, assume NOTHING — no proxy framing at all this
   run.

Language is a WEAK signal only: zh input never implies region CN. The
region-conditional rules elsewhere (`deal-hunting.md` §3.2 item 5,
`ranking-template.md` §5 item 4) key off the region resolved here, never
off language.

## Instant hunt workflow (LIGHT & FULL)

1. **Context.** Detect language; note the implied region / model need; read
   `assets/vendor-cache.md` (if readable) for saved preferences and the
   last-run snapshot — context only, **never facts to print** (freshness rule
   F4 in `deal-hunting.md` §0).
2. **Search.** LIGHT: the fixed top-source list in `deal-hunting.md` §2.6.
   FULL: ≥1 query per class per `vendor-registry.md` **plus** the
   new-provider radar from `discovery-sources.md`. Query templates, source
   triage and the conflict rule: `deal-hunting.md`.
3. **Freshness contract** — the canonical rules live in `deal-hunting.md` §0
   (F1–F5). In short: as-of date + source on every line; live-verify before
   printing; cannot re-confirm → print `{i18n:policy_changed}`, never a stale
   number.
4. **Score & tier.** `scoring.md`: unit normalization (§0) → 7-dimension
   weighted total + confidence flag (§1–§2); assign the 🟢/🟡/🔴 tier from
   `safety.md`. "Confirmed" requires ≥2 independent sources or the official
   page; on conflict the official page wins.
5. **Render.** `ranking-template.md` — pick the **persona rendering** first
   (§0.5: beginner vs expert, auto-detected; `/simple` `/pro` override; it
   also decides the shortlist variant and the module order), then the
   shortlist (§1.1), then compact cards (LIGHT, §1 — led by the one-line
   {i18n:best_pick_headline}, which must pass §1.1 eligibility) or the
   **three** back-to-back modules (FULL, §2 — ① API · ② 免费 AI 产品 ·
   ③ 会员三货架, official discounts first). Run the pre-delivery checklist
   (§7) before sending.
6. **Close.** The two-line close per `ranking-template.md` §8 (delivery-form-
   matched action line + plain-word escape hatch), then the sanctioned **ONE
   disclosure line** (§8.1: cache state + the global "official pages
   unreachable" note when applicable + at most one time-boxed promo). If the
   user's message already states intent ("register me on X" / "帮我买 XX
   会员"), skip the menu and execute — load `auto-register.md`,
   `buy-membership.md`, or the matching `agents/*` doc.
7. **Persist — hard gate, BEFORE composing the send.** Seed confirmed
   discoveries + preferences per the `assets/vendor-cache.md` rules
   (persistence ladder + **ingression gate** included there). If nothing was
   persisted, the disclosure line must carry a CONCRETE reason (host
   read-only / nothing cross-confirmed / write error) — a bare "not
   persisted" is a checklist failure; never claim "saved".

## Model-vs-platform compare (COMPARE mode)

One table per model, channels as rows: normalized price per 1M output tokens
(`scoring.md` §0), speed/stability/quota evidence, safety tier, confidence
flag, as-of date. End with one best-value line per use case (coding / chat /
translation / batch).

## Configuration teaching (CONFIG mode)

1. Load the matching doc: `agents/fundamentals.md` (concepts first),
   `agents/international.md`, or `agents/domestic-oss.md`.
2. Explain in plain words — "API key = the key; base URL = the door's
   address".
3. Give the shortest copy-paste path (2 fields: base URL + key).
4. If the agent supports config import, offer a ready-to-import file from
   `assets/templates/`.
5. On errors → `agents/troubleshooting.md`.

## Registration & API-key automation (REGISTER mode)

Run `capability-check.md` (probe capabilities, never names) →
`auto-register.md` graded protocol: silent pre-checks first (reachability
pre-flight with **session-first reuse**, ToS, account-status probe), then the
**expectation declaration** (number of assists + rough time + the three
safety promises, §0.5), then the **highest gear the user can ride**
(L4→L0 auto-shift, §0.4). Enter through the official front door, automate
what the environment allows, pause at human-verification gates with the
handoff protocol (§2.2), narrate progress, degrade honestly. If the user
only wants to *use* free/cheap AI, offer the **delivery downgrade** first
(key → login-and-use C7 app → cheap membership) — the key path is the
hardest delivery form. Every dead end lands in the fallback ladder (§7) with
a saved checkpoint (§8). **Never claim a browser action that did not
happen.** Keys go only to the credential ladder's secure store — never
plaintext in chat, never into `vendor-cache.md`.

**Post-success continuity (don't drop the user at the finish line):** the
intake already asked which tool they use — on key capture, load that
`agents/*` doc and start the config walkthrough **without asking again**;
then offer, in one line, the scheduled scan (`/scan`) to watch price drops /
quota resets at the trust peak.

## Membership purchase (BUY mode)

`buy-membership.md` — the graded purchase flow for core function ③: shelf
routing (official discount 🟢 → carrier bundle → cross-region 🟡 → reseller
🔴), ONE batched intake (product / account region / payment means / device),
expectation declaration with the **price restatement** and the buy-version
three promises, gears L3→L0 with **payment never automated**, the worst-case
line ({i18n:worst_case}) before any cross-region step, and the
purchase-confirmation stop (charge matches → plan active in-app → renewal
date + cancel path). Checkpoints: `purchased` / `plan_active`. Fabricated
identity / address / payment remains a hard refusal (`safety.md` §2).

## Scheduled deal scanning

On a recurring/scheduled run, produce the compact deal brief per
`commands.md` §2 in the user's language (< ~300 words): headline changes,
new free credits, expiring promos, price moves, risk alerts. Diff against the
last snapshot in `vendor-cache.md` when one exists; without a baseline, say
"first scan — no baseline to diff" and give a plain brief.

## Safety floor (never cross)

- Never help steal quota, commit identity fraud (including fabricated local
  identity/address for region deals), or bypass paywalls via technical abuse.
- Grey / region-locked / reseller channels may be *described with steps and
  clear ⚠️ labels* (`safety.md`), but compliance/ban risk and ToS caveats
  come first. "You decide; we inform."
- Neutral, conflict-of-interest-free scoring (`scoring.md` §4).

## Resource index

| Concern | File |
|---|---|
| Hunt methodology, query templates, **freshness contract (canonical)** | `references/deal-hunting.md` |
| Coverage map — classes to scan (**no prices inside**) | `references/vendor-registry.md` |
| New-provider radar (brand-new free-token vendors) | `references/discovery-sources.md` |
| Neutral scoring: unit normalization, 7 dims + confidence | `references/scoring.md` |
| Safety tiers, key hygiene, scam detection | `references/safety.md` |
| Commands (canonical), `/estimate`, scheduled brief, preferences | `references/commands.md` |
| Graded register/get-key automation | `references/auto-register.md` |
| Graded membership purchase (payment never automated) | `references/buy-membership.md` |
| Host capability probe (portable) & guided install | `references/capability-check.md` |
| Pre-delivery checklist & golden test cases | `references/self-check.md` |
| Agent config fundamentals / international / domestic-OSS / errors | `references/agents/*.md` |
| Output strings (en/zh) | `references/i18n/en.json`, `zh.json` |
| Ranking/report templates (compact & full) | `references/ranking-template.md` |
| One-page HTML report skeleton | `assets/templates/full-report.html` |
| Ready-to-import config template | `assets/templates/openai-compatible-config.md` |
| Writable cache & preferences (persistence ladder) | `assets/vendor-cache.md` |
