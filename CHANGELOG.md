# CHANGELOG

One line per rule change: date — event — product. Case IDs (N16, the
2026-09-05 defect) referenced by other files resolve here.

## 2.9.6 — 2026-09-08 (provenance + rendering-purity release)

- **Attribution provenance (Wave 3).** New `assets/branding.md` is the
  single source of truth for author / repo URL / license / star CTA. The
  HTML template's footer adds an attribution block filled from that file
  (`{i18n:author_credit}` + `{i18n:repo_cta}` → `{{repo_url}}`); the
  plain-text close adds a one-line §8.2 attribution. Author = @老王AI瞎bb
  (小红书); repo = `https://github.com/laowang-ai-xbb/free-ai-token/`;
  license = MIT. Every output now carries provenance when shared or
  screenshotted — the v2.9.5 audit's "无作者署名" finding resolved. SKILL.md
  version bumped to 2.9.6; resource index gains branding.md.
- **Shortlist three seats (Wave 2 — problem 1).** §1.1 rewritten: the
  shortlist is now three seats (one API · one product · one membership),
  fixed shape, persona shapes ORDER and WORDING only, never PRESENCE.
  Empty seats render a one-line honest note (`{i18n:empty_member_seat}`),
  never a silent fill. New i18n: `form_chip_api` / `form_chip_app` /
  `form_chip_member`; the nav chip renamed to "本周精选" / "This week's
  picks" to match the new shortlist title wording.
- **Module render order fixed ①→②→③ in FULL (Wave 2 — problem 2).**
  §0.5 rule rewritten: numbered modules always render in ID order; persona
  care moves to the hero / shortlist order / module-② sec-sub / nav.
  LIGHT plain-text chat output (unnumbered) keeps the persona order.
  The "② before ①" cognitive dissonance is gone.
- **Module ③ shelf 2 broadened to partner bundles (Wave 2 — problem 3).**
  i18n `shelf_bundle` = "伙伴权益（运营商 / 银行 / 支付 / 终端）" / en =
  "Partner bundles (carrier / bank / payment / device)". `vendor-registry.md`
  C6 adds five sub-rows for partner types (carriers · bank credit-card
  perks · payment-platform campaigns · device makers · broadband/retail
  memberships). `discovery-sources.md` adds EN + CN partner-bundle radar
  queries. `buy-membership.md` §0.1 shelf routing updated; SKILL.md BUY
  mode wording and natural-language trigger wording sync.
- **P0 contract enforcement (Wave 1).** New mechanical ★ items in the
  pre-delivery checklist (§7) and 5 new golden cases S15–S20 in
  `self-check.md`:
  - S15 hero KPI == Σ of module counts (the v2.9.5 "23 vs 25" defect).
  - S16 no braces leak in user-facing output (the "{合规/封号/退款}"
    defect — slot values substitute CLEAN, no braces).
  - S17 global card numbering 1..N across modules (the v2.9.5 "回复编号 1–6"
    three-modules-all-start-at-1 ambiguity).
  - S18 data-nocard attribute must match the visible chip (the v2.9.5
    module-②③ missing-chip defect) — the attribute is renamed from the
    ambiguous `data-card` to `data-nocard` (yes = no credit card needed)
    to remove all reading-ambiguity; template filter JS, comment, and
    run-contract doc all updated.
  - S19 reach no-tag rule: region-unknown + no live evidence → no reach
    pill, never the improvised "可能需要工具" / "可达性未验证" euphemism
    (which the no-tag rule already forbids — S19 makes the rejection
    explicit and adds a golden case).
  - S20 attribution provenance on every output.
- **Other rendering hardening (also ★ items).** Third-party price trackers
  may never appear as a clickable element (no `<a>`, no `<button>`-styled
  ghost CTA — the v2.9.5 subprice.org / opentherank.com defect); template
  adds a `.srcref` plain-text style for "参考来源" notes. Radar finds
  without a registry official entry render as plain name + textual access
  path (the v2.9.5 stdaily.com-as-CTA defect). Card rank numbers are
  global across modules. Display-level dates are day-level
  (YYYY-MM-DD); month/year-only evidence is flagged. Module-end `note`
  blocks obey the same freshness contract as cards (no numbers without
  an as-of date).
- No new files except `assets/branding.md`; no schema change. S1–S14
  acceptance items updated to match (S2 fixed-order rule, S9 link
  whitelist hardening, S12 form-blending guard referencing §1.1 rule 7).

## 2.9.5 — 2026-09-07 (scenario→pick table + radar additions from competitive scan)

- ranking-template §1.2 scenario→pick table (pattern borrowed from awesome-free-llm-apis' decision table, rebuilt for three-module/persona architecture): intake phrases → module + registry classes = HUNTING ORDER only; C-IDs stay internal, §1.1/best_pick rules unchanged, no-row default = mode router.
- vendor-registry C2: +6 dedicated rows — GitHub Models, Together AI, Fireworks AI, Databricks, Kluster AI, Ollama Cloud (Together/Fireworks promoted out of the combined row). Provider list now covers 100% of awesome-free-llm-apis' table (14/14), each with live-verify questions instead of hard-coded facts.

## 2.9.4 — 2026-09-06 (cross-region Flight-Check: live facts, payment matrix, enforcement heat)

- buy-membership.md §2.0 Cross-Region Flight-Check: four live checks before any 🟡 step — price now / payment feasible now / enforcement heat now / ToS clause now — each with (source, date) or a declared degrade; checks 3–4 conditional (merge into one batched search); mandatory failure routes to the fallback ladder, never silently skipped.
- §2.1 payment-means × region matrix (from intake 0.2): every common means mapped to App Store / web routes with 🟢/🔴/dead-end verdicts; red line unchanged (no identity fixes by the agent).
- §2.2 node–region consistency is now an executable step at 🟡 start, not a passive requirement.
- safety.md §4: the static worst-case banner now carries the time-stamped enforcement-heat result; "no public report found" must NEVER be worded as safe ({i18n:xr_enforcement_note}) — absence of evidence ≠ absence of risk.
- i18n: 8 new xr_* tokens (en/zh). Self-check adds golden case S14. No new files, no schema change, prohibited-acts list untouched.
## 2.9.3 — 2026-09-06 (empty-week fallback: no-increment UX)

- Radar probe → three-state delta (deal-hunting.md §2.6): promo → change (price drop / free-tier increase / new model, can wear UPDATED variant under the same ≤7-day verified-on bar) → new-provider; graceful fallback inside the SAME single LIGHT slot, never extra queries.
- Empty-week protocol (ranking-template.md §1.1 rule 5 + §8.1 item 6): state plainly {i18n:hot_alt_note}; shortlist still ships THIS-run verified (never cache-warm ✓); leaderboard as-of kept; standing /scan invitation; never fabricate or dress up increments.
- UPDATED badge variant: known-vendor change hits may wear {i18n:new_badge} with variant wording, same discovered_on ≤7d discipline (schema 4, no new fields).
- Self-check: S13b golden case (empty-week branch); badge rule cross-ref renumbered 5→6; checklist gains the empty-week audit item. No 8th scoring dimension; cache schema stays 4.
## 2.9.2 — 2026-09-06 (time-point increment: hot/new within 7 days)

- Radar probe (deal-hunting.md §2.6): the LIGHT promo mini-radar is now a time-point delta probe — promo XOR new-provider chosen by cache state (≥4-query budget unchanged). Purpose: surface what changed recently, not a fame ranking.
- NEW badge (ranking-template.md §1.1 rule 5): an entry may wear {i18n:new_badge} only with a this-run cross-confirm AND a cache `discovered_on` ≤7 days; badge is a tie-break/flag, never a rank boost; first run (no baseline) shows no badges.
- Delta note (ranking-template.md §8.1 item 5): "X new platforms since {updated_on}" only with a cache baseline; first run says first-scan-no-baseline — never fabricated.
- Cache schema 3→4 (vendor-cache.md): additive `discovered_on` field (first-seen date, survives re-verification); null/missing row never wears NEW; existing schema-3 rows keep full status (same G1/G1.5 gate). §7 checklist gains the badge-audit item.
- i18n: en/zh add new_badge + delta_note. Self-check adds golden case S13.
- Design note: deliberately NO 8th scoring dimension — heat/momentum stays an evidence+render concern (scoring §4.2 already admits it), avoiding learnability damage to the 7-dim anchor system.

## 2.9.1 — 2026-09-06 (adversarial review round: P0/P1 hardening)

- P0: G1.5 pseudo-independence guard added to the cache ingression gate (`assets/vendor-cache.md`) — same-origin sources count as ONE source. Fixes the "two citations of the same Product Hunt post" false cross-confirmation hole.
- P0: i18n fallback path added (`ranking-template.md` §0 rule 3) — en.json string → plain internal label → disclosure-line language note; raw `{i18n:…}` tokens and bare ✓/~/⚠ must never reach the user. Fixes the i18n single point of failure.
- P0: cache schema-migration rule (`assets/vendor-cache.md` "Schema migration") — schema < 3 rows demote to `unverified_heard_of`, never silently converted.
- P1: freshness F2.5 graded re-verify (`deal-hunting.md` §0) — full re-verify only for PRINTED figures; unprinted rows cap at ⚠; budget overrun routed to §3.1 instead of more re-pings. Keeps the ✓ badge intact.
- P1: product-name-only persona guard (`ranking-template.md` §0.5) — "which Claude is cheapest" stays beginner; /pro hint appended.
- P1: CN-unknown one-line caveat (`deal-hunting.md` §2.6) — zh + unknown region gets an availability note without proxy framing or region assumption.

## 2.9.0 — 2026-09-06 (goal-driven: automation + speed + global)

- LIGHT staple list made REGION-CONDITIONAL (`deal-hunting.md` §2.6): CN set vs Global set, resolved by the 2.8.0 region chain; Global set is the no-assumption default. Fixes: non-CN users received a CN-flavored default scan (source: external review, "全球" gap).
- Module-② LIGHT asks now swap the five API staples for registry C7 top-3 + radar. Fixes: the "怎么免费用AI" fast path queried zero product sources (source: external review N2).
- Expert fast lane (`auto-register.md` §0.5): returning users / expert persona get a one-line expectation declaration and L4 start when gates+ToS pass; protocol weight shrinks, safety checks do not. Source: external review, "自动化+快速" gap.

## 2.8.0 — 2026-09-06 (debt release: no new capabilities)

- Cache shipped EMPTY (schema 3, all-null preferences) — fixes the 2.7.0 defect where a fresh install silently inherited the developer's region=CN / lang=zh / no-card filter (source: external review, rounds 1–4).
- Region inference chain added to SKILL.md §“Region”: user statement > saved preference > ONE batched intake; language is a weak signal only — zh input never implies region CN.
- Module numbering unified: circled ①②③ mean module IDs (① API · ② free AI products · ③ memberships) everywhere; the SKILL.md intro now uses plain bullets for delivery forms. Fixes the 2.7.0 same-file double semantics (source: external review N1).
- FULL budget recomputed: 16 → 18 hops with an explicit allocation (7 classes ≥1 + module-② ×≥2 + radar ≤2 + verify ≤5 + retry reserve 2). Fixes: §2.8 consumer queries had no slot (F6 retries cannibalized verification).
- Three-module FULL output contract made honest: HTML report is the DEFAULT; plain-text hosts reuse the §1 compact-card grammar, ≤80 content lines. Fixes: the old "≤80 lines stacked blocks" contract was unreachable at the ≥7-card HTML threshold.
- §2.8 per-surface detail now scoped to FULL cards; LIGHT cards carry a single surface-summary line (fixes rule-vs-grammar collision).
- HTML filling contract: 8 value placeholders (apps_count, apps_note_title/text, shortlist_note, member_note, free_alt_note_title/text, member pricing) documented in `ranking-template.md` §8.2; member_note moved out of the count span.
- Scoring ease-of-use anchor reworded to "signed in & working in <5 min" (covers no-key products).
- description slimmed: behavior narrative removed, all trigger words/command names/product names kept (function split, not length cut).
- QA single-source-of-truth: `self-check.md` regression checks now REFERENCE §7 items (→) instead of restating rules; §7 checklist 27 → 26 items with the 5 mechanically verifiable ones (★) checked first.
- vendor-registry module-map heading de-versioned ("three delivery forms, three modules") to stop per-file version drift.

## 2.7.0 — 2026-09-05

- New module ② free AI products; delivery-form gate ("app free ≠ API free", DeepSeek as the canonical trap case).
- best_pick eligibility (three conditions); persistence hard gate; claims discipline extended to guidance text.
- Known defects shipped (fixed in 2.8.0): cache carried developer state; intro/module numbering collision; FULL budget had no module-② slot.

## 2.6.0 — 2026-09-05

- Live-audit rules 4–7 added after the 09-05 live-run divergence event (N16).
- Freshness contract F1–F6 as the single authority; confirmed/confidence dual axis.
