# Commands — canonical command set, scheduled scans, /estimate, preferences

Instant mode is the default, but repeat/power users get one-word commands so
nothing feels slow. A message beginning with `/` is always a command.
Unknown `/…` → treat as a plain query and run the instant hunt (see the mode
router in SKILL.md).

---

## 1. Command reference

| Command | Meaning | Action |
|---|---|---|
| `/deals` | Show current top AI money-saving deals now | FULL instant hunt, ranked list |
| `/deals api` / `/deals apps` / `/deals member` | Narrow to one module: API tokens / free AI products (no key) / membership plans | Hunt that module only |
| `/keys <model>` | Cheapest legit way to get this model's API access | COMPARE channels for that model → best-value ranked |
| `/compare <model>` | Price/score one model across channels | Emit the model-vs-platform compare table |
| `/eval <platform>` | Neutral score a specific platform/relay | Run `scoring.md` on it, output scorecard + risk tier + verdict |
| `/estimate [usage]` | "What will I actually pay per month?" | ESTIMATE mode — see §3 |
| `/config <agent>` | How to wire a key into this agent | Load `references/agents/…` and give the shortest path |
| `/register <platform>` | Get me a key on this platform | Load `references/auto-register.md`; graded automation or steps |
| `/buy <product>` | Get me this membership at the best legit price | Load `references/buy-membership.md`; graded purchase guidance — **payment never automated** |
| `/specs <platform>` | Expert depth on one platform | Model IDs, RPM/TPM/RPD, context window, data-training default, commercial terms, endpoint path — under {i18n:specs_heading} |
| `/simple` · `/pro` | Force beginner / expert rendering | Overrides persona auto-detection (`ranking-template.md` §0.5); the choice is saved to preferences |
| `/scan [daily|weekly]` | Set up a scheduled deal scan | Produce the scheduled-brief format; hook to host scheduler **if it has one** |
| `/lang en|zh` | Force output language | Override auto-detection; other values → note en/zh-only labels, fall back to English |
| `/safe` | Key hygiene & scam checklist | Output `safety.md` §3 + §5 in the user's language, under the headings {i18n:scam_heading} then {i18n:key_hygiene_heading} |
| `/help` | List commands | Show this table |

---

## 2. Scheduled scan brief format

When a recurring schedule (daily/weekly) invokes this skill, output a compact
brief in the user's language. Target **under ~300 words**. Sections:

```
# AI 省钱快报 · {date}
(Sections, in order of importance:)
1. Headline — the single best new/changed deal, 1–2 lines.
2. New free credits / free tiers that appeared since last scan.
3. Expiring promos / credits about to end (with the end date if known).
4. Price moves (up/down) on majors the user might care about.
5. Risk alerts — anything newly risky/flagged in the saved list.
6. (Optional) Top-3 "act now" recommendations, one line each.
Footer: "要我把某项展开 / 帮你注册 / 改配置？" (ONE line)
```

- Re-scan; do not reuse a cache older than 24 h (freshness contract F2,
  `deal-hunting.md` §0). Label every figure with its as-of date.
- **Diff against the baseline** in `assets/vendor-cache.md` when a previous
  snapshot exists ("changed since last run" is the headline). **No baseline
  yet** → give a plain brief and say "first scan — no baseline to diff".
  **"Changed" is defined** — any of: a vendor added/removed; `deal` or
  `normalized_price` text differs; `tier` moved; a NEW dated note appeared;
  an `unverified_heard_of` entry got promoted into `vendors` (or demoted).
  Nothing else counts.
- If nothing changed, say so plainly and stop — no filler.

**No scheduler on this host?** Say so plainly (one line), then give the
user-side alternative: a self-run command/cron snippet to invoke the skill on
schedule, or a saved prompt the user can fire manually.

---

## 3. `/estimate` — monthly cost estimator

Goal: turn "price lists" into "what I'd pay". Steps:

1. **Usage profile** — ask once (or infer from context, stating the guess):

   | Profile | Assumed volume |
   |---|---|
   | light chat | ~0.5M tokens/day |
   | coding copilot | ~2M tokens/day |
   | batch pipeline | ~20M tokens/day |
   | custom | user states tokens/day or requests/day |

2. **Normalize** the shortlisted 3–5 options to $/1M output tokens per
   `scoring.md` §0 (every converted number starts with "~").
3. **Compute**: monthly volume = daily × 30; monthly cost = volume × unit
   price, then subtract what the free tier covers (state coverage %).
4. **Output** one small table — option × profile ⇒ ~monthly cost (USD and
   CNY) + free-tier coverage — titled "{i18n:estimate_title}", ending with
   one best-value line per profile.

---

## 4. Saved-preference ledger (persistence ladder)

Source of truth, in order of preference:

1. **Host persistent memory / ledger tool** — preferred when the host exposes
   one.
2. **`assets/vendor-cache.md`** — the skill-writable cache (schema, merge
   rules and expiry live in that file).
3. **Session-only** — and SAY SO. Never claim a preference was "saved" when
   nothing persisted.

Ledger fields (same shape as `vendor-cache.md` `preferences`):

```
region · default_target (api | memberships | both) · saved_picks ·
filters (avoid / require) · lang
```

Respect these as defaults on every hunt; never let them override a fresher,
higher-scoring, safer current option. **Make personalization visible:** when a
preference actually shaped this run's output (a filter applied, the region
assumed, the persona overridden), say so in one short header phrase — e.g.
"已按你的偏好：免信用卡". Silent personalization reads as generic.
