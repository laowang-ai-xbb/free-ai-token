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
**Module order — numbering discipline (v2.9.6):**
- **FULL three-module output (numbered modules, the standard artifact):**
  modules render in **FIXED order ① → ② → ③** — always. The ①②③ are
  **stable module IDs** (`SKILL.md`: "one meaning in every file") and
  numbered sections must read in ID order, otherwise readers see "Module ②"
  before "Module ①" and the numbered contract breaks. **Persona does NOT
  reorder modules in FULL output.** Persona care moves to four other
  surfaces (none of which disturb the numbered order):
  1. **Hero best_pick** (§2) — beginner still gets a no-key best pick on top.
  2. **Shortlist order** (§1.1) — beginner ②→①→③, expert ①→②→③.
  3. **Module ② sec-sub lead-in** — "不想折腾，从这一节开始" type line for
     beginner, no module reorder.
  4. **Nav chips** — emphasis on the recommended entry point.
- **LIGHT plain-text chat output (unnumbered, three-line cards):** persona
  order still applies — beginner ②→①→③, expert ①→②→③ — because there is
  no numbered section to break.

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

## 1.1 Shortlist — three seats, one per delivery form (v2.9.6)

The shortlist is the page's most-trusted slot: first content block, first
nav chip, sits next to the best_pick hero. It must show the **full breadth
of the skill's three delivery forms** (① API · ② product · ③ membership) —
not just one form, however strong. Persona shapes the *order* and *wording*
of the three seats, never their *presence* or *count*.

**Three seats — each renders a different delivery form:**

| Seat | Delivery form | Verb | Form chip | Empty-handling |
|---|---|---|---|---|
| A | ① API (free / low-cost key) | {i18n:get_key} | {i18n:form_chip_api} | drop the seat, render a one-line "本轮暂无 ① 通过交叉核实的免费 API" — never fill with a ②/③ entry silently |
| B | ② Free product (sign-in-and-use) | {i18n:get_use} | {i18n:form_chip_app} | same: state plainly, never merge with another seat |
| C | ③ Membership / time-boxed deal | {i18n:membership} | {i18n:form_chip_member} | render the one-line {i18n:empty_member_seat} note; never fill with a stale deal |

**Persona-conditioned order (render order of the three seats):**

- **Beginner** → B → A → C. Humanized quotas via {i18n:human_units};
  no model-name tables; C seat only renders if a time-boxed / no-code
  membership is found (beginners prefer the no-key path).
- **Expert** → A → B → C. Model names + rate limits; C seat always
  present if any membership deal cleared the bar.

**Discipline per seat (the existing §1.1 gates, applied per-seat):**

1. **Safety is the gate.** Every seat picks from 🟢 / 🟡 channels only;
   a 🔴-channel item never enters any seat.
2. **Free first, strength second.** Free access first; strength decides
   order within a tier; low-cost options may follow, clearly priced.
3. **Strength by evidence, not fame.** Quality claims come from a live
   leaderboard (Artificial Analysis / LMArena / OpenRouter `:free`)
   with an as-of date. No fresh evidence → "free to use" and no strength
   claim.
4. **Never cached.** Rebuild the shortlist from THIS run's evidence.
5. **EMPTY-timepoint fallback** (`{i18n:hot_alt_note}`) — same as before.
6. **NEW badge** discipline — same as before (this-run cross-confirm +
   `discovered_on` ≤ 7 days, tie-break only).
7. **Form-blending guard (v2.9.6).** A seat's `get_*` verb and free-tier
   facts must match its delivery form:
   - Seat A may cite an API free tier (RPM/RPD/TPM), may NOT cite
     consumer-app features.
   - Seat B may cite the app's free model, may NOT cite API-side gifts
     (e.g. a 智谱清言 seat must not carry "2000 万 tokens 礼包" — that is
     BigModel/①'s gift, not 清言's; the canonical 2026-09-05 defect).
   - Seat C may cite price / promo window, must carry its end-date.

**HTML template rendering** (v2.9.6): each `<li>` carries the seat's
form chip (`<span class="form {{form}}">{{i18n:form_chip_*}}</span>`)
between rank and name. The single `{{i18n:shortlist_title}}` value from
`zh.json` / `en.json` covers the title for both personas.

**best_pick eligibility** — unchanged from v2.9.5: the pick must wear
{i18n:badge_official} or {i18n:badge_cross}, be actionable for the user's
region + payment/network reality, and be one of the numbered cards. The
2026-09-05 defects (single-source ⚠ row on top, DeepSeek-form-blending)
still fail.

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

After the header: the shortlist (§1.1, three seats — one per form), then the
**three modules in FIXED order ① → ② → ③** (§0.5). Persona's job is done
by the hero / shortlist order / module-② sec-sub / nav — NOT by reordering
the numbered modules.

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
2. **{i18n:shelf_bundle}** 🟢/🟡 — partner bundles: telecom carriers · banks
   (credit-card perks) · payment platforms (Alipay/WeChat/UnionPay
   campaigns) · device makers · broadband / retail memberships. Eligibility
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
  notes, glossary terms). Hero KPIs: {i18n:hero_count_label} = **exact sum of
  the three module counts this run** (`{{api_count}}` + `{{apps_count}}` +
  `{{member_count}}`); count AFTER composing all cards, BEFORE writing the
  hero, so the two never disagree (the v2.9.5 "23 vs 25" defect); {i18n:hero_best_label}
  = the best pick's name.
- Shortlist source references render as **plain text + date** (no third-party
  `<a>`); the only clickable links on the whole page are official domains
  (registry whitelist). **v2.9.6:** the rule extends to `<button>`-styled
  "ghost" CTAs — a third-party price tracker may never appear as a
  clickable element (the v2.9.5 subprice.org / opentherank.com defect);
  use the template's `.srcref` plain-text style for "参考来源" notes.
- Every card carries the data attributes the template's filter chips rely
  on. **v2.9.6 anti-ambiguity:** the `data-nocard` attribute replaces the
  ambiguous `data-card` — values are `yes | no` where `yes` = "no credit
  card needed" (the attribute's value matches the filter's predicate in
  the template: `c.dataset.nocard === 'yes'` → shown under
  {i18n:filter_direct}'s sibling chip "免信用卡"). Pills and data
  attributes must agree: a card displaying {i18n:chip_nocard} must carry
  `data-nocard="yes"`, displaying {i18n:chip_card} must carry
  `data-nocard="no"` — checklist item, no exceptions (the v2.9.5 module-②
  "missing chip + inverted value" defect). `data-reach` values: `direct |
  proxy | na` — a card with no live reach evidence carries `data-reach="na"`
  and **NO reach pill** (never the improvised "可能需要工具" euphemism —
  the no-tag rule from §1 + the self-check anti-regression line are binding).
- Evidence pills use the plain-word badges (`scoring.md` §2.1); the reach
  pill uses {i18n:reach_direct} / {i18n:reach_proxy} per `deal-hunting.md`
  §3.2 (add the template's "blocked" pill style when the user's own node is
  blocked). Each card ends with a CTA button that links ONLY to the vendor's
  official page — a module ③ membership card never links to a third-party
  listing/aggregator (cite those as plain text + date); module ② cards link
  to the CONSUMER entry (C7 whitelist), never the developer console; then a
  one-phrase howto hint. Fill the `#apps` section (nav chip
  {i18n:nav_apps}) whenever module ② has candidates.
- **Radar finds without an official domain (v2.9.6).** A radar-discovered
  vendor with no `vendor-registry.md` official entry MUST render as plain
  name + a textual access path ("入口：App 内领取" / "via 灵犀·晓伴 App"),
  NEVER as a news / aggregator / third-party URL CTA (the v2.9.5
  stdaily.com-as-CTA defect). If a single news article is the only
  evidence, that is corroboration, not an entry point — do not promote
  it to `<a>`.
- **Card numbering is global (v2.9.6).** Rank numbers are 1..N across the
  whole report in render order (① then ② then ③), never per-module
  restarts. The "回复编号" CTA in the close line (§8) must be answerable
  for the best pick's exact rank without ambiguity (the v2.9.5
  three-modules-all-starting-at-1 defect).
- **Slot values never carry braces (v2.9.6).** Every `{slot}` filled from
  an i18n string substitutes a clean value, no braces around it:
  `{risk}`→`合规/封号/退款`, never `{合规/封号/退款}`. The only braces on
  the finished page are template placeholders that have ALL been replaced
  (zero `{{…}}` and zero unpaired `{…}` left). User-facing output must
  never contain raw `{i18n:…}` or `{slot}` syntax (the v2.9.5 banner
  `{合规/封号/退款}` defect).
- **Footer attribution (v2.9.6).** Fill from `assets/branding.md` (the
  single source of truth for author / repo / license / version / star
  CTA). The template's footer block is filled with: author line
  {i18n:author_credit} + repo CTA {i18n:repo_cta} linking to `{{repo_url}}`.
  This block is part of the template (single-file, offline-friendly) and
  must NOT be removed by hosts that want "cleaner footers" — it is the
  provenance the product carries when shared / screenshotted.
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
  = per-section one-line notes (empty shelf / caveats) · `{{repo_url}}` /
  `{{skill_version}}` = attribution values from `assets/branding.md`.
  Card-level slots ({{name}} {{deal}} {{score}} {{source_label}} …) follow
  the marked card block comments in the template itself; rank uses the
  **global** number 1..N as above.

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
★ □ Module render order in FULL is ① → ② → ③ (FIXED; persona does NOT reorder numbered modules — §0.5)
★ □ Shortlist is three seats (one per delivery form); persona shapes order/wording only; no seat is silently filled with another form's evidence; empty seats render a one-line honest note (§1.1)
★ □ Hero KPI count == api_count + apps_count + member_count for this run (count AFTER composing, BEFORE writing hero — the v2.9.5 "23 vs 25" defect)
★ □ Card rank numbers are global (1..N across modules); the "回复编号" CTA can be answered without ambiguity
★ □ Card data attributes match visible pills: `data-nocard="yes"` ↔ {i18n:chip_nocard} pill, `data-nocard="no"` ↔ {i18n:chip_card} pill; module ②③ cards missing the chip fail (v2.9.6)
★ □ Every reach pill has live evidence; no improvised "可能需要工具" / "可达性未验证" reach labels — no-tag = no evidence is the rule (§1 + self-check anti-regression line)
★ □ Slot values never carry braces; no `{slot}` or `{i18n:…}` syntax reaches the user (v2.9.6)
★ □ No third-party domain renders as a clickable element anywhere (no `<a>`, no `<button>`-styled CTA); "参考来源" notes use the template's `.srcref` plain-text style
★ □ Radar finds without a registry official entry render as plain name + textual access path (no news/aggregator URL as CTA)
★ □ Footer attribution block is present (author credit + repo star CTA) and filled from `assets/branding.md` — never stripped by hosts
★ □ Person detected and rendering matches (§0.5); `/simple` `/pro` override honored
★ □ Every deal line: as-of date + real link + evidence badge (plain words)
★ □ Line-1 / CTA link's domain == a `vendor-registry.md` official domain; no search-result href; membership links official only; HTML shortlist sources plain-text
★ □ Every card carries the {i18n:chip_nocard|chip_card} chip; beginner persona shows {i18n:human_units} quotas
★ □ As-of dates are day-level (YYYY-MM-DD); month/year-only evidence dates are flagged (e.g. "2026-06 · 来源粒度：月") or upgraded
★ □ Module-end `note` blocks obey the same freshness contract as cards — no numbers without an as-of date
★ □ Any "model M free on platform P" claim cleared `deal-hunting.md` §3.3 (a catalog sighting this run), else not printed
★ □ Scores follow `scoring.md` §1.1 anchors; N/A dims annotated ("估n维"); {i18n:legend_score} present when scores show
★ □ Labels verbatim from i18n — no improvised synonyms, no internal jargon (契约/维度/权重/新鲜度/归一化) in user text
★ □ Shortlist rendered first (LIGHT & FULL); LIGHT led by {i18n:best_pick_headline}; no 🔴-channel model in it; every strength claim dated; single-source entries make no strength claim
★ □ Reachability tags only with §3.2 evidence (live test or ≥2 community reports); no blanket "needs proxy"; domestic not presumed direct; no jargon labels
★ □ Scope label matches what was actually hunted; `{region}` rendered via the display map
★ □ Three modules kept separate — no card/line mixes delivery forms; {i18n:get_use} vs {i18n:get_key} vs {i18n:membership} each only in its own module (DeepSeek defect guard)
★ □ Module ② cards state the free model version PER surface (网页/电脑/App), newest/strongest first, dated; consumer-entry links only
★ □ Shortlist form-blending guard: seat A (API) carries API-side facts only; seat B (app) carries app-side facts only; seat C (membership) carries price + end-date (§1.1 rule 7)
★ □ best_pick passes §1.1 eligibility (verified badge + actionable + is a numbered card)
★ □ Module ③ in three shelves, official discounts first; empty shelf stated; every cross-region card has {i18n:worst_case} + the §6 banner before any steps
★ □ LIGHT with ≥4 queries spent ONE slot on the three-state radar probe (`deal-hunting.md` §2.6: promo → change → new-provider by cache state, graceful fallback, never extra queries)
★ □ Closing = scope-matched i18n sentence + ONE {best} slot (two lines) + at most ONE disclosure line (§8.1) + for plain-text hosts, one allowed attribution line (author credit + repo CTA — see §8.2)
★ □ No bare "(估算)/(estimated)" or unexplained symbols anywhere user-facing
★ □ Coverage line present (FULL); empty classes stated (incl. "search failed" ≠ "nothing found"), never silently dropped
★ □ Tier order respected: 🟢 → 🟡 → 🔴; no 🔴 above 🟢/🟡 on price alone
   (every {i18n:new_badge} entry: this-run cross-confirm + ≤7-day discovered_on; null date never badged — §1.1 rule 5)
★ □ EMPTY week handled per §1.1 rule 5 + §8.1 item 6: plain {i18n:hot_alt_note} in the lead, shortlist still THIS-run verified (never cache-warm ✓), leaderboard as-of kept, /scan invitation; no fabricated increment; UPDATED variant follows the same ≤7-day discovered_on bar
★ □ Unverified items labeled {i18n:badge_unverified}; stale vendors say "{i18n:policy_changed}"
★ □ No ✓ unless an official surface was reached this run (`deal-hunting.md` §3.1); secondhand-fed outputs carry the global disclosure line (§8.1)
★ □ Prices normalized per `scoring.md` §0 (memberships per §0.6, USD + local in parens); estimates flagged via badge, not jargon
★ □ No number printed from registry/cache without this run's live verification
★ □ Persistence hard gate: the cache write happened BEFORE composing the send; "未持久化" is only allowed with a concrete reason (host read-only / nothing cross-confirmed / write error) — a bare "not persisted" fails
★ □ Disclosure line (§8.1): cache state (with reason if not persisted); ≤1 promo note; dropped candidates mentioned in a phrase

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

### 8.2 The ONE attribution line (v2.9.6) — author / repo, on every deliverable

The skill ships with provenance: author, repository, license, star CTA —
all from the single source of truth at `assets/branding.md`. Every output
carries this attribution so the product is discoverable when shared or
screenshotted. The HTML report's footer block is filled from the same
source; plain-text hosts add **exactly one** attribution line after the §8.1
disclosure, in the user's language:

```
{i18n:author_credit} · {i18n:repo_cta} → {repo_url}
```

Rules:
- The line is **mandatory** for every output (LIGHT, FULL, COMPARE, BUY
  reply, and any shareable artifact) — checklist item, no carve-out.
- It is the **only sanctioned addition** to the close, on top of §8.1.
  Nothing else joins the output; `/help` carries the rest.
- The {repo_url} slot comes from `assets/branding.md` — never invent a URL
  in the run. The two i18n tokens ship with the skill; missing tokens
  fall back to the English values from `en.json` per §0 rule 3, never to
  improvised wording.
- Plain-text hosts that already wrap the reply in a host-specific
  attribution footer (some chat agents) MAY omit this line, but the run
  must state the omission in the disclosure line (item 7 of §8.1, with a
  concrete reason) — silent omission fails the checklist.

Nothing else joins the output; `/help` carries the rest.
