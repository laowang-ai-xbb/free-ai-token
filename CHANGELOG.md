# CHANGELOG

One line per rule change: date — event — product. Case IDs (N16, the
2026-09-05 defect) referenced by other files resolve here.

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
