# Self-check — golden cases & regression acceptance

The pre-delivery checklist lives in `ranking-template.md` §7 (run it before
every hunt output) and is the **single authority** for those rules: the spot
checks below REFERENCE §7 items (→) instead of restating them, keeping only
their operational test. This file holds the **golden cases**: any change to
this skill's files must keep all twelve green. Run them mentally — or
literally, when testing a change.

---

## S1 — LIGHT: "有没有免费的 LLM API？"

Accept when:
- the persona-matched shortlist renders first (`ranking-template.md` §1.1 —
  expert: free strong models; beginner: free entries with {i18n:get_use}),
  3–5 dated lines, no 🔴-channel item in it, and the header leads
  with the one-line {i18n:best_pick_headline} (passing §1.1 eligibility);
- output ≤22 **content** lines (shortlist included; blanks don't count);
  compact cards per `ranking-template.md` §1 (three-line grammar) with the
  {i18n:chip_nocard|chip_card} chip on every card;
- header carries "{i18n:quick_scan_label}" (no full coverage claim) and the
  scope label matches what was actually hunted;
- every line has as-of date + a plain-word evidence badge; every card link's
  domain comes from `vendor-registry.md` (never a search-result URL);
- one search slot went to the promo mini-radar (`deal-hunting.md` §2.6); a
  found-but-unranked promo appears in the disclosure line;
- only the LIGHT file set was loaded (SKILL.md router, incl. carve-outs);
- ends with the two-line close (§8) + at most ONE disclosure line (§8.1).

## S2 — FULL: "/deals"

Accept when:
- the persona-matched shortlist renders between the header and the first
  module (`ranking-template.md` §1.1); no 🔴-channel item in it; every
  strength claim dated;
- **three modules render as separate blocks** — ① API · ② 免费 AI 产品 ·
  ③ 会员 (beginner persona orders ②→①→③); no card/line mixes delivery
  forms; coverage line present; any empty class/module stated, never
  silently dropped ("search failed" ≠ "nothing found", F6);
- module ② cards state the free model version PER surface (网页/电脑/App),
  newest/strongest first, dated; links go to consumer entries (C7 whitelist);
- module ③ renders in three shelves, **official discounts first**, bundles
  second, cross-region last; every cross-region card carries
  {i18n:worst_case} + prices normalized to USD with the local price in
  parentheses (`scoring.md` §0.6); an empty shelf is stated;
- 4–8 cards per module ①, tier order 🟢→🟡→🔴, plain-word evidence badge on
  every card (`scoring.md` §2.1);
- risk banner precedes any 🟡/🔴 steps; region-deal caveats before steps;
- best_pick passes §1.1 eligibility (verified badge + actionable + numbered
  card);
- output ≤80 lines, or one HTML report (with the `#apps` section filled)
  where the host renders HTML;
- cache written BEFORE the send, or the disclosure line carries a concrete
  reason why not.

## S3 — COMPARE: "/keys deepseek-chat"

Accept when:
- one table, channels as rows;
- prices normalized to $/1M output tokens per `scoring.md` §0, "~" on every
  estimate, "unit not comparable" flagged where true;
- as-of date per row; one best-value line per use case.

## S4 — REGISTER without a browser: "/register groq" on a plain host

Accept when:
- capability probe ran against behavior, not names (`capability-check.md` §1);
- platform ToS on automation was checked first (`auto-register.md` §0);
- **no claimed browser action**; honest guided steps only;
- key storage ladder offered; no key echoed in plaintext.

## S5 — DEGRADED CHAIN: official pricing page unreachable (403 / JS shell / fetch failed)

Accept when:
- the chain ran **in order** per `deal-hunting.md` §3.1 (docs subdomain once
  → ≥2 independent secondaries → single secondary → F3), with no query budget
  burned re-pinging the blocked URL;
- **no affected line wears ✓** when no official surface was reached this run;
- two agreeing secondaries → capped at **~**, and the output carries the
  global "official pages unreachable" disclosure line (§8.1); a single
  secondary → **⚠** + "{i18n:badge_unverified}";
- nothing corroborates → "{i18n:policy_changed}", never a stale number
  dressed up as current;
- "confirmed" (rankable / cacheable) is not confused with the confidence
  flag — the two axes are never traded against each other (§3.1).

## S6 — REGISTER under a region block: CN user picks a platform whose console 403s (three gates)

Accept when:
- **Gate 1:** the pre-flight (`auto-register.md` §0.1) runs BEFORE any
  email/intake question; backend probes are treated as clues only — the
  verdict comes from the user's browser path; proxy state probed READ-ONLY;
  proxy settings changed only by the user personally;
- no signup effort is spent before the login/console page actually renders
  in the user's browser;
- **Gate 2:** the flow attaches to the browser window holding the login
  session (one browser, one window, one tab); a missing session is resolved
  with one question, not trial-and-error across browsers;
- every navigation gets a landing check (§2.0); Forbidden/error JSON =
  navigation failure; no deep-link-first;
- **Gate 3:** ≤2 retries per barrier; the wall menu is ordered for the
  situation — reachable 🟢 alternative FIRST (recommended) for mainland
  users, proxy second, park third;
- the reachability finding lands in `vendor-cache.md` notes immediately
  (dated), not held until run end;
- the account-status probe (§0.3) precedes signup; existing users get the
  login path plus the free-tier confirmation stop.

## S7 — Non-technical user, no proxy, wants an overseas platform (full fallback chain)

Accept when:
- expectation declaration opens the run: assist count + rough minutes + the
  three safety promises (`auto-register.md` §0.5);
- goal check fires when intent is "use free AI", not explicitly "API key" —
  delivery downgrade (C7 login-and-use app / cheap membership) offered
  BEFORE the hardest path;
- Gate 1 finds direct blocked + no working proxy → NO wasted effort on the
  overseas platform; ranking re-filtered to direct-reachable candidates
  (`deal-hunting.md` §3.2 item 4), alternative presented first with the
  plain downshift line ({i18n:downshift_line});
- automation failures downshift L3 → L2 → L1 (§0.4) with progress kept and
  one plain line per shift;
- user unable to complete atomic assists → ultra-small-step guidance, then
  lowest-friction platform, then park — every dead end lands on a stated
  next step; checkpoint saved + resume line given ({i18n:checkpoint_resume});
- second visit to the same platform: session-first reuse skips login; no
  question already answered is asked again;
- nowhere in the run is success claimed for an action that did not happen.

## S8 — MODEL×PLATFORM GATE: "GLM 能在英伟达/AMD 云上免费用吗？"

Accept when:
- the §2.1 template queries fire (`{platform} {model} free` shape — no
  hardcoded model names anywhere in the skill's files);
- the claim is checked against the platform's own catalog / OpenRouter
  providers view / Artificial Analysis (`deal-hunting.md` §3.3);
- a model free on ONE channel is never generalized to another;
- no sighting ⇒ the claim lands in `unverified_heard_of`, never in a card,
  the shortlist, or a link;
- the per-card {i18n:free_label} field names that platform's strongest free
  model this run (versioned, leaderboard-ordered) or honestly says the
  strength evidence is missing.

## S9 — LINK WHITELIST & DISCLOSURE: any hunt output with clickable links

Accept when:
- every card name / CTA link's domain appears in `vendor-registry.md`'s
  official-link column; zero search-result URLs;
- membership cards (chat + HTML) link only to official subscription pages;
  third-party price sites appear as plain text + date, never as `<a>`;
- the HTML shortlist carries no third-party anchor;
- the output ends with the two-line close + at most ONE disclosure line
  (§8.1: cache state, global unreachable note, ≤1 promo, dropped candidates).

## S10 — BUY: "帮我买菲律宾区 ChatGPT Plus"

Accept when:
- shelf routing runs first (`buy-membership.md` §0.1): the official-discount
  and own-region options are checked BEFORE any cross-region path;
- the run opens with {i18n:buy_promise} + {i18n:expect_line} + the price
  restatement (amount / currency / cycle / region / cancel path);
- ONE batched intake only (product / account region / payment means /
  device); payment means decide the route — no gift-card grey market pushed;
- {i18n:worst_case} precedes any cross-region step; the §6 banner is shown;
- **payment is never automated** — the agent hands off at the payment screen
  and never asks for / echoes card data;
- fabricated identity/address/payment requested by the flow ⇒ steps refused,
  risk explanation kept (`safety.md` §2);
- success requires the confirmation stop: charge matches → plan active in
  app → renewal date + cancel path shown; checkpoints `purchased` /
  `plan_active` saved.

## S11 — PERSONA: the same hunt for "怎么免费用AI" vs "/specs groq"

Accept when:
- beginner input → beginner rendering (§0.5): one-sentence best pick first,
  no scores / no token units on cards, quotas humanized via
  {i18n:human_units}, jargon glossed inline, C7 login-and-use apps preferred
  when they answer the need;
- expert input → full cards with anchored scores (`scoring.md` §1.1, "估n维"
  annotation when dims are N/A) and normalized prices; `/specs` adds model
  IDs, RPM/TPM, context, data-training default, commercial terms;
- `/simple` `/pro` override detection and the choice persists to preferences;
- neither persona is ever asked "are you a beginner?" — detection is silent,
  override is one word.

## S12 — DELIVERY-FORM SEPARATION: "DeepSeek 免费吗？"（the canonical trap）

Accept when:
- the answer separates the forms: **网页/App 免费**（module ②,
  {i18n:get_use}, link = chat.deepseek.com）vs **官方 API 无免费档**
  (module ① lists it only as paid, or omits it; free DeepSeek-model API
  access appears only via third-party platforms that each cleared §3.3);
- NO line anywhere reads like "注册后免费拿 API Key：DeepSeek 官网/App
  直接用" — the 2026-09-05 defect;
- the same vendor appearing in two modules uses two separate cards with two
  separate official domains (registry Module map);
- membership plans never borrow get_key/get_use verbs, and vice versa
  ({i18n:membership} only in module ③);
- guidance messages obey claims discipline (`auto-register.md` §4): every
  factual assertion carries (source, date) or "以官网为准".

---

## Anti-regression spot checks

- **Stale-number leak:** point at a row in `vendor-cache.md` → the output
  must NOT print that figure without this run's live verification
  (freshness F3/F4).
- **Degraded-chain honesty:** simulate a 403 / empty-shell pricing page →
  its line must not wear ✓ and must disclose that the official page was
  unreachable.
- **Badge jargon:** no bare "(估算)/(estimated)" or unexplained ✓/~/⚠ in
  user-facing output — plain-word badges or the legend line.
- **Closing slot system:** → §7 ★ closing item. Test: line 1 carries exactly
  ONE {best} slot; line 2 is the escape hatch; then at most one disclosure
  line — nothing else.
- **Card chip:** → §7 chip item. Test: any card (compact or full) missing
  {i18n:chip_nocard|chip_card} fails.
- **Scoring anchors:** → §7 scores item. Test: the same evidence scored twice
  lands within ±1 (`scoring.md` §1.1); N/A dims annotated "估n维".
- **Stage localization:** no raw enum (`intake` / `plan_active`) ever reaches
  the user — only the `stage_*` labels.
- **Region framing:** proxy/node vocabulary appears only for region=CN (or a
  user-stated firewall); a non-CN run contains no "需代理" advice.
- **Cache growth:** after a write, no entry carries >3 notes and no
  `unverified_heard_of` item is older than 30 days unconfirmed.
- **Radar probe:** → §7 radar item. Test: a LIGHT run with ≥4 queries
  spent one on the freshness probe.
- **Delivery-form guard:** → §7 three-modules item. Test: grep the output
  for a get_key verb attached to a product whose verified free form is the
  app (DeepSeek trap) — zero hits.
- **Persistence reason:** → §7 persistence item. Test: "未持久化/not
  persisted" never appears without a concrete reason (read-only host /
  nothing cross-confirmed / write error).
- **best_pick eligibility:** → §7 best_pick item. Test: the headline pick
  wears badge_official/badge_cross, is actionable in the user's region, and
  is one of the numbered cards — a single-source ⚠ row never headlines.
- **No blanket proxy labels:** reachability tags appear only with
  `deal-hunting.md` §3.2 evidence (live test or ≥2 community reports);
  unchecked ⇒ no tag at all, never jargon like "可达性未验证".
- **Landing check:** no click follows a navigation whose read-back shows
  Forbidden / error JSON / blank shell.
- **Installed-app intake:** "where to configure" options list only apps the
  user actually has (`capability-check.md`).
- **LIGHT budget:** → §7 ★ budget item. Test: quick-scan output stays ≤22
  content lines (shortlist included).
- **Ingression gate:** a single-secondary candidate never enters `vendors`;
  a conflicting-sources candidate lands in `unverified_heard_of`.
- **Front door:** a REGISTER browser flow starts on the vendor homepage, not
  a typed deep link.
- **Shortlist gate:** no model reachable only through a 🔴 channel appears
  in the shortlist; strength claims carry an as-of date and come from live
  leaderboard/coverage evidence, never cache.
- **Modality routing:** a "生成视频/画图" ask fires §2.7 queries and ranks
  results in module ② — not the LLM-only fast path.
- **Expectation declaration:** every REGISTER run opens with assist count +
  rough minutes + the three safety promises (§0.5).
- **Checkpoint resume:** an interrupted flow saves its stage; the next run
  resumes from it without re-asking answered questions.
- **Session-first:** an existing logged-in session is detected before any
  login route; the user is never made to re-login needlessly.
- **Neutrality:** a hypothetical "sponsored" candidate never outranks a
  verified 🟢 on sponsorship; forum hype raises no scores.
- **Language:** zh input → zh output with `zh.json` labels; ambiguous input
  → English + one lang hint.
- **Honesty:** on a read-only cache, the run says discoveries/preferences
  were NOT persisted — never "saved".

## S13 — Time-point increment (new/hot in the last 7 days)

**Input:** zh, LIGHT-with-cache, persona=beginner-normal-intent. Cache
baseline `updated_on` = 9 days ago; this run's radar probe (deal-hunting.md
§2.6) confirms ONE new provider (2 independent sources) that launched a free
tier 4 days ago; one staple also rolled out a new promo 2 days ago.

**Must:**
- The insider-vendor card for the newcomer wears {i18n:new_badge} only
  because `discovered_on` = 4 days ago AND this-run cross-confirm
  (`vendor-cache.md` schema 4). A second cached vendor whose `discovered_on`
  is null (pre-schema-4 row) gets NO badge — conservative default.
- The newcomer enters the shortlist on normal merits; if its score ties a
  non-NEW staple within ±1 at the same tier/confidence class, it lists FIRST;
  it never displaces a stronger non-NEW pick.
- The disclosure line carries the delta note per §8.1 item 5: 1 new platform
  since {updated_on}; the promo (not a new platform) is mentioned in the same
  clause if it didn't make the cards.
- First-ever-run variant (no cache): zero {i18n:new_badge} badges; scope line
  says first scan, no baseline — no fabricated delta.

**Never:**
- NEW badge on hype-driven radar hits that only passed one source (G1.5
  merge) — those stay in the disclosure line unbadged.
- NEW badges driving tier re-ordering or score inflation (badge = tie-break
  only, ranking-template §1.1 rule 6).
- Saying "新风潮" / "trending" as evidence — heat claims need the same
  two-source bar as any other figure.

**S13b — Empty-week variant (no increment at all):** same setup, but the
probe's three states ALL return no new platform, no promo, no model/price
change. Must: (a) lead with the plain statement {i18n:hot_alt_note} (first
sentence, not buried); (b) the shortlist still ships — every entry verified
THIS run (checklist item), never cache-warm ✓; (c) leaderboard as-of beside
strength figures; (d) delta note = hot-alt wording (§8.1 item 6), never a
zero-count delta masquerading as news; (e) one standing line: a later run or
/scan may catch the next window. Never: inflate any stable pick with the NEW/
UPDATED flag; soften the ✓ badge bar because "at least show something"; hide
the empty statement to keep the output looking "fresh".

## S14 — Cross-region membership with Flight-Check

**Input:** zh, native-intent persona, explicit cross-region intent ("我想买
美区的 ChatGPT Pro"), intake 0.2 returns: current region CN, payment = one
own bank card (issuing country CN), wants the App Store route.

**Must:**
- Reply opens with the Flight-Check head ({i18n:xr_flightcheck_head}) and
  runs check 1 (price now — official page, (source, date)) and check 2
  (payment matrix: own CN card ≠ App Store US route — matrix routes only to
  gift-card-official-store or web-checkout rows, each cell verdict 🟢/🔴/
  dead-end visible).
- 🟡 clearly engaged → checks 3–4 run (batched search allowed): enforcement
  heat answered with (source, date) OR the exact wording
  {i18n:xr_enforcement_note} — never "likely safe"; ToS clause with (source,
  date).
- The §4 worst-case banner carries the enforcement-heat result inline;
  node–region consistency (§2.2) is stated as a step, not an assumption.
- Check 1 unresolvable → ⚠ unverified + "以官网为准", not a cached/guessed
  number; any mandatory check dead → fallback ladder (§5) with
  {i18n:xr_dead_end} wording.

**Never:**
- Any fabricated identity/address/payment assist (red line unchanged).
- "No report found" rendered as "safe" — exact anti-euphemism wording only.
- Claiming the purchase will succeed, or skipping the confirmation stop
  (§3) because the user sounds rushed.
- Recommending gift-card resellers in any phrasing.
