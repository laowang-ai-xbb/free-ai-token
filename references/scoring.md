# Scoring — neutral, multi-dimensional, evidence-based

This is the rulebook for scoring any platform / model / deal **neutrally**.
The goal is defensible, conflict-of-interest-free scores a professional can
reproduce and a novice can read. Every score must be traceable to evidence
(official page, cross-corroborated community report, or an explicit "could
not verify" note).

---

## 0. Unit normalization (always before scoring Price)

Vendors quote incomparable units — tokens, requests, credits, neurons,
RPD/RPM caps. Normalize before comparing or scoring:

1. **Target unit:** USD per 1M output tokens (state the in/out ratio used).
2. **Credit-based offers** (e.g. $-credits, starter credits) → convert at the
   provider's own list price; label "≈".
3. **Request-capped offers** → convert assuming a stated typical request
   size; declare the assumption inline.
4. **Rate-capped "unlimited volume" offers** (e.g. 3 RPM, no token cap) →
   express as practical monthly throughput at the cap, not a unit price.
5. **Not computable** → mark "unit not comparable"; Price is then scored
   qualitatively and the flag appears on the card.
6. **Membership / region subscription prices** (module ②) → normalize to USD
   per period (月 / 年) so regions are comparable side by side, and keep the
   local price + currency code in parentheses — e.g. `≈$17.7/月 (PKR 4,999)`.
   Use the provider's own list price for the conversion; the figure is an
   estimate and wears "~" / {i18n:badge_converted}.
7. **Human-unit conversion (beginner persona).** A raw quota means nothing to
   a non-technical user. Render it through {i18n:human_units}: tokens → pages
   (~1,300 tokens/page) or chat turns (~600 tokens/turn); RPM → "about N
   requests a minute — fine for one person typing". The assumption goes in the
   slot; a humanized number is never presented as an official figure.

All converted figures start with "~" (estimate) per `deal-hunting.md` F5.

---

## 1. The 7 scored dimensions

Score each 0–10, integers.

| Dim | What it measures | Where the evidence comes from |
|---|---|---|
| **Price** | Normalized cost per 1M tokens (in+out), free-tier size, first-credit generosity | Official pricing; promo pages |
| **Stability** | Uptime, throttling, outages, maintenance frequency | Status pages, community reports |
| **Speed** | First-token latency & throughput (TTFT / TPS) | Benchmarks, user reports |
| **Quota / transparency** | Hidden fees, prepay floors, expiry of credits, rate caps stated clearly | ToS, pricing FAQ |
| **Security** | Key handling, encryption, privacy policy, whether data trains models | Privacy policy, SOC2/ISO notes |
| **Compliance** | Region legality **and accessibility** (open to the user's region for signup/payment?), ToS-abidance, data residency | ToS, jurisdiction |
| **Ease of use** | Signup friction, dashboard, docs quality, onboarding | Direct observation |

### 1.1 Scoring anchors (reproducibility — use these, not vibes)

Two runs over the same evidence must land within ±1 point. Score from the
anchors; interpolate only with a stated reason.

| Dim | 10 | 7–8 | 4–6 | 1–3 | 0 |
|---|---|---|---|---|---|
| Price | Long-term $0, no card | $0 but rate-capped / short window | Low-cost, transparent per-token | Mid-market pricing | Above market without cause |
| Stability | No incidents this quarter; status page clean | Rare, brief incidents | Periodic throttling/outage reports | Frequent incidents | Chronic downtime |
| Speed | Top-quartile published TTFT/TPS | Good community-reported speed | Average | Slow reports dominate | Unusable latency |
| Quota/transparency | All caps published, no hidden fees | Most caps published | Partial disclosure | Key limits only in ToS | Opaque / silent changes |
| Security | No training on data by default + SOC2/ISO | No-training default, no cert | Training opt-out exists | Training by default | No policy / known incidents |
| Compliance | Fully open to user's region, ToS-clean | Open with minor friction | Self-service cross-region needed (🟡) | Officially restricted but reachable | Blocked / needs fabricated identity |
| Ease of use | Signed in & working in <5 min (key created, or first app conversation — the delivery form decides which) | Email signup, minutes | Approval / waitlist friction | Multi-day approval | Hostile onboarding |

---

## 2. Total, confidence flag, risk tier

- **Total** = weighted mean of the 7 dimensions. Default weights (adjust and
  say so): Price 26% · Security 16% · Stability 16% · Speed 11% ·
  Quota/transparency 10% · Compliance 10% · Ease-of-use 11%.
- **Freshness is NOT a score dimension** — it describes our evidence, not the
  vendor. It is the line's **confidence flag**, shown beside every deal:
  - ✓ verified this run on an **official surface** (pricing page *or* official
    docs) — a reachable official figure
  - ~ estimated/converted (§0), partially evidenced, **or** two agreeing
    secondary sources when the official page was unreachable this run
    (capped at ~, never ✓ — see `deal-hunting.md` §3.1)
  - ⚠ stale (>24 h, a **single** secondary source, or "{i18n:badge_unverified}")

  A ⚠ line may still be listed, but flag-first — never ranked above verified
  rivals on score alone.
- Show the **per-dimension breakdown** in EVAL mode or on request, so the
  score is auditable. Keep totals to 1 decimal **only when the §1.1 anchors
  were applied**; annotate estimated dimensions **on the user-facing card** —
  `9.1/10·估3维` — with {i18n:legend_score} nearby. An unannotated total with
  silent N/A dimensions is false precision and fails the checklist.
- Independent of the total, assign the **🟢/🟡/🔴 safety tier** from
  `references/safety.md`. **The tier is the primary sort key in ranking; the
  total is secondary.**

### 2.1 User-facing evidence badges (say it in plain words)

The symbols ✓/~/⚠ are internal shorthand. Anything shown to the user uses the
plain-word badge instead — never a bare "(估算)/(estimated)", which reads as
"made up". State WHO verified the figure:

| Internal | User-facing badge |
|---|---|
| ✓ | {i18n:badge_official} |
| ~ — ≥2 agreeing secondary sources | {i18n:badge_cross} |
| ~ — converted/computed (§0) | {i18n:badge_converted} |
| ⚠ | {i18n:badge_unverified} |

In tables where space is tight, symbols may stand in ONLY with the legend
line ({i18n:legend_confidence}) directly beneath.

---

## 3. Data-availability downgrade (anti false-precision)

If evidence for a dimension cannot be obtained **this run** (Speed /
Stability / Security are often unavailable), do NOT invent a number:

- Score that dimension **N/A** with a one-line reason.
- When computing the total, drop N/A dimensions and **re-normalize the
  remaining weights to 100%**. If more than half the dimensions are N/A,
  output no total at all — show only available sub-scores + the safety tier.
- Never present a weighted total as exact: annotate estimated dimensions and
  keep totals to 1 decimal.

---

## 4. Neutrality rules (non-negotiable)

1. **No paid placement.** If an item paid or incentivized us, score it as any
   other and flag "sponsored/affiliate" — never boost it.
2. **Evidence > reputation.** Forum hype does not raise Price/Security
   scores; only verifiable facts do. Mark anything unverified. **Benchmark
   evidence is legitimate evidence:** leaderboard standings (Artificial
   Analysis, LMArena/Chatbot Arena, LiveBench) may drive quality ordering
   and the free-strong-models shortlist — neutrality forbids paid placement
   and shill hype, not ranking by measured quality.
3. **Two-sided cons.** For every downside listed, state the condition under
   which it matters ("unless you need EU residency", "unless you scale past
   the free tier"). Avoid scare-labeling without grounds.
4. **Disclose the source of each number** inline (per `deal-hunting.md` §0,
   with as-of date). Estimates labeled "~".
5. **Conflicts resolve to the official page** (`deal-hunting.md` §3).
6. **Model-vs-platform:** when the same model is sold by multiple channels,
   score the *channel + model* combination — price and quota belong to the
   channel, performance mostly to the model.

---

## 5. Scorecard skeleton (EVAL mode; fill per candidate)

```
{Name} — {one-line identity}
Price {x}/10 · Stability {x}/10 · Speed {x}/10 · Quota {x}/10
Security {x}/10 · Compliance {x}/10 · Ease {x}/10
Total {t}/10 ({n} of 7 dims estimated) · Confidence {✓/~/⚠} · Tier {🟢/🟡/🔴}
Key evidence: ...
```
