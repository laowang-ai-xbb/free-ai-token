# Auto-register — graded automation to obtain an API key

Goal: get the user a working API key on a chosen platform with **as little
manual work as the environment allows**, and never lie about what was done.
Two runtime profiles:

- **Browser-capable** (a real page-driving capability was probed per
  `capability-check.md`): drive the flow automatically, pause only at
  human-verification gates.
- **Plain** (no browser automation): skip straight to precise steps. Never
  claim a browser action ran when it didn't.

Flow order: silent pre-checks (§0, incl. session-first reuse) → gear choice
+ expectation declaration (§0.4–§0.5) → capability check (§1) → ONE batched
intake round (§0.3) → browser flow (§2) or hand-holding (§4). Every dead end
lands in the fallback ladder (§7); progress is checkpointed (§8).

Platform names from the user are fuzzy-matched (grop → Groq): echo the
canonical name once to confirm, never interrogate the typo.

---

## 0. Silent pre-checks — before asking the user anything

### 0.1 Reachability pre-flight — the three gates (before asking anything)

Registration is the user's second core need; its success is dominated by
reachability. Never collect an email or open a signup form before these
gates pass.

**Gate 1 — Path confirmation, judged in the user's real path.**
Backend probes (curl/fetch) are CLUES only — the verdict comes from the
user's browser path (their system/browser proxy is the path they will
actually use; shell and browser often disagree). Any reachability wording
shown to the user (直连 / 需代理) follows the evidence standard of
`deal-hunting.md` §3.2 — no unevidenced assertion, and **domestic platforms
are not presumed direct either**. Order:
1. Backend quick probe of the signup/console URL (retry ONCE on transient
   error). Reachable AND matching the user's network situation → proceed.
2. Blocked or doubtful → check proxy state silently (**READ-ONLY**), then
   guide the user to open their proxy if they have one, and RE-TEST THROUGH
   THE USER'S BROWSER: open the platform homepage and confirm it renders.
3. Node guidance (experience rule, not dogma): prefer 美国/日本/新加坡
   exits, avoid 香港 and data-center IPs. **Only the user may change proxy
   settings, with explicit consent.**
4. Homepage renders but console/API blocked ⇒ run the diagnostic ladder in
   `agents/troubleshooting.md` (L1), don't guess.
5. **Session-first, before any login route:** consult the account ledger in
   `vendor-cache.md`; then open the console URL once in the session-bearing
   browser — if a LOGGED-IN view renders, skip the entire login step and go
   straight to the key page. Never make the user re-login or re-register an
   account that already works.

**Gate 2 — Right browser, one window.**
For a login path, enumerate open browser windows and attach to the one whose
title/URL shows the platform AND holds the login session; if none is found,
ask ONE line ("which browser are you logged in with?"). One browser, one
window, one tab; close any window opened by mistake immediately.

**Gate 3 — Bounded retries, guaranteed exit.**
≤2 attempts per barrier (anti-bot). When a barrier holds, stop and present
the wall menu, **ordered for the user's situation** — for mainland-China
users the directly-reachable alternative comes FIRST:
1) **Switch to the best reachable 🟢 alternative (recommended)** — the
   highest-scoring verified 🟢 from this run's ranking that connects
   directly from the user's region;
2) Retry with a proxy — caveat: daily use after registering will likely
   need the proxy too;
3) Park it for today.

**What we guarantee vs. cannot.** Geo-blocking policy belongs to the
platform — nobody can guarantee 100% success, and we never promise it. We
DO guarantee: no registration effort spent on an unreachable platform;
reliable driving once the path renders; and an honest fast exit to a working
alternative.

Record the reachability finding in `vendor-cache.md` **immediately** (§6) —
don't hold it until the end of the task.

### 0.2 Platform ToS check

Check the platform's terms for automated/bot signup restrictions. Order:
fetch likely official URLs directly first (`{vendor}/legal`,
`{vendor}/terms`, `{vendor}/tos`, or the site footer's links); web search
only as fallback.

- Prohibited → say so in one line and run the hand-holding flow (§4).
- **Unverifiable this run → say so in one line and apply the conservative
  default:** the agent only opens pages and navigates; login/submit actions
  are performed by the user personally. Never pass unverifiable off as
  verified.

### 0.3 Account-status probe (with intake)

Most users picking a platform either don't have an account yet, or ARE
existing users who never knew about the free tier. In the same ONE batched
question round (email, target tool, browser consent), ask "do you already
have an account here?" and route:

| Answer | Route |
|---|---|
| Have one | **Login path** — shortest: log in → API keys → create key. After login, first stop at the quota/billing page and SHOW the user their free-tier status (some platforms require opting in — confirm before creating the key) |
| Not sure | Try logging in with the user's usual email first; fall back to fresh signup if it fails |
| None | Fresh signup (§2 / §4) |

Never create a second account where the user already has one — multi-account
bonus abuse is a `safety.md` §2 red line.

### 0.4 Gear levels — auto-shift to the highest gear the USER can ride

The gear is chosen by what the user can cooperate with, not by what the host
can technically automate. Shift down at the first real barrier; announce it
in one plain line; never lose progress.

| Gear | Shape | User effort | When |
|---|---|---|---|
| **L4 full-auto** | agent does everything | 0 assists | valid session already confirmed (§0.1 step 5) and no human gates expected |
| **L3 semi-auto** (default target) | agent drives; user assists at gates | ≤2 atomic assists | the normal case |
| **L2 co-pilot** | user clicks, agent verifies every step | every step | ToS forbids automation (§0.2) or anti-bot risk is high |
| **L1 hand-holding** | precise plain-word guidance, one micro-step at a time | all steps | no browser automation, or two automation failures |
| **L0 fallback** | alternatives / delivery downgrade | — | platform impassable (§7) |

Downshift etiquette: one plain line — **{i18n:downshift_line}** — no
technical post-mortem, all progress kept.

### 0.5 Expectation declaration — before the first action

Non-technical users panic in silence and abandon flows they don't understand.
Before starting, say in their language:

1. **{i18n:expect_line}** — how many assists, what they are, rough minutes
   (fill from the chosen gear's gates).
2. **{i18n:safety_promise}** — the three promises, verbatim.
3. **Goal check (once):** if it's unclear whether the user needs an API key
   or just wants to *use* the model, ask **{i18n:goal_question}**. Answer
   "just use it" → offer the **delivery downgrade FIRST**: a login-and-use
   app (registry class C7) or a cheap membership — the API-key path is the
   HARDEST delivery form, not the default assumption.
4. **Progress narration (during the run):** one plain line per completed
   step ("page opened — filling your email now"). Never go silent across
   several actions; silence reads as "broken".

**Fast lane (persona-conditional protocol weight, 2.9.0).** The declaration
above is sized for first-run novices. For a returning user with saved
preferences (`assets/vendor-cache.md`) or a clearly expert persona
(`/pro`, precise ask: exact platform + exact key), compress the three
declaration items into ONE line — target gear + assists + minutes — and
start at **L4** when the §0.1 three gates and §0.2 ToS check pass.
**Hard boundary: the fast lane lightens protocol WEIGHT, never safety
checks** — ToS review, the three reachability gates, the human-verification
pause, and "payment is never automated" all execute unchanged. Any
friction (CAPTCHA, unexpected consent screen) downshifts to the normal
protocol mid-run, progress kept.

## 0b. Personal-data minimization

Use only personal data the user provided (their email, a name they gave).
**Never invent identity details** — name, birth date, address, phone,
documents. If the platform demands more than the user is willing to provide,
stop and tell the user; don't paper over it.

---

## 1. Capability check first

Probe the host's real abilities (behavior, not names — see
`references/capability-check.md`):

- **Browser automation present** → profile = browser-capable, try automation
  (`capability-check.md` §1 detects it regardless of what it's named; its
  first real navigation can double as the micro-test).
- **Absent but the user wants automation** → the options in
  `capability-check.md` §2–§3 (consent-gated enablement, else guided
  install), or jump straight to §4 plain steps.

> If browser tools exist but every attempt fails (login wall, CAPTCHA loop,
> anti-bot), fall back to §4. Do not loop retries more than ~2 times;
> anti-bot systems punish repeated attempts and can blacklist the user's IP.

---

## 2. Browser-capable flow (try to automate)

### 2.0 Front-door principle — enter through the official lobby

Always land on the vendor's **homepage first**, then click the official entry
("Start building / Sign in / Console" button) to reach the signup/console
pages. Do not type deep links straight into the address bar. The front door
carries a referrer chain and cookies (kinder to anti-bot systems), matches
what the user would do by hand, and yields diagnostic evidence — homepage
opens but console blocked ⇒ subdomain/region block, not operator error. Only
fall back to a direct deep link when the front door fails, and say so.

**Landing check after EVERY navigation (no exceptions).** Read back the
address bar + tab title, and confirm the intended UI element is actually on
the page before the next action. A `Forbidden` / error JSON / blank shell is
a navigation FAILURE — return to the front door or the diagnostic ladder
(`agents/troubleshooting.md`), never continue clicking as if the page
loaded. A URL is "good" only when the intended UI is OBSERVED rendering —
never because you "know" it.

### 2.1 Input discipline (non-negotiable)

- **Select-all before typing** into the address bar or any field (Ctrl+A /
  Ctrl+L), so new text replaces instead of appending to old text.
- **Verify after every type/key action** via window state that the text
  landed in the intended control of the intended window; if it drifted (e.g.
  into a chat input), clean it up immediately before continuing.
- Confirm the target window is in the foreground before each action block.

### 2.2 Human-verification gates (pause automation)

| Gate | What happens |
|---|---|
| Email verification code sent to inbox | Ask user to read it to you (or read from an already-logged-in mailbox if legitimately available). Pause. |
| SMS code | Pause; ask user for the code. Never guess. |
| Google/GitHub/Apple OAuth | Pause; let user complete the SSO in the visible browser, then resume. |
| CAPTCHA / reCAPTCHA / slider | Pause; ask user to solve it in the browser. |
| Anti-bot / device-fingerprint block | Stop automating; degrade to §4 steps. |

**Gate handoff protocol (every pause):**
1. ONE atomic request, precisely guided — e.g. "open your mailbox, find the
   mail from Groq, tell me the 6 digits; inbox empty? check the spam folder".
2. Email-code fallback order: wait ~60 s → check spam/junk → still nothing →
   suggest a Gmail/Outlook address (overseas delivery to some mailboxes is
   unreliable) → re-send ONCE at most.
3. **Prefetch while waiting:** load the next page's structure, pre-read the
   target tool's config docs — resume instantly when the user returns.
4. On resume, verify the entered value before continuing — a wrong code
   burned twice can lock the account.

### 2.3 Steps

1. Open the vendor homepage, dismiss the cookie banner, click the official
   console/signup entry (§2.0).
2. Prefill form fields (email, password, name) the user approved — nothing
   invented (§0b).
3. Submit, passing the gates above by pausing for user input as needed.
4. On success: navigate to the **API keys** section, click *create*, name the
   key, and capture it. **Login path (§0.3):** after login, visit the
   quota/billing page first and point out the free-tier status, then create
   the key.
5. Store the key per the ladder in §3 — never echo it into the shared chat
   transcript. Tell the user *where* it is stored and how to retrieve it;
   remind them to rotate it if it ever leaks.
6. Keep the same browser session open across steps; close it only at the
   very end.

---

## 3. Key-capture & storage ladder

- Capture from the **one-time display** on the provider's page. Some
  providers show the full key only once — if missed, guide the user to
  regenerate.
- Store via the first available rung, and tell the user which one was used:
  1. OS keychain / credential store (via CLI, if the host can);
  2. the user's password manager;
  3. a `.env` file with restrictive permissions in the user's own project;
  4. none of the above → the user copies it into their own password manager.
- Never echo the key into the chat transcript; never write it into
  `assets/vendor-cache.md` or any shared log.

---

## 4. Plain-environment steps (hand-holding, no browser)

Give the shortest possible path. Two-ish steps whenever the platform allows:

```
1) 打开 {platform} 官网 → 注册/登录
2) 进入「API Keys」→「创建新 Key」→ 复制
(保管：存进你自己的密码管理器/环境变量，别发聊天里)
(接下来：要我教你把它填进 {agent}？ → 加载 references/agents/…)
```

Login-path variant (§0.3): 登录 → 先看一眼额度页确认免费档 → 创建 Key。

**Module-② product variant (no key — {i18n:get_use}):** open the CONSUMER
entry (registry C7 whitelist domain, e.g. chat.deepseek.com — never the
developer console) → register/login → confirm a conversation works → point
out what the free tier includes (model version / caps, per this run's
evidence). Never mention API keys unless the user asks for the advanced
path.

**Claims discipline (every guidance message):** factual assertions inside
steps ("完全免费不限次数" / "国内直连") follow the same freshness rules as
rankings — this run's evidence with (source, date), or soften to "以官网
为准". Never claim a delivery form the evidence doesn't cover: a free app
does not prove a free API (`deal-hunting.md` §1 gate).

Adapt wording to the platform's actual UI and the user's language. If the
user reports a blocked step (CAPTCHA, region block, payment card needed),
troubleshoot with them conversationally; do not invent workarounds that cross
`references/safety.md` red lines.

---

## 5. After you have a key (any profile) — continue, don't drop

The intake already asked which tool the user runs (§0.3). **Don't offer —
continue:** load that `references/agents/…` doc and start the config
walkthrough in the same breath (base URL + key + model id), unless the user
declines. Then at most ONE extra line:

- the scheduled scan (`/scan`) — offered at the trust peak, to watch price
  drops / quota resets / promo expiry; or
- key hygiene (spending cap / rotation, `safety.md` §5) when any paid tier
  was touched.

Never dump a wall of follow-ups; never re-ask a question the intake already
answered.

---

## 6. Immediate persistence of findings

Significant discoveries made mid-flow — reachability blocks, signup-path
surprises, card requirements — are written to `vendor-cache.md` **as soon as
found** (dated entries in `notes`), not held until the end of the task. Host
tool rule: read the cache file before editing it.

---

## 7. Fallback ladder — every dead end lands somewhere soft

A dead end is never the end: the user must always land on a stated next
step. Six layers, walked top-down:

1. **Network:** direct blocked + no working proxy → stop pushing overseas;
   re-filter the ranking to direct-reachable candidates (`deal-hunting.md`
   §3.2, `ranking-template.md` §5) and recommend from those.
2. **Automation:** two automation failures → downshift L2 → L1 (§0.4), all
   progress kept.
3. **Capability:** no browser tool → guided install → user declines → L1.
4. **Platform:** registration impassable → ① another official entry of the
   same platform → ② a direct-reachable 🟢 alternative with similar models
   ("this one's free models are close — and it registers direct") → ③
   delivery downgrade (C7 login-and-use app, or a cheap membership).
5. **User ability:** the user can't complete even atomic assists →
   ultra-small-step L1 ("I say one step, you do one step") → still failing →
   switch to the lowest-friction platform (phone-number signup, domestic),
   or park with everything saved.
6. **Honesty:** whatever fails, say it plainly; save the checkpoint (§8) and
   give the exact resume line ({i18n:checkpoint_resume}). Never fake success.

---

## 8. Checkpoint & resume

After each completed stage, persist a checkpoint to `vendor-cache.md`
(`checkpoints`: platform · stage · date; stages = `preflight` / `intake` /
`submitted` / `email_verified` / `key_created` / `saved`).

On a later invocation for the same platform: read the checkpoint + account
ledger, re-verify state quickly (sessions expire), and resume from the
recorded stage with {i18n:checkpoint_resume} — never repeat questions
already answered, never redo stages already done.

> **Localize {stage}, never leak the enum.** The stored `stage` is an internal
> English token (`preflight`/`intake`/`submitted`/`email_verified`/
> `key_created`/`saved`). When filling the `{stage}` slot, map it to the
> localized `stage_*` i18n label (`{i18n:stage_intake}` → 刚开始登记信息, etc.,
> in `references/i18n/<lang>.json`) — a user must never see `intake`/`preflight`
> in plain output.
