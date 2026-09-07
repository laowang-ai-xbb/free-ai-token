# Safety — Risk tiers, key hygiene, scam & red-line rules

The user explicitly wants grey channels *described with steps + clear risk
labeling* — but this skill must never cross the red lines below. This file is
the safety floor for every output.

---

## 1. Risk tiers (apply to every candidate)

| Tier | Meaning | How we treat it |
|---|---|---|
| 🟢 **Safe / official** | Official free tiers, verified low-cost official plans, reputable licensed resellers with clean record | Recommend normally; put top of ranking |
| 🟡 **Caution** | Legit but with a catch: prepay floor, non-refundable credits, ToS-grey, newer/less-proven reseller, **self-service cross-region purchase** (own account + your own VPN + a payment method you legitimately hold) | Show with a clear ⚠️ note listing the specific catch; rank below 🟢 |
| 🔴 **High risk / grey** | A region deal needing **fabricated local identity/address/payment** (see §2), shared/leased keys, unvetted reseller, paid third-party "setup/代充" middleman, "too good" relay | Show steps **only with** the risk banner first; rank last; never imply it's a good idea |

Independent of tier, every candidate still gets its neutral score from
`references/scoring.md`.

---

## 2. Red lines — never do (hard refusal)

- **Never** help steal or abuse someone else's quota/credits/accounts.
- **Never** create accounts for identity fraud or multi-account abuse of
  signup bonuses in bad faith — this includes fabricated local identity,
  address, or payment identity used to reach region pricing.
- **Never** bypass paywalls via technical exploitation (scraping protected
  endpoints, replaying keys, etc.).
- **Never** fabricate that a browser/registration action succeeded when it
  did not. On a non-browser environment, degrade to steps; do not fake
  automation.
- Payment-card fraud, phishing, or laundering tools: refuse outright.

---

## 3. Scam & fraud detection checklist (teach the user)

Show this when a candidate smells off, or when the user asks "is X legit?":

1. **No real homepage / no legal entity** → treat as very high risk.
2. **Price 10× below market** with no explanation → almost certainly theft or
   a scam; flag 🔴 and warn.
3. **Asks for your card "just to verify" on a reseller** → stop; real free
   tiers don't. Use a virtual single-use card if any card is ever needed.
4. **Shared / "team" / "family seat" keys on resellers** → many are sold to
   several people at once → revoked mid-term, no refund.
5. **No ToS, no privacy policy, no support channel** → do not recommend.
6. **Telegram/QQ "admin will set it up for you"** → phishing; never hand over
   any existing key or OTP.
7. **Benchmark/score claims that don't match any independent report** →
   mark unverified, drop the confidence flag.

---

## 4. Region-deal specific warnings

Region-priced AI memberships (Turkey/India/Argentina etc.) usually violate
the provider's and/or the app store's terms. Always surface, in the user's
language and *before* steps:

- Account / card / IP **region mismatch** can cause instant block or ban.
- **Payment declined** is common → your money may be held then reversed.
- If the AI product or store **detects the bypass**, the account can be
  **terminated with credits/membership lost**.
- Reseller "subscription setup service" fees are often unrecoverable when it
  fails.
- If executing the deal would require fabricated local identity documents,
  addresses, or payment identities → that crosses §2's identity-fraud red
  line: refuse the steps, keep only this risk explanation.
- State clearly: "You decide; we inform." Never encourage; never moralize.

### 4.1 Membership-purchase money safety (BUY mode)

Spending money scares users more than signing up. The purchase flow
(`buy-membership.md`) therefore carries its own floor:

1. **Three promises, verbatim** ({i18n:buy_promise}) before any navigation:
   amount and billing period stated first; only a payment method in the user's
   own name; the agent never holds card details.
2. **Never ask for, receive, echo, or store** card numbers, CVV, payment
   passwords, or payment OTPs. If the user pastes one, advise rotating it and
   move on.
3. **Worst case in concrete words** ({i18n:worst_case}) on every 🟡
   cross-region card and before its steps — "订阅可能被取消、钱可能拿不回、
   账号可能被标记" beats any abstract risk label. When the Flight-Check
   (`buy-membership.md` §2.0) ran, append its time-stamped enforcement-heat
   result (source, date); "未见近 30 天公开执法报告" is NEVER worded as
   "likely safe" ({i18n:xr_enforcement_note}) — absence of evidence is not
   absence of risk.
4. **Before the first payment step**, hand over the money-hygiene pair: a
   virtual single-use card where available (§5 rule 6) + a spending cap/alert
   (§5 rule 5). One line each.
5. **Cancel path always shown** after purchase (renewal date + how to
   cancel). No dark patterns, no "forget to mention auto-renew".
6. Gift cards: official store channels only; reseller gift cards and
   pre-made accounts are a top scam vector (§3 rules 4/6) → 🔴.

---

## 5. API key hygiene (the 10 rules)

1. **Treat a key like a password.** Never post it, never paste it in a shared
   chat, never commit it to a public repo.
2. **Store in env vars or a password manager**, not in plaintext files.
3. **Scope keys to minimum permission** when the platform allows it.
4. **Rotate keys** on suspicion of exposure.
5. **Set hard spending caps / alerts** where the platform offers them, so a
   leak can't rack up a bill.
6. Use **virtual/single-use cards** for any pay-to-try provider.
7. If the skill auto-obtains a key, write it only via the storage ladder in
   `auto-register.md` §3 — never echo it into the transcript.
8. Check the provider's data-training default; disable it for sensitive work.
9. Revoke unused keys.
10. Different key per agent is fine, but keep a ledger of which key goes
    where.

---

## 6. Neutrality & disclosure

- Disclose any affiliate/sponsor relation inline for the affected item.
- Scores must not be inflated for popularity. Two-sided cons per
  `references/scoring.md`.
