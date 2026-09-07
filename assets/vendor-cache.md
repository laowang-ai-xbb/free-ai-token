# Vendor cache — writable persistence layer (fact layer, timestamped)

The **only** place volatile facts live: confirmed deals, last-run snapshots,
user preferences. Everything here carries a date and expires. This file is
loaded at the start of every hunt and rewritten at the end.

Rules (same contract as `vendor-registry.md` § Seed back-fill):

1. Only **cross-confirmed** vendors (≥2 independent sources or the official
   page) and user-saved preferences may be written here. One-snippet claims
   and pure promo never enter — at most the `unverified_heard_of` list, which
   is never ranked.
2. Every vendor entry carries `verified_on` + risk tier + source. Rows not
   re-confirmed within **30 days** are removed at the next write (accuracy
   beats shelf count).
3. **Never store API keys or secrets here** — preferences and vendor rows
   only.
4. Merge rules: dedupe by `(name, class)`; single writer per run; rewrite the
   whole JSON block atomically at run end.
5. Nothing in this file may be printed as a current fact without this run's
   live verification — freshness contract F4 (`deal-hunting.md` §0).
6. **Read before write** (host tool requirement): read this file before
   editing it within a task.
7. Significant findings made mid-task (reachability blocks, signup-path
   surprises) are written **as soon as found** — never held until run end.
8. **Growth limits (the cache is read on every run — keep it lean):** each
   entry's `notes` keeps the **≤3 most recent** dated observations; older ones
   are dropped at write time (the `deal` field carries the current truth).
   `unverified_heard_of` entries not re-confirmed within **30 days** are
   removed at the next write, same as vendors (rule 2).

---

## Schema migration (read before load)

If a data block declares `schema` < 3 (or a missing/foreign `schema` field):
treat every existing vendor row as `unverified_heard_of` — it may NOT be
printed, ranked, or linked this run; re-confirm it per G1/G1.5 before it can
be promoted back into `vendors`, then rewrite the block at schema 4. Never
convert silently.

**Schema 3 → 4 (additive only):** rows from a schema-3 block keep their full
status (they passed the same G1/G1.5 gate); at the next write, add
`"discovered_on": null` to each row. `discovered_on` = the date the vendor
FIRST entered this cache — it survives re-verification and is never reset
(`verified_on` already carries the latest check). A row lacking the field, or
with `discovered_on: null`, never wears the NEW badge — absence of evidence
is the conservative default.

## Ingression gate — enforce before EVERY cache write

Each candidate entry must pass, in order; failure sends it to
`unverified_heard_of`, never into `vendors`:

- **G1 Cross-confirmed:** ≥2 independent sources agree, or the official page
  states it. A single source — however reputable — fails.
- **G1.5 Independence check (pseudo-independence guard):** two "independent"
  sources that share one origin count as ONE source. Same-origins include:
  same root domain or mirror; same first-poster / same first post (one Product
  Hunt / HN / Reddit thread and its reposts); aggregator-panel clones
  (one-api/new-api panel listings) echoing the same upstream; syndicated news
  reprints of one wire item. To pass G1 as two sources, they must have
  different root domains AND independently discoverable first publications.
- **G2 No conflict:** if sources disagree on the figure, the entry fails;
  keep the conflict note in `unverified_heard_of`.
- **G3 No secrets:** keys/passwords never enter this file (rule 3).

Mid-task findings (rule 7) are appended to the entry's dated `notes` list —
they are observations, not deal claims, so G1/G2 do not apply to them.

---

## Persistence ladder (where to actually write)

1. **Host persistent memory / ledger tool** — preferred when the host exposes
   one.
2. **This file** — when the skill directory is writable.
3. **Session-only** — and TELL the user this run's discoveries/preferences
   were NOT persisted. Never claim "saved" when nothing was written.

---

## Schema (valid JSON — keep comments OUTSIDE the block)

> **Why the `__EXAMPLE` suffix below:** `accounts` / `checkpoints` are suffixed
> in this illustrative block only so they can never collide with the live `##
> Data` block when you find/replace it (empty arrays repeat otherwise). The real
> data block uses the plain names described in Field notes below. When editing
> the data block, anchor on a data-only line (e.g. `"region": "CN"`), never on
> a bare `"accounts"` / `"checkpoints"`.

```json
{
  "schema": 4,
  "updated_on": null,
  "preferences": {
    "region": null,
    "default_target": "both",
    "lang": null,
    "filters": { "avoid": [], "require": [] },
    "saved_picks": []
  },
  "accounts__EXAMPLE": [],
  "checkpoints__EXAMPLE": [],
  "vendors": {
    "C1_gpu_cloud": [],
    "C2_inference": [],
    "C3_china": [],
    "C4_frontier_official": [],
    "C5_aggregators": [],
    "C6_memberships": [],
    "C7_app_bundled": []
  },
  "unverified_heard_of": []
}
```

Field notes:

- `schema`: bump when the shape changes.
- `updated_on`: last write date, e.g. `"2026-09-04"`.
- `default_target`: one of `api` | `memberships` | `both`.
- `lang`: `en` | `zh` | null (auto-detect).
- Class keys mirror `vendor-registry.md` C1–C7.
- `accounts`: registration ledger — entries shaped `{platform, email,
  session_confirmed_on, notes}`; reused for session-first fast paths
  (`auto-register.md` §0.1 step 5) and never re-asking answered intake
  questions. Sessions expire — re-verify before trusting.
- `checkpoints`: in-progress registrations **and purchases** —
  `{platform, stage, updated_on}`; `stage` ∈ `preflight` / `intake` /
  `submitted` / `email_verified` / `key_created` / `saved` / `purchased` /
  `plan_active` (the last two are BUY-mode, `buy-membership.md` §3). Resumed
  per `auto-register.md` §8; shown to the user via the localized `stage_*`
  i18n labels, never the raw enum.

Vendor entry shape (illustrative, not a real claim):

```json
{
  "name": "ExampleVendor",
  "class": "C2_inference",
  "deal": "free inference credits for new users",
  "normalized_price": "~$0.00 per 1M out tokens during trial",
  "verified_on": "2026-09-04",
  "discovered_on": "2026-09-04",
  "tier": "green",
  "source": "official pricing page",
  "notes": ["2026-09-04: console subdomain returns 403 from CN networks"]
}
```

(`tier` stored as plain `green` | `yellow` | `red` so the file stays
diffable; render as 🟢/🟡/🔴.)

---

## Data (last-run snapshot — do NOT print without live re-verification, F4)

```json
{
  "schema": 4,
  "updated_on": null,
  "preferences": {
    "region": null,
    "default_target": "both",
    "lang": null,
    "filters": { "avoid": [], "require": [] },
    "saved_picks": []
  },
  "accounts": [],
  "checkpoints": [],
  "vendors": {
    "C1_gpu_cloud": [],
    "C2_inference": [],
    "C3_china": [],
    "C4_frontier_official": [],
    "C5_aggregators": [],
    "C6_memberships": [],
    "C7_app_bundled": []
  },
  "unverified_heard_of": []
}
```

> **Shipped state = EMPTY by design (2.8.0).** This file ships with an empty
> Data block so a fresh install inherits NOTHING from the developer's
> machine — no region, no language, no filters, no vendor rows (the 2.7.0
> defect: a new install silently inherited region=CN / lang=zh). The first
> run initializes it; treat `updated_on: null` as "no baseline to diff"
> (`commands.md` §2). **Packaging rule:** before zipping a release, empty
> the Data block — real run data lives only in the installed copy, which
> release packaging never touches.
