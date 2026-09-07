<div align="center">

# 🪙 free-ai-token

**Global AI money-saver — as an Agent Skill.**
Find **free AI API tokens, free-to-use AI products, and the cheapest AI memberships** (incl. region pricing), scored neutrally and set up for you end-to-end.

[English](./README.md) | [简体中文](./README.zh-CN.md)

![version](https://img.shields.io/badge/version-2.9.5-blue) ![license](https://img.shields.io/badge/license-MIT-green) ![format](https://img.shields.io/badge/Agent%20Skills-SKILL.md-orange) ![i18n](https://img.shields.io/badge/i18n-en%20%7C%20zh-success)

An [Agent Skill](https://agentskills.io) for: *free AI API keys · cheapest LLM API · free-tier comparison · Claude / OpenAI / Gemini free tier · AI membership region deals (Turkey / India / Argentina) · 免费token · 白嫖AI · 低价API · 便宜AI会员*

<!-- TODO: replace with a real demo GIF (≤30s) -->
<!-- ![demo](assets/demo.gif) -->

</div>

---

## ⚡ Install（一行安装）

```bash
npx skills add laowang-ai-xbb/free-ai-token
```

- **Requirements**: any [Agent Skills](https://agentskills.io)-compatible client (Claude Code, Claude Desktop, QwenWork, Cursor, Codex, Gemini CLI and more) with **web access enabled** (WebSearch/WebFetch) — live verification is the core of this skill. Node.js 18+ is needed for `npx`.
- **No terminal? Manual install**: download the latest zip from [Releases](../../releases), unzip it into your client's skills directory (e.g. `.claude/skills/free-ai-token/`), done.
- **Uninstall**: delete that folder.

New to Agent Skills? A skill is just a folder with a `SKILL.md` playbook that your AI agent loads on demand — no API key, no config. Install it, then talk to your agent in plain language.

## 🤔 What problem does it solve?

Asking an LLM "which AI service is free?" gets you **outdated, blended, often wrong** answers — free *web apps* get mixed up with free *API tiers*, and region-priced memberships are buried in forum posts.

**free-ai-token is a living procedure, not a paragraph.** Your agent hunts live sources, verifies against the vendor's official page in-session, scores neutrally, and walks you through setup — so you stop reading ten blog posts and start using the thing.

### The three delivery forms — strictly separated

This skill never blends them in one recommendation (the #1 source of bad advice):

| Module | What you get | Example |
|---|---|---|
| **① API tokens** | Free-tier API keys from official platforms → wired into your favorite tool | "Get me a free LLM API key and wire it into Cherry Studio" |
| **② Free AI products** | Sign-in-and-use products — **no key involved** | "What can I use AI for without paying anything?" |
| **③ Memberships** | Paid plans incl. **region deals** (Turkey / India / Argentina …), price vs. value scored | "Cheapest legit way to get Claude Plus" |

> **DeepSeek rule of thumb**: the web app is free, the official API is pay-per-use (as of 2026-09; re-verified in-session). Most content online gets this wrong. This skill checks which side you're actually asking about.

## ✨ Why it's different

- **🔍 Live-verified, not memorized** — every claim is checked against the vendor's official page during the session (where reachable), and findings carry a source + date.
- **⚖️ Neutral scoring** — a transparent scoring model (`references/scoring.md`) with badge levels; no sponsorships, no affiliate links.
- **🧾 Numbered result cards** — every recommendation is an executable step-by-step card with an official link, so you can act, not just read.
- **🔌 End-to-end setup** — registering, buying, and wiring keys into Cherry Studio / Chatbox / NextChat / LobeChat / Dify and any OpenAI-compatible client.
- **📅 Deal scans** — `/deals` runs a one-shot market scan; `/scan` sets up a recurring watchlist **on hosts that provide a scheduler**.
- **🌍 Bilingual** — auto-detects English/Chinese and replies in your language.
- **🛡️ Honest about limits** — tells you when something *isn't* free (see the DeepSeek rule above) instead of promising freebies.

## 💬 Usage — just say it

<details open>
<summary><b>English triggers</b></summary>

- "How can I use AI for **free**?"
- "Find me the **cheapest API** for coding / long context / image generation."
- "Is there a **free tier** for Claude / OpenAI / Gemini?"
- "Get me a free API key and **wire it into Chatbox**."
- "**Scan** for AI membership deals this week."

</details>

<details>
<summary><b>中文触发词</b></summary>

- “怎么**免费用**AI？”
- “有没有**免费 token / 免费 API Key**？”
- “哪家大模型 API **最便宜**？”
- “**便宜 AI 会员**有没有？土耳其区/阿根廷区还值不值？”
- “帮我**接入**一个免费模型到 Cherry Studio。”
- “**扫描**一下这周有没有 AI 优惠。”

</details>

### Slash commands

| Command | What it does |
|---|---|
| `/deals` | One-shot scan of current free tiers & membership deals |
| `/scan` | Recurring watchlist scan (requires a host with a scheduler) |

## 📦 What you get

- **Ranked, numbered cards** — top picks with badges, prices, limits, and direct official links.
- **Full HTML report** (`assets/templates/full-report.html`) — a shareable one-pager of the whole market scan.
- **Ready-to-paste configs** — OpenAI-compatible endpoint snippets (`assets/templates/openai-compatible-config.md`).
- **Vendor cache** (`assets/vendor-cache.md`) — a curated, dated snapshot of major vendors, re-verified on every run (a scheduled monthly refresh is on the [roadmap](#-roadmap)).

## 🗂️ Repository structure (for humans *and* agents)

```text
free-ai-token/
├── README.md / README.zh-CN.md  # You are here
├── SKILL.md                     # Skill entry point — agents start here
├── LICENSE                      # MIT
├── CHANGELOG.md
├── references/
│   ├── deal-hunting.md          # Live sourcing & verification procedure
│   ├── ranking-template.md      # Output card formats (3 modules, best_pick rules)
│   ├── scoring.md               # Neutral scoring model & badge levels
│   ├── vendor-registry.md       # Known vendors, module mapping, official links
│   ├── self-check.md            # 14+ golden test cases for output quality
│   ├── safety.md                # Compliance & user-protection rules
│   ├── auto-register.md         # OPTIONAL assisted sign-up (default OFF, opt-in)
│   ├── buy-membership.md        # Region-deal purchase walkthrough
│   ├── capability-check.md      # Verify claims against official pages
│   ├── commands.md              # /deals · /scan behavior
│   ├── discovery-sources.md     # Where deals are found
│   ├── agents/                  # Client notes: domestic-oss · fundamentals · international · troubleshooting
│   └── i18n/                    # en.json · zh.json display labels
└── assets/
    ├── templates/               # full-report.html · openai-compatible-config.md
    └── vendor-cache.md          # Dated vendor snapshot
```

<details>
<summary><b>🤖 For AI agents &amp; integrators</b></summary>

The skill follows [progressive disclosure](https://agentskills.io): on trigger only `SKILL.md` (<300 lines) is loaded; everything under `references/` is read on demand. Trigger matching is driven by the frontmatter `description`:

```yaml
---
name: free-ai-token
description: "Global AI money-saver: find FREE or cheap LLM API tokens/keys, free AI
  apps (no key), and low-cost AI memberships (region deals for Claude/OpenAI/Gemini);
  wires keys into agents (Cherry Studio/Chatbox/NextChat/LobeChat/Dify); scheduled
  scans via /deals /scan. 免费token · 白嫖AI · 低价API · 便宜AI会员 · cheapest API ·
  free API key. NOT for general AI pricing questions or ordinary chat/translation."
version: "2.9.5"
---
```

Output discipline: results are always numbered cards with the module ID (①/②/③), a badge level, and an official link — never a free-form paragraph.

</details>

## ❓ FAQ

<details>
<summary><b>Is this legal?</b></summary>

Yes — it's a research-and-compare tool. It points to official free tiers and legitimate regional pricing, always linking to official pages. You are responsible for complying with each vendor's Terms of Service; the skill flags known ToS-sensitive steps (see <a href="#%EF%B8%8F-safety--disclaimer">Safety</a>).

</details>
<details>
<summary><b>Does it cost anything?</b></summary>

The skill itself is free and open-source. It will tell you honestly when your best option is <i>not</i> free (e.g. DeepSeek's API is pay-per-use) — its job is to stop you overpaying, not to promise freebies.

</details>
<details>
<summary><b>Does it work with ChatGPT / other assistants?</b></summary>

It works with any client that supports the Agent Skills standard (40+ tools per <a href="https://agentskills.io">agentskills.io</a>). It is not a standalone app and needs a host agent with web access.

</details>
<details>
<summary><b>Why not just ask my AI directly?</b></summary>

Because a general model answers from memory: outdated prices, mixed-up tiers, no verification. This skill encodes a verification procedure — it re-checks the official page <i>this</i> session, scores options against a published model, and hands you executable steps.

</details>

## ⚠️ Safety & disclaimer

- **Read-only research by default.** Guided sign-up (`references/auto-register.md`) is **optional and opt-in** — it never runs unless you explicitly ask, every step is confirmed on screen, and payment steps are never automated.
- **"Free" means free tiers, not piracy.** The skill only recommends official channels and legitimate regional pricing; it does not assist with account sharing, abuse of trials, or ToS circumvention.
- **Region deals** are legitimate regional pricing, but you are responsible for complying with each vendor's Terms of Service. Known ToS-sensitive steps are flagged in-app.
- **No affiliate links, no sponsors.** Rankings come from a published scoring model you can audit.
- Prices and policies change without notice — the skill always re-verifies before acting. Vendor names and trademarks belong to their owners. This project is for learning and research.

## 🗺️ Roadmap

- [ ] Scheduled monthly vendor-cache refresh, published in Releases
- [ ] More agent wiring guides (per-request)
- [ ] Multi-region price tracker dashboard

Feature requests → [open an issue](../../issues). PRs welcome — for changes to scoring or ranking logic, please include a before/after example on a real vendor case.

## 👤 Author

**laowang-ai-xbb**（小红书：[@老王ai瞎bb](https://www.xiaohongshu.com)）

I build practical Agent Skills that make AI cheaper and easier to use. If this skill saved you money or time, a ⭐ is the best fuel — and issues/PRs are very welcome.

- 📮 Feedback: [Issues](../../issues) · Discussions welcome
- 🔄 Follow the project: click **Watch** to get deal-scan updates
- 📕 Chinese tutorials & real-world cases: 小红书 @老王ai瞎bb

## 📜 License

[MIT](./LICENSE) © laowang-ai-xbb (老王ai瞎bb)

---

<div align="center">

**If this saved you money, consider giving it a ⭐ — it's free (like the tokens).**

</div>
