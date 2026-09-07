# Ranking template — output contracts: compact & full, three modules, checklist

Output contract for every hunt. Render in the **user's language** — display
strings come from `references/i18n/<lang>.json` (referenced below as i18n
tokens; never invent raw-text labels). Safety tier always sorts 🟢 before 🟡
before 🔴, regardless of small price gaps.

**Coverage contract applies first (FULL):** the `vendor-registry.md` map and
`discovery-sources.md` radar must already have run, plus the coverage
self-check line. Never silently omit an empty class (GPU clouds incl.
AMD/NVIDIA, inference, China, frontier, aggregators, memberships,
app-bundled access).

---

## 0. Choose the contract by mode (see SKILL.md mode router)

- **LIGHT** → §1 compact cards, ≤22 **content** lines total (shortlist
  included; blank separators don't count; if over, trim cards to 3), header
  label "{i18n:quick_scan_label}", led by the one-line
  {i18n:best_pick_headline} — beginners want the answer before the list.
- **FULL** → §2 three modules as **three complete blocks, one after the
  other**. **Three-module FULL defaults to the one-page HTML report**
  (`assets/templates/full-report.html`) wherever the host renders HTML.
  Plain-text hosts render the three modules with the **§1 compact-card
  grammar** (three-line cards, not §4 full cards) within **≤80 content
  lines**; the §4 full-card format serves single-module hunts, EVAL, and
  expert deep-dives.
- **COMPARE** → §3 table. **EVAL** → the scorecard skeleton in
  `scoring.md` §5.

**Output voice (all modes):** plain for a beginner, professional for an
expert, at the same time. Two hard bans:

1. **Labels come verbatim from i18n — never improvise a synonym.** Needing
   the get-key label? take {i18n:get_key} as-is (whatever its current value
   is); do not coin shortened slang like "领Key". Anything shown uses the
   plain-word evidence badges (`scoring.md` §2.1) — never a bare
   "(估算)" / "(estimated)"; say WHO verified a figure.
2. **Internal jargon never reaches the user.** 契约 / 维度 / 权重 / 新鲜度 /
   归一化 and the ✓/~/⚠ symbols stay backstage — the user sees an as-of date +
   a plain-word badge (the ✓/~/⚠ set is allowed only in tight tables, and only
   with the legend line beneath.
3. **i18n fallback path (never fail naked).** If the user's language file
   cannot be read, or an `{i18n:*}` token cannot be resolved: render the
   **English** string for that token from `references/i18n/en.json`; if
   `en.json` itself is unreadable, fall back to the internal label names as
   plain English text (no braces, no raw `{i18n:…}` syntax on screen) and
   carry the language note "labels fell back to English" in the disclosure
   line (`§8.1`). A run must never emit raw unresolved `{i18n:…}` tokens or
   bare ✓/~/⚠ symbols to the user.

Deliverable narration ties to the goal (find → get the key → wire it into the
agent), never to side features like printing.

---

## 0.5 Persona rendering — one dataset, two shapes (auto-detect, overridable)

The audience is BOTH beginners and experts; wording rules (§0) are not enough
— the *shape* of the output must fit too. Detect once per run and render
accordingly; `/simple` / `/pro` override, and the override is saved to cache
preferences. Never ask the user which persona they are.

| Signal in the message | Persona | Rendering |
|---|---|---|
| No model names, no tech words (RPM / base URL / token / agent names); asks like "怎么免费用AI" | **Beginner** | Lead with the ONE best pick in a sentence; cards drop scores and token units; quotas humanized via {i18n:human_units} ("≈750 页文档 / 每天约 50 次对话"); jargon glossed inline at first use; **prefer C7 login-and-use apps** (no key at all) as the top recommendation |
| Mentions model names / rate limits / endpoints / specific tools | **Expert** | Full cards with scores (+ {i18n:legend_score} note), normalized prices, evidence badges; `/specs <platform>` on demand adds model IDs, RPM/TPM/RPD, context window, data-training default, commercial-use terms, endpoint path |

**Product-name-only guard:** a message that mentions a *product* name
(Claude / ChatGPT / Gemini …) but contains NO comparison, quota, pricing, or
endpoint vocabulary ("which Claude is cheapest", "Claude 怎么便宜买") stays
**beginner** shape — product familiarity is not expertise. Only
comparison/quota/endpoint/model-ID vocabulary triggers expert. When in doubt,
render beginner and append one line: "想按模型/价格细比？回复 /pro".（"Want a
model-level comparison? Reply /pro."）
**Module order follows the persona:** beginner → ② 免费 AI 产品 → ① API →
③ 会员 (the no-key path leads); expert → ① → ② → ③.

---

## 1. Compact cards (LIGHT) — three-line grammar, 3–5 cards

Each card uses the fixed three-line grammar — one job per line, each line
short enough to scan:

```
{n}) [{Name}]({official_url}) {tier chip 🟢/🟡/🔴} {total}/10{·估n维 if any N/A} · {i18n:chip_nocard|chip_card} · {reachability tag if evidenced}
   {i18n:free_label}: {what's free, normalized — plus {i18n:human_units} in beginner persona} ｜ {i18n:for_who}: {fit}
   {i18n:cons}: {top catch} · {evidence badge} · {MM-DD}
```

- Line 1 = identity (name, tier, score, card chip). The credit-card chip
  ({i18n:chip_nocard} / {i18n:chip_card}) is **mandatory** — "will it ask for
  my card" is a beginner's first fear. A reachability tag ONLY when evidenced
  per `deal-hunting.md` §3.2 — {i18n:reach_direct} / {i18n:reach_proxy}; no
  tag = not checked yet, and **domestic platforms are not presumed direct
  either**. If scoring dimensions were N/A, the score carries the estimate
  annotation (`scoring.md` §2). Never any other label.
- Line 2 = the deal + who it fits.
- Line 3 = the catch + evidence badge (`scoring.md` §2, plain words) + date.
- **Line-1 name is a markdown link to the official signup page**, so a capable
  user clicks straight through. `{official_url}` comes ONLY from the vetted
  domain in `vendor-registry.md` — **never a search-result URL.** A radar find
  not in the registry links only if its domain is corroborated by ≥2
  independent sources; otherwise print the plain name with no link. The
  line-3 evidence badge is where the *verification source* (which may be
  third-party) belongs — kept separate from the action link.

Header block (max 3 lines — title+date, scope+region, best pick):

```
{i18n:title} · {i18n:quick_scan_label} · {i18n:as_of=date}
{i18n:scope_api|scope_member|scope_both} · {i18n:region}
{i18n:best_pick_headline} {the pick + why, one short sentence}
```

The scope label must match what was ACTUALLY hunted (an API-only scan wears
{i18n:scope_api}, never scope_both). `{region}` renders via the display map
({i18n:region_cn} / {i18n:region_us}, else the given name as-is).

Render order: **header → shortlist (§1.1) → cards → close (§8) → the ONE
disclosure line (§8.1)**.

---

## 1.1 Shortlist — persona-conditional, delivery-form exact

Renders in LIGHT and FULL before any cards. **Which shortlist depends on the
persona (§0.5):**

**Expert persona → "free strong models"** (what to use, before where to get
it):

```
{i18n:shortlist_title}
1) {model} — {one-line strength} · {i18n:get_key}: {free channel} · {badge}
2) …   (3–5 lines total)
```

**Beginner persona → "free entries"** (打开就能用的入口，不谈模型榜):

```
1) {product} — {它最擅长什么，一句人话} · {i18n:get_use}: {网页/手机App} · {badge}
2) …   (3 lines)
```

**Delivery-form rule (both variants, non-negotiable).** The "get" verb must
match the evidence — {i18n:get_use} for sign-in products, {i18n:get_key} ONLY
where an API free tier was verified for that exact platform
(`deal-hunting.md` §1 gate + §3.3). A product whose APP is free but whose API
is not (DeepSeek, verified 2026-09-05) must never wear get_key wording.

Four disciplines:
1. **Safety is the gate.** Only models/products reachable through 🟢/🟡
   channels; a 🔴 channel never feeds the shortlist, however strong.
2. **Free first, strength second.** Free access first; strength decides the
   order among those; low-cost options may follow, clearly priced.
3. **Strength by evidence, not fame.** Quality claims come from live-fetched
   leaderboards (Artificial Analysis, LMArena/Chatbot Arena, LiveBench) or
   recent coverage — each with an as-of date. No fresh evidence → say
   "free to use" and make no strength claim. A single-source entry makes no
   strength claim at all.
4. **Never cached.** Model versions turn over fast; rebuild the shortlist
   from this run's evidence every time.

5. **EMPTY-TIMEPOINT fallback (graceful no-increment week).** When the radar
   probe (`deal-hunting.md` §2.6) returns no new platform AND no promo AND no
   model/price change in the last 7 days, never leave the increment promise
   silent or fabricate one. Do all of: (a) state it plainly in the first
   short sentence — 近 7 天无新平台、新活动或调价，本轮聚焦当前最强 free/cheap
   实时短名单 (or {i18n:hot_alt_note}); (b) the shortlist itself still ships
   with THIS-run verification (✓/~/⚠), never stale cache — a secondhand
   costume of "stability" earns no ✓; (c) the leaderboard as-of date appears
   next to strength figures as usual; (d) end with the standing invitation
   that a later run (or /scan schedule) may catch the next window. Increment
   value is industry-cadence-dependent: a quiet week ships verified
   current-best, not fabricated news.
6. **NEW badge (time-point increment, ≤7 days).** An entry carries the
   {i18n:new_badge} flag only when ALL hold: (a) it was cross-confirmed
   (G1/G1.5) THIS run; (b) its cache row carries a `discovered_on` ≤ 7 days
   before today (`vendor-cache.md` schema 4) — a null/missing date NEVER
   earns the badge; (c) first-ever run of an install (no cache baseline) shows
   no NEW badges at all — nothing is "new" without a baseline. The badge is a
   **tie-break and a flag, never a rank boost**: only among entries already
   equal on tier, evidence-confidence, and score within ±1 does a NEW entry
   list first; it never lifts an entry into the shortlist or above a stronger
   non-NEW pick, and hype alone can never trigger it.


**best_pick eligibility (the {i18n:best_pick_headline} line and the close's
{best} slot).** The pick must pass ALL three, or it is not the pick:
① wears {i18n:badge_official} or {i18n:badge_cross} — a single-source ⚠ row
can NEVER headline (the "尼日利亚区单源价上头条" defect); ② actionable for
this user's region + payment/network reality; ③ is one of the numbered cards
— the "回复编号" CTA must be answerable by the headline's own pick.

---

## 1.2 Scenario → pick table (speak the user's situation, return hunting order)

Beginner users don't say "C2" or "module ①" — they describe their situation.
When intake (§0.5) matches a row, jump-start the hunt with the mapped module
+ registry classes. **This table maps a HUNTING ORDER, not an answer** — final
cards still come from this run's live verification (F4), and only ①②③ module
labels are ever shown to users (C1–C7 IDs are internal).

| User says (zh / en) | Module first | Hunt these registry classes first | Why this row exists |
|---|---|---|---|
| “写代码/搭 agent 要便宜 API” / "cheap API for coding" | ① | C2 dedicated rows → C1 GPU clouds | coding needs a stable free-tier API, not a chat app |
| “不想折腾，打开就能用” / "just let me try AI" | ② | C7 app-bundled | sign-in-and-use beats key setup for beginners |
| “国内直连就行” / "must work from CN" | ①+② | C3 → C7 | reachability gate first (`deal-hunting.md` §3) |
| “长期大量用，怎么最省” / "heavy daily use, cheapest" | ③ | C6 memberships (② free baseline alongside) | plans/region deals beat per-token at volume |
| “学生，没钱” / "student, broke" | ②→① | C7 → C2 free tiers | entry products first, key route second |
| “数据不能出欧盟” / "EU-hosted only" | ① | C2 EU-hosted rows (e.g. Kluster) | hosting-region filter before price |
| “免费额度老撞限流” / "keeps hitting rate limits" | ① | C2 caps column → provider rotation | rotate free providers instead of paying |

Rules: ① rows are additive intake hooks — the three-module gate
(`deal-hunting.md` §1) still runs; ② a row never feeds a card directly — the
shortlist (§1.1) and best_pick (§1.1) rules apply unchanged; ③ if intake
matches NO row, hunt by the default mode router (SKILL.md) as today.

---

## 2. FULL — three modules back to back

Header block:

```
{i18n:title} · {i18n:as_of=date} · sources inline
{i18n:coverage_line}
{i18n:scope_api|scope_member|scope_both|scope_free_use} · {i18n:region}
{i18n:best_pick_headline} {the single best current pick — never bury the winner; must pass §1.1 eligibility}
```

After the header: the shortlist (§1.1), then the three modules — expert order
①→②→③, beginner order ②→①→③ (§0.5).

**Module ① — {i18n:module_api_title}** (register → API key → wire into a
tool): ranked cards per §4, 4–8 candidates. Every row carries a real link
+ as-of date. Delivery-form discipline: only platforms with a verified API
free tier / low-cost access belong here, and only they may use
{i18n:get_key}.

**Module ② — {i18n:module_app_title}** (sign in and use — NO key): consumer
products (DeepSeek 网页/App · 豆包 · 智谱清言 · Kimi · 腾讯元宝 · Copilot Free
· Gemini CLI …), 3–6 cards. Each card states **per surface**
({i18n:surface_web} / {i18n:surface_pc} / {i18n:surface_app}): available?
which model VERSION is free there — newest / highest 3rd-party-ranked first,
each dated (`deal-hunting.md` §2.8)? daily cap in {i18n:human_units} for
beginners? The CTA links to the **consumer entry** (registry C7 whitelist —
chat.deepseek.com, never platform.deepseek.com when the app is what's
recommended). The same vendor may appear in Module ① with its API entry —
as a SEPARATE card, never merged (delivery-form gate, `deal-hunting.md` §1).

**Module ③ — {i18n:module_member_title}** (**any AI subscription** — chat,
image, video, audio, music, 3D · incl. region pricing and carrier bundles),
rendered in **three shelves, safest first** — the legitimate saving leads;
the grey option is an informed second choice, never the headline:

1. **{i18n:shelf_official}** 🟢 — education / annual / first-year / live promo
   windows (re-verified this run).
2. **{i18n:shelf_bundle}** 🟢/🟡 — carrier & partner bundles, eligibility
   stated (plan / region / new-customer).
3. **{i18n:shelf_region}** 🟡 — cross-region prices; region tag (🇹🇷 🇵🇭 🇵🇰 …),
   the §6 risk banner **before** any "how to", and a one-line
   {i18n:worst_case} per card (subscription cancelled / money possibly lost /
   account possibly flagged — concrete beats abstract). 🔴 only per
   `safety.md` §1 (fabricated identity, reseller middlemen).

Plus:

- Corroborate each region price across **≥2 independent sources**; a figure
  from a single listing site wears {i18n:badge_unverified}.
- **Normalize every price to USD** for side-by-side comparison, with the local
  price + code in parentheses — `≈$17.7/月 (PKR 4,999)` (`scoring.md` §0.6; the
  conversion wears {i18n:badge_converted}).
- Anywhere in the output (chat or HTML), a membership card links **only** to
  the vendor's official subscription page (registry C6 domain). Third-party
  price sites are cited as plain text + date, never as a clickable link.
- An empty shelf is stated in one line, never silently dropped.

> All three modules render when the hunt covers all targets (FULL default).
> If the user asked for only one, show it fully + one line
> ({i18n:other_module_pointer}). An empty module is stated in one line,
> never silently dropped.

**HTML report filling contract** (`assets/templates/full-report.html`):
- Fill every `{{i18n:*}}` chrome token from the user's language file — the
  template's nav chips, filter chips, eyebrow, disclaimer, close label, tier
  legend, score legend and hero-KPI labels are ALL i18n tokens; never
  hand-write chrome wording. Repeat the marked blocks (shortlist lines, cards,
  notes, glossary terms). Hero KPIs: {i18n:hero_count_label} = number of
  ranked cards THIS run (never an invented total); {i18n:hero_best_label} =
  the best pick's name.
- Shortlist source references render as **plain text + date** (no third-party
  `<a>`); the only clickable links on the whole page are official domains
  (registry whitelist).
- Every card carries the data attributes the template's filter chips rely
  on: `data-reach` (direct|proxy|na) · `data-card` (yes|no credit card) ·
  `data-tier` (green|yellow|red).
- Evidence pills use the plain-word badges (`scoring.md` §2.1); the reach
  pill uses {i18n:reach_direct} / {i18n:reach_proxy} per `deal-hunting.md`
  §3.2 (add the template's "blocked" pill style when the user's own node is
  blocked). Each card ends with a CTA button that links ONLY to the vendor's
  official page — a module ③ membership card never links to a third-party
  listing/aggregator (cite those as plain text + date); module ② cards link
  to the CONSUMER entry (C7 whitelist), never the developer console; then a
  one-phrase howto hint. Fill the `#apps` section (nav chip
  {i18n:nav_apps}) whenever module ② has candidates.
- Include the glossary: plain-word explanations of every jargon term used on
  the page — the audience is non-technical.
- The file must stay self-contained: no external fonts/scripts/CDNs, no
  storage APIs — it must open offline and print cleanly.
- **Value placeholders (non-i18n) — fill from THIS run; the page must ship
  with zero `{{…}}` left.** Run-level slots: `{{lang}}` / `{{date}}` =
  output language code / run date · `{{hero_1_v}}` / `{{hero_2_v}}` = best
  pick's name / secondary KPI value (must pass §1.1 eligibility) ·
  `{{shortlist_note}}` = shortlist line count · `{{api_count}}` /
  `{{apps_count}}` / `{{member_count}}` = card counts per module ①②③ this
  run · `{{note_title}}`+`{{note_text}}` / `{{apps_note_title}}`+
  `{{apps_note_text}}` / `{{free_alt_note_title}}`+`{{free_alt_note_text}}`
  = per-section one-line notes (empty shelf / caveats). Card-level slots
  ({{name}} {{deal}} {{score}} {{source_label}} …) follow the marked card
  block comments in the template itself.

---

## 3. COMPARE table (model-vs-platform)

| {i18n:channel} | {i18n:price}/1M out (normalized) | {i18n:speed} | {i18n:stability} | {i18n:quota} | {i18n:safety} | evidence | {i18n:for_who} | {i18n:as_of} |
|---|---|---|---|---|---|---|---|---|
| … | ~$x.xx | … | … | … | 🟢/🟡/🔴 | badge | … | date |

Under the table, one legend line: {i18n:legend_confidence}.
{i18n:compare_price_spread} across the rows; end with one
"{i18n:recommend_use_case}" line per use case.

---

## 4. Full card format (per item, all three modules)

**🥇/🥈/🥉 or 1..N — [{Name}]({official_url from `vendor-registry.md`})** · tier chip 🟢/🟡/🔴 · {i18n:chip_nocard|chip_card} · region tag if any · {evidence badge}
- **{i18n:score_total}:** {x}/10 · "估{n}维" when dimensions were N/A (anchors per `scoring.md` §1.1 keep scores reproducible; breakdown inline in FULL or on request; N/A per `scoring.md` §3 when unevidenced)
- **{i18n:for_who}:** dev→batch jobs / hobbyist / heavy chat … (one line, plain)
- **{i18n:free_label}:** this platform's **strongest free model this run**, named
  with its version, ordered by a live 3rd-party leaderboard (Artificial
  Analysis / LMArena / OpenRouter `:free`) + as-of date; availability gated by
  `deal-hunting.md` §3.3 — only if a source shows that model on THIS platform's
  free tier. Newest / highest-ranked first; never an arbitrary or stale name.
- **{i18n:surface_web} / {i18n:surface_pc} / {i18n:surface_app}:** module ②
  cards only — one line per available surface: the free model VERSION there
  (newest/strongest first, dated) + any daily cap in {i18n:human_units};
  surfaces that don't exist are omitted, surfaces that lag say so
- **{i18n:price}:** normalized per `scoring.md` §0 · **{i18n:as_of=date}**
- **{i18n:source}:** official page link / {site} {as-of date} (short, real, clickable)
- **{i18n:pros}:** ≤3 bullets
- **{i18n:cons}:** ≤2 bullets (two-sided, per `scoring.md` §4.3)
- **{i18n:get_use}:** module ② action line — "打开就能用", pointing at the
  consumer entry; NEVER {i18n:get_key} wording in this module
- **{i18n:get_key}:** module ① action line — one-line pointer to the register flow
- **{i18n:membership}:** ≈$z / 月 (地区) — module ③; normalized per `scoring.md` §0.6, official buy-page link only (no third-party href)

Keep each card **≤10 lines**; trim fields not relevant to the user's ask.
Evidence badges are the plain-word set from `scoring.md` §2 — never bare
symbols without the legend, never "(估算)/(estimated)".

> **Freshness on every line (non-negotiable):** the canonical rules are
> `deal-hunting.md` §0 (F1–F5). If a known vendor's policy can't be
> re-confirmed this run, render "{i18n:policy_changed}" — never a confident
> stale number.

---

## 5. Sort policy (hard rule)

1. **Tier first**: 🟢 → 🟡 → 🔴. The 🟢 group stays on top regardless of
   small price gaps.
2. **Within a tier**: free & high-score first, then best value.
3. **Never** place 🔴 above 🟢/🟡 merely because it is cheaper; never omit
   the risk label on a grey item. A "NEW" vendor ranks only after passing
   cross-confirmation (`discovery-sources.md` §2).
4. **No-proxy users:** when the user's network has no working proxy, prefer
   direct-reachable candidates first within each tier, and say so in one
   line (`deal-hunting.md` §3.2 item 4).

---

## 6. Safety banner (before any 🔴/🟡 "how to")

> {i18n:safety_banner}

(⚠️ {item} carries {risk} — compliance / ban / region-lock / ToS / refund.
You decide; we only inform.)

---

## 7. Pre-delivery checklist (run before EVERY hunt output)

The five **★ items are mechanically verifiable — check them FIRST**; the
rest are judgment items. (This checklist is the single authority for these
rules; golden cases and spot checks in `self-check.md` reference items here
by position instead of restating them.)

★ □ Line budgets: LIGHT ≤22 content lines; three-module FULL uses the HTML report (text hosts: §1 compact cards, ≤80 content lines)
□ Persona detected and rendering matches (§0.5); `/simple` `/pro` override honored
★ □ Every deal line: as-of date + real link + evidence badge (plain words)
★ □ Line-1 / CTA link's domain == a `vendor-registry.md` official domain; no search-result href; membership links official only; HTML shortlist sources plain-text
□ Every card carries the {i18n:chip_nocard|chip_card} chip; beginner persona shows {i18n:human_units} quotas
□ Any "model M free on platform P" claim cleared `deal-hunting.md` §3.3 (a catalog sighting this run), else not printed
□ Scores follow `scoring.md` §1.1 anchors; N/A dims annotated ("估n维"); {i18n:legend_score} present when scores show
□ Labels verbatim from i18n — no improvised synonyms, no internal jargon (契约/维度/权重/新鲜度/归一化) in user text
□ Shortlist rendered first (LIGHT & FULL); LIGHT led by {i18n:best_pick_headline}; no 🔴-channel model in it; every strength claim dated; single-source entries make no strength claim
□ Reachability tags only with §3.2 evidence (live test or ≥2 community reports); no blanket "needs proxy"; domestic not presumed direct; no jargon labels
□ Scope label matches what was actually hunted; `{region}` rendered via the display map
□ Three modules kept separate — no card/line mixes delivery forms; {i18n:get_use} vs {i18n:get_key} vs {i18n:membership} each only in its own module (DeepSeek defect guard)
□ Module ② cards state the free model version PER surface (网页/电脑/App), newest/strongest first, dated; consumer-entry links only
□ best_pick passes §1.1 eligibility (verified badge + actionable + is a numbered card)
□ Module ③ in three shelves, official discounts first; empty shelf stated; every cross-region card has {i18n:worst_case} + the §6 banner before any steps
□ LIGHT with ≥4 queries spent ONE slot on the three-state radar probe (`deal-hunting.md` §2.6: promo → change → new-provider by cache state, graceful fallback, never extra queries)
★ □ Closing = scope-matched i18n sentence + ONE {best} slot (two lines) + at most ONE disclosure line (§8.1)
□ No bare "(估算)/(estimated)" or unexplained symbols anywhere user-facing
□ Coverage line present (FULL); empty classes stated (incl. "search failed" ≠ "nothing found"), never silently dropped
★ □ Tier order respected: 🟢 → 🟡 → 🔴; no 🔴 above 🟢/🟡 on price alone
   (every {i18n:new_badge} entry: this-run cross-confirm + ≤7-day discovered_on; null date never badged — §1.1 rule 5)
□ EMPTY week handled per §1.1 rule 5 + §8.1 item 6: plain {i18n:hot_alt_note} in the lead, shortlist still THIS-run verified (never cache-warm ✓), leaderboard as-of kept, /scan invitation; no fabricated increment; UPDATED variant follows the same ≤7-day discovered_on bar
□ Unverified items labeled {i18n:badge_unverified}; stale vendors say "{i18n:policy_changed}"
□ No ✓ unless an official surface was reached this run (`deal-hunting.md` §3.1); secondhand-fed outputs carry the global disclosure line (§8.1)
□ Prices normalized per `scoring.md` §0 (memberships per §0.6, USD + local in parens); estimates flagged via badge, not jargon
□ No number printed from registry/cache without this run's live verification
□ Persistence hard gate: the cache write happened BEFORE composing the send; "未持久化" is only allowed with a concrete reason (host read-only / nothing cross-confirmed / write error) — a bare "not persisted" fails
□ Disclosure line (§8.1): cache state (with reason if not persisted); ≤1 promo note; dropped candidates mentioned in a phrase

Golden regression cases: `references/self-check.md`.

---

## 8. Confirm-and-act close (mandatory follow-up, ONE clear ask)

After the module(s), drive the user to **pick one** and let the skill execute
the next step — never leave it as a passive menu.

> Line 1 = the variant matching the best pick's **delivery form**:
> **{i18n:footer_next}** (API key) · **{i18n:footer_next_use}** (login-and-use
> product) · **{i18n:footer_next_member}** (membership)
> **{i18n:footer_escape}**

Rules: exactly **two short lines — slot system.** Line 1 = the delivery-form-
matched fixed i18n sentence with ONE slot: {best} = the top pick's name (≤8
chars); no other additions or rewording — if none of the three variants fits,
that is a spec bug to report, not a license to improvise. Line 2 = the escape
hatch in plain words ("find me more options" / "cheap memberships") — these
natural phrases are registered triggers in the SKILL.md router, so no
commands need to be taught. If the user's message already implies clear
intent, skip the menu and execute directly. When the user confirms a pick,
immediately load `auto-register.md` (API key), the module-② product's
sign-up hand-holding (`auto-register.md` §4 with {i18n:get_use} framing),
`buy-membership.md` (membership), or the matching `agents/*` doc and run it —
no further stalls. If browser automation is missing, `capability-check.md`
first, then hand-hold.

### 8.1 The ONE disclosure line (the only thing allowed after the close)

Exactly one short line, carrying in order (omit empty parts):

1. **Cache state** — what was persisted this run; if nothing was, a CONCRETE
   reason is mandatory (host read-only / nothing cross-confirmed / write
   error). A bare "未持久化" with no reason is a checklist failure (§7).
2. **Global freshness disclosure** — when no official page was reached this
   run: "官方页本轮未能打开，数字来自多家第三方一致口径" (this replaces any
   per-line unreachable note; per-line notes are only for vendors whose state
   differs from the global one).
3. **At most ONE time-boxed promo** the user may care about even if it didn't
   rank (e.g. a free window for paid-plan users), with its dates and who it
   applies to.
4. **Dropped candidates in a phrase** — a queried staple that didn't make the
   cards ("Groq 本轮未上榜：节点问题依旧").
5. **Delta note (time-point increment)** — only when the cache has a baseline
   (`updated_on` non-null): one short clause — X new platform(s) confirmed this   run since {updated_on} / no new platforms since {updated_on}. First run
   (null baseline): say "first scan, no baseline" — never fabricate a delta.
6. **Hot-alt fallback (empty week per §1.1 rule 5).** When the radar probe
   found no new platform, promo, or change in 7 days: the delta note reads
   {i18n:hot_alt_note} — stating plainly that nothing changed in the last 7
   days, while the shortlist ships freshly verified (this-run ✓/~/⚠, never
   stale cache) with leaderboard as-of dates; close with the standing note
   that a later run (or /scan) may catch the next window. Never dress up a
   stable pick as news, and never fabricate an increment.

Nothing else joins the output; `/help` carries the rest.
