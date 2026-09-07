# Buy membership — graded, low-barrier flow to actually GET the plan

Core function ③ of this skill: help the user **obtain a membership plan**
(ChatGPT Plus / Claude Pro / Gemini Advanced / Midjourney / Suno …) with as
little friction as possible — mirroring `auto-register.md`'s gear system, with
one absolute difference: **payment is NEVER automated. The user's own hands,
every time.**

Entry: `/buy <product>` · "帮我买/开通 XX 会员" · user picks a module-② card.
Load set: this file + `safety.md` §4–§5 + `capability-check.md` (browser probe
only). Query budget 0–1.

---

## 0. Money-safety floor (before anything else)

1. **Three promises, verbatim** ({i18n:buy_promise}) — stated at run start,
   before any navigation: amount and billing period first; only a payment
   method in the user's own name; the agent never holds card details.
2. **Never ask for, receive, or store**: card numbers, CVV, payment passwords,
   payment OTPs. If the user pastes one, tell them to rotate/cancel it and
   never echo it back.
3. **Red line (safety.md §2):** any path requiring fabricated identity,
   address, or payment subject → refuse the steps, keep only the risk
   explanation, and offer the official-discount alternative.
4. **Before the first payment step**, hand over the money hygiene pair
   (`safety.md` §5): virtual single-use card where possible + a spending
   cap/alert. One line each, not a lecture.
5. **Claims discipline:** factual assertions inside guidance ("教育折扣还在"
   / "该区不需要当地卡") carry this run's evidence — (source, date) — or
   soften to "以官网为准". Money decisions deserve the same freshness
   contract as rankings (`deal-hunting.md` §0).

## 0.1 Shelf routing — which kind of deal is this?

Decide FIRST; it determines the whole path (shelves defined in
`ranking-template.md` §2 module ③):

| Shelf | Tier | Path |
|---|---|---|
| Official discount (education / annual / first-year / promo window) | 🟢 | Straight to the official buy page; verify the discount is still live this run |
| Carrier / bundle (e.g. SoftBank × Perplexity) | 🟢/🟡 | Eligibility check first (plan / region / new-customer) |
| Cross-region price (self-service) | 🟡 | §2 below — worst-case line BEFORE steps |
| Reseller / 代充 middleman | 🔴 | Risks described, no steps; licensed resellers only, and only with the risk banner |

> **Cheapest legit first.** If the user's account region ALREADY qualifies for
> a lower official price, there is nothing to bypass — say so and skip the
> grey path entirely.

## 0.2 ONE batched intake round (never more)

Ask in a single message, with sensible defaults:

1. Product + plan (Plus / Pro / Advanced; monthly vs annual — annual often
   beats any region trick).
2. Account status: have one? **which region is it registered in?**
3. Payment means the user ACTUALLY has: own card (issuing country) / App
   Store or Google Play account region / gift card / none of these.
4. Where they'll use it (phone app vs web) — decides App Store path vs web
   checkout path.

Payment means decide the route: no matching payment method for the target
region → the cross-region path is likely a dead end; pivot to the official
discount shelf or the API-key alternative (delivery downgrade) instead of
pushing gift-card grey markets.

## 0.3 Gears (payment never automated)

| Gear | Shape | When |
|---|---|---|
| **L3 guided checkout** | agent opens/navigates pages, explains each screen; user clicks pay | normal case |
| **L2 co-pilot** | user operates, agent verifies every screen | ToS-sensitive flows, anti-fraud walls |
| **L1 hand-holding** | plain-word steps only | no browser automation |
| **L0 fallback** | official discount / cheaper API path / park | impassable (§5) |

Automation may open pages and read screens; it **prefills nothing
payment-related** and hands off at the payment screen with one plain line
("到付款这步了——金额核对一下，你自己点确认"). Downshift etiquette:
{i18n:downshift_line}.

## 0.4 Expectation declaration (before the first action)

{i18n:expect_line} + {i18n:buy_promise} + **the price restatement**: the
exact amount, currency, billing cycle, region, and how to cancel — e.g.
"你会被扣 ≈$16.0/月（₱999，菲律宾区，App Store 订阅），随时可在订阅管理里
取消。" Never start navigation before this lands.

## 1. Pre-flight — the same three gates as auto-register §0.1

Reachability (user's browser path judges), right browser/session, bounded
retries (≤2), wall menu ordered for the situation: **reachable 🟢 official
discount first**, cross-region second, park third. Record findings in
`vendor-cache.md` immediately (dated notes). Session-first reuse applies: an
already-logged-in store/account session skips the login steps.

## 2. Cross-region (🟡) execution notes

### 2.0 Cross-Region Flight-Check — four live checks BEFORE any step

The cross-region path is the most time-sensitive thing this skill ships:
store prices, payment rails, and enforcement posture all move weekly. Static
advice here breaks silently. So the 🟡 path starts with a Flight-Check —
each element carries (source, date) this run, or degrades per the honesty
layer (⚠ unverified / "以官网为准"). Category-tiered so the query budget
(0–1) survives:

| # | Check | Type | Pass rule |
|---|---|---|---|
| 1 | **Price now** — target-region price + tax + currency for this exact plan | mandatory | this run's official page/store price; else ⚠ unverified |
| 2 | **Payment feasible now** — does the user's actual payment means (intake 0.2) map to a live route for THIS region? (matrix below) | mandatory | route name this run; unverifiable → treat as dead end per 0.2 |
| 3 | **Enforcement heat** — any public ban/cancellation wave against self-service region buyers on THIS product in the last 30 days | conditional (🟡 engaged) | (source, date) or explicit "未见近 30 天公开执法报告" — which is NEVER worded as "safe" ({i18n:xr_enforcement_note}) |
| 4 | **ToS clause now** — the platform's current regional/terms clause affecting cross-region subscription («payment region enforcement») | conditional (🟡 launch) | quote or paraphrase with (source, date); stale ToS quotes carry a date and are re-verified only on 🟡 launch |

Checks 3–4 can be merged into ONE batched search when needed ("{product}
account banned region change {month} {year}"). A check that cannot be
verified is REPORTED as degraded — never silently skipped — and the
Flight-Check failing any mandatory check routes to the fallback ladder (§5)
instead of proceeding.

### 2.1 Payment means × region matrix (from intake 0.2)

| User's means (from 0.2) | App Store/Play path | Web checkout path |
|---|---|---|
| Own card, issuing country = target region | 🟢 direct | 🟢 direct (billing address honest) |
| Own card, different country | switch-store region needs local method or gift card (§2a) | product-dependent: try honest card first; decline/3DS wall → next row |
| App Store/Play account IN target region | 🟢 direct — but cancelling current-region subscriptions may be required | n/a |
| Gift card (official store, own hands) | 🟢 after region switch — code input while store region matches | n/a mostly |
| Gift card via reseller | 🔴 top scam vector — official cards only | 🔴 |
| None of these | dead end → fallback ladder (§5): official discount → API-key alternative → park | same |

Never prefill or "improve" payment identity; a mismatched handle is the
user's decision point, not the agent's tast to fix. The matrix routes; only
the user's own real payment identity passes, anything else hits the red line.

### 2.2 Always-on step: node–region consistency check
At the moment the 🟡 path starts: confirm the VPN node's country matches the
target store region (ask the user to check their exit-country, or probe the
geo via the browser header when automation is on). A mismatch before
checkout is the cheapest fix and the most common silent failure — one line
before the App Store/web paths begin.

- **Worst case first** ({i18n:worst_case}): subscription cancelled, money
  possibly unrecoverable, account possibly flagged/banned — one line, BEFORE
  any step. Then the §6-style banner from `ranking-template.md`.
- **App Store path:** region switch usually needs a local payment method or
  gift card; switching region may require cancelling active subscriptions
  first; gift cards bought from resellers are a top scam vector — official
  store gift cards only; NEVER buy a pre-made account.
- **Web checkout path:** billing-address mismatch is the #1 failure; the
  user's own real card works on some products without address tricks — try
  the honest path first; keep the VPN node consistent with the store region.
- **Any step needing fabricated identity/address/payment → STOP** (red line),
  keep the risk explanation, offer the official-discount alternative.

## 3. Purchase-confirmation stop (mirror of key capture)

After the user pays, do not declare success until all three are seen:

1. **Charge matches** the restated amount + currency (receipt screen).
2. **Plan active IN the product** (settings / subscription page shows Plus /
   Pro / Advanced).
3. **Renewal date + cancel path noted** — always show how to cancel, one
   line, no dark patterns.

Checkpoint stages: `purchased` → `plan_active` (`vendor-cache.md`; resume per
{checkpoint_resume} with localized stage labels).

## 4. After success — close the journey, don't drop the user

ONE line, pick what fits:

- "要我盯着续订日期 / 促销到期，提前提醒你吗？"（→ `/scan`, `commands.md` §2）
- official-discount upgrade check at renewal (annual vs monthly),
- if the membership turned out unnecessary → the delivery downgrade in
  reverse: a free API/app path may cover the same need.

Never upsell; never suggest stacking grey channels.

## 5. Fallback ladder — every dead end lands soft

1. Payment declined → check region/card mismatch → honest path or official
   discount.
2. No gift-card/payment route → official discount shelf → cheaper API
   alternative (function ②) → park.
3. Account flagged during purchase → STOP, do not retry; explain the risk,
   park with checkpoint.
4. Store/app unreachable → web checkout path, or park.
5. Honesty layer: whatever fails, say it plainly; save the checkpoint; give
   the resume line ({i18n:checkpoint_resume}). Never claim a purchase
   succeeded that did not.
