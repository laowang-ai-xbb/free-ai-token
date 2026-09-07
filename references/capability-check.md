# Capability Check — probe what this host can actually do

Purpose: when a user wants auto-registration / automated browser steps, first
find out what the **current host** can actually do, and — where the user
wants automation — offer the missing capability. Never guess; probe.

> **Principle: probe capabilities, not names.** The same capability ships
> under different names on different hosts (skills, MCP servers, built-ins,
> renamed variants). Checking "is X installed?" by name can wrongly report
> "missing". Names are hints; **behavior is proof**.

---

## 1. Probe what the host can do (run once at the start of a reg/get-key task)

Check in this order and record results for the session (don't re-probe within
the same session):

| Capability | How to probe (name-agnostic) | If present |
|---|---|---|
| **Browser automation** | List available tools/skills; look for anything that can open a URL + observe the page (screenshot / snapshot / DOM read) + click / type. Confirm with a live micro-test: open `example.com`, take a snapshot. | browser-capable profile |
| **Live web search** | Any web-search tool/connector answers a trivial query | can hunt fresh deals |
| **Secure storage** | Can write a file with restricted permissions / call an OS keychain CLI / host credential store | keys can be stored per `auto-register.md` §3 ladder |
| **Persistent memory** | Host exposes a memory/ledger tool | cache & preferences persist (persistence ladder rung 1) |

Routing: browser automation present → `auto-register.md` §2. Absent → decide
whether to enable it (§2 below), else degrade to `auto-register.md` §4
hand-holding steps.

**Micro-test exception:** if the task's own first action already opens a real
page (e.g. a registration flow opening the vendor homepage), that navigation
doubles as the micro-test — do not open an extra example.com tab.

**Installed-app awareness:** when the flow will ask "where to configure the
key", probe the user's installed apps/clients first — intake options may only
list tools the user actually has. Never offer a target app that isn't
installed.

**Probe boundary:** all network / proxy probing is **READ-ONLY**. Changing
proxy or network settings is never done by the skill — it requires the
user's explicit consent and is performed by the user personally.

---

## 2. Enabling a missing browser capability (only on explicit request)

**Non-blocking by default:** automation adds convenience; its absence never
blocks the core value (hunt / rank / teach / guide all work without a
browser). Never over-pursue installation at the cost of the main task.

Only attempt when the user has **explicitly** asked for automated
registration AND the host offers an install mechanism:

1. **Confirm the gap is real.** Probe behavior, not names (§1). An equivalent
   capability under another name may already provide it — if so, use it and
   skip install.
2. **Disclose & ask first (hard gate).** In one message: the exact component
   name, exactly where it will come from, and what capabilities it will gain.
   Proceed only on explicit user consent for that install. Do not expand
   "user wants automation" into "install by default".
3. **Sources, in order:** the host's official/curated marketplace → the
   vendor's own official domain → any other source ONLY with the user's
   explicit per-source approval. Never from arbitrary git repos, forum
   links, or unknown mirrors. Record exactly where it came from.
4. **Install, then verify** by re-probing behavior (§1 micro-test). Not
   usable = failed.
5. **Retry budget = 3** across sources/variant names. After 3 failures, stop
   auto-installing and go to §3.

---

## 3. Guided install (after failed auto-install, or no install mechanism)

Do **not** keep silently retrying. Tell the user plainly and show the
benefit:

> 自动补装试了 3 次没成功。原因是 {…: 当前环境没有可用的浏览器自动化安装通道 /
> 源不可达}。
> **为什么需要它：** 有了浏览器自动化，我就能替你自动打开平台、填注册、过验证、
> 点「创建 Key」并把它安全存好，你基本不用动手。没有它，我只能一步步教你手动点
> （也完全能用，只是要你操作几步）。
> 安装方式（任选其一）：
>   1) 在 {host} 的「技能/插件市场」搜索安装官方浏览器自动化组件（约 1 分钟）；
>   2) 或告诉我具体组件名和来源，经你确认后我帮你装；
>   3) 先不装 —— 我直接手把手教你手动注册取 Key（无浏览器版流程照常可用）。

Then respect whatever the user chooses. If they decline, proceed with the
hand-holding flow in `auto-register.md` §4.

---

## 4. Fall back gracefully, never fake it

- If no browser automation after all attempts, use the **plain hand-holding**
  flow. Never claim a browser action "ran" when it did not.
- Automation adds convenience; its absence never blocks the core value
  (hunt / rank / teach / guide still all work without a browser).
- After this task, note which capabilities the host has so future runs in the
  same session skip redundant probing.
