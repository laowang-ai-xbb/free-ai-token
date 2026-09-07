<div align="center">

# 🪙 free-ai-token

**全球 AI 省钱管家 —— 以 Agent 技能（Skill）的形式。**
帮你找到**免费的 AI API token、免费 AI 产品、最划算的 AI 会员**（含土耳其/阿根廷等区域价），中立评分，端到端代办到位。

[English](./README.md) | [简体中文](./README.zh-CN.md)

![version](https://img.shields.io/badge/version-2.9.5-blue) ![license](https://img.shields.io/badge/license-MIT-green) ![format](https://img.shields.io/badge/Agent%20Skills-SKILL.md-orange) ![i18n](https://img.shields.io/badge/i18n-en%20%7C%20zh-success)

一个 [Agent Skill](https://agentskills.io) 开放标准技能：*免费token · 白嫖AI · 低价API · 便宜AI会员 · 免费 AI 产品 · 怎么免费用AI · 区域价 · Claude / OpenAI / Gemini 免费额度 · free AI API · cheapest LLM API · agent skill*

<!-- TODO: 替换为真实演示 GIF（30 秒以内） -->
<!-- ![demo](assets/demo.gif) -->

</div>

---

## ⚡ 安装（一行命令）

```bash
npx skills add laowang-ai-xbb/free-ai-token
```

- **前提条件**：任何支持 [Agent Skills](https://agentskills.io) 开放标准的客户端（Claude Code、Claude Desktop、千问办公、Cursor、Codex、Gemini CLI 等），且**已开启联网能力**（WebSearch/WebFetch）——现场核实是本技能的核心，断网等于残废。`npx` 需要 Node.js 18+。
- **不会用命令行？手动安装**：到 [Releases](../../releases) 下载最新 zip，解压放进你客户端的技能目录（如 `.claude/skills/free-ai-token/`）即可。
- **卸载**：删掉那个文件夹。

第一次听说 Agent Skill？它就是一个带 `SKILL.md` 说明书的技能文件夹，AI 助手在需要时按需加载——不需要 API Key、不需要配置。装好后直接对助手说人话。

## 🤔 它解决什么问题？

直接问大模型"哪家 AI 免费"，你会得到**过时、混杂、经常出错**的答案——免费*网页版*和免费 *API 额度*被混为一谈，区域价会员则埋在论坛帖子里。

**free-ai-token 是一套"活的流程"，不是一段"死的介绍"。** 你的 AI 助手会实时检索信息源、到厂商官方页面现场核实、按公开规则中立打分，再手把手帮你配置到位——你不用再读十篇博客，直接开始用。

### 三种交付形态 —— 严格分开，绝不混装

这是网上 AI 省钱内容最大的坑，本技能从机制上杜绝：

| 模块 | 你拿到什么 | 例子 |
|---|---|---|
| **① API token** | 官方平台的免费额度 API Key → 帮你接进常用工具 | "给我一个免费的大模型 API Key，接进 Cherry Studio" |
| **② 免费 AI 产品** | 登录即用的消费端产品——**不涉及任何 Key** | "不花钱，我能用上哪些 AI？" |
| **③ 会员计划** | 付费方案（含**区域价**：土耳其/印度/阿根廷等），价格与价值分开算 | "最划算的正版 Claude Plus 途径" |

> **DeepSeek 判例**：网页/App 免费，官方 API 按量付费（截至 2026-09，会话内重新核实）——网上大量内容把这两件事说混。本技能会先确认你问的是哪一侧。

## ✨ 跟别的"AI 省钱清单"有什么不同

- **🔍 现场核实，不靠记忆**——每条结论都在会话中到厂商官方页面验证（可达的前提下），并标注来源和日期。
- **⚖️ 中立评分**——评分模型公开（`references/scoring.md`）、徽章分级透明；无广告、无返利链接。
- **🧾 编号卡片式产出**——每条推荐都是可执行的编号步骤卡 + 官方直达链接，看完就能动手。
- **🔌 端到端代办**——注册、购买、把 Key 接入 Cherry Studio / Chatbox / NextChat / LobeChat / Dify 及任何 OpenAI 兼容客户端。
- **📅 优惠扫描**——`/deals` 做一次性市场扫描；`/scan` 设置重复扫描清单（**需要客户端支持定时调度**）。
- **🌍 中英双语**——自动识别你用中文还是英文，用什么语言问就用什么语言答。
- **🛡️ 实话实说**——不免费的东西明确告诉你"不免费"（见上面的 DeepSeek 判例），不画饼。

## 💬 用法 —— 直接说人话

<details open>
<summary><b>中文触发说法</b></summary>

- “怎么**免费用**AI？”
- “有没有**免费 token / 免费 API Key**？”
- “哪家大模型 API **最便宜**？”
- “**便宜 AI 会员**有没有？土耳其区/阿根廷区还值不值？”
- “帮我**接入**一个免费模型到 Cherry Studio。”
- “**扫描**一下这周有没有 AI 优惠。”

</details>

<details>
<summary><b>英文触发说法</b></summary>

- "How can I use AI for **free**?"
- "Find me the **cheapest API** for coding / long context / image generation."
- "Is there a **free tier** for Claude / OpenAI / Gemini?"
- "Get me a free API key and **wire it into Chatbox**."
- "**Scan** for AI membership deals this week."

</details>

### 斜杠命令

| 命令 | 作用 |
|---|---|
| `/deals` | 一次性扫描当前免费额度与会员优惠 |
| `/scan` | 定时盯价扫描（需客户端支持定时调度） |

## 📦 你会拿到什么

- **排序编号卡片**——带徽章的最佳推荐：价格、限制、官方直达链接。
- **完整 HTML 报告**（`assets/templates/full-report.html`）——整场市场扫描的可分享一页纸。
- **即贴即用配置**——OpenAI 兼容接口的配置片段（`assets/templates/openai-compatible-config.md`）。
- **厂商缓存**（`assets/vendor-cache.md`）——主要厂商的信息快照，标注日期、每次运行重新核实（定时月更在[路线图](#%EF%B8%8F-路线图)中）。

## 🗂️ 仓库结构（给人看，也给 AI 看）

```text
free-ai-token/
├── README.md / README.zh-CN.md  # 你正在看的文件
├── SKILL.md                     # 技能入口——AI 和人都先看这个
├── LICENSE                      # MIT 协议
├── CHANGELOG.md                 # 更新日志
├── references/
│   ├── deal-hunting.md          # 实时信息猎取与核实流程
│   ├── ranking-template.md      # 输出卡片格式（三模块 + best_pick 资格）
│   ├── scoring.md               # 中立评分模型与徽章等级
│   ├── vendor-registry.md       # 厂商清单、模块映射、官方链接
│   ├── self-check.md            # 14+ 条金标准测试用例
│   ├── safety.md                # 合规与用户保护规则
│   ├── auto-register.md         # 可选的协助注册（默认关闭，需显式开启）
│   ├── buy-membership.md        # 区域价购买指引
│   ├── capability-check.md      # 结论对照官方页面核实
│   ├── commands.md              # /deals · /scan 行为定义
│   ├── discovery-sources.md     # 优惠信息从哪找
│   ├── agents/                  # 客户端笔记：domestic-oss · fundamentals · international · troubleshooting
│   └── i18n/                    # en.json · zh.json 界面文案
└── assets/
    ├── templates/               # full-report.html · openai-compatible-config.md
    └── vendor-cache.md          # 厂商信息快照（标注日期）
```

<details>
<summary><b>🤖 给 AI 与集成者看</b></summary>

本技能遵循[渐进式披露](https://agentskills.io)架构：触发时只加载 `SKILL.md`（<300 行），`references/` 下的文件按需读取。触发匹配由头部 `description` 字段驱动：

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

输出纪律：结果永远是带模块编号（①/②/③）、徽章等级和官方链接的编号卡片，绝不输出随意的段落式推荐。

</details>

## ❓ 常见问题

<details>
<summary><b>这合法吗？</b></summary>

合法——它是一个"调研比价"工具，只指向官方免费额度和合法的区域定价，且永远给官方链接。各厂商服务条款需要你自己遵守；技能会标出已知的条款敏感步骤（见<a href="#%EF%B8%8F-安全与免责声明">安全与免责</a>）。

</details>
<details>
<summary><b>要花钱吗？</b></summary>

技能本身免费开源。当你的最优选择其实<b>不</b>免费时（比如 DeepSeek 官方 API 按量付费），它会如实告诉你——它的任务是让你不多花冤枉钱，不是许诺"全都白嫖"。

</details>
<details>
<summary><b>能在 ChatGPT 等其他助手里用吗？</b></summary>

支持 Agent Skills 开放标准的客户端都能用（据 <a href="https://agentskills.io">agentskills.io</a> 已有 40+ 工具）。它不是独立 App，需要一个能联网的宿主 AI 助手。

</details>
<details>
<summary><b>为什么不直接问 AI 就好？</b></summary>

因为通用模型靠"记忆"回答：价格过时、额度混装、不做核实。这个技能把"核实流程"写成了规矩——当次会话重新查官方页面、按公开模型打分、直接给你能执行的步骤。

</details>

## ⚠️ 安全与免责声明

- **默认只做调研。** 协助注册（`references/auto-register.md`）为**可选功能，默认关闭**——除非你明确要求，否则绝不运行，每一步都在屏幕上向你确认，支付环节永不自动操作。
- **"免费"指官方免费额度，不是盗版。** 本技能只推荐官方渠道与合法区域定价，不协助账号共享、滥用试用或绕过服务条款。
- **区域价**是厂商的合法区域定价，但请自行遵守各厂商服务条款；技能会标出已知的条款敏感步骤。
- **无返利、无赞助。** 排名完全来自可审计的公开评分模型。
- 价格与政策随时可能变化——技能在执行前总会重新核实。厂商名称与商标归其所有者所有。本项目仅供学习研究。

## 🗺️ 路线图

- [ ] 厂商缓存定时月更，发布在 Releases
- [ ] 更多客户端的接入指南（可提需求）
- [ ] 多区域价格追踪面板

功能建议 → [提个 issue](../../issues)。欢迎 PR——修改评分或排名逻辑时，请附一个真实厂商案例的修改前后对照。

## 👤 作者

**laowang-ai-xbb**（小红书：[@老王ai瞎bb](https://www.xiaohongshu.com)）

我做实用的 Agent 技能，让 AI 用起来更便宜、更省心。如果这个技能帮你省了钱或时间，一个 ⭐ 就是最好的燃料——issue 和 PR 也非常欢迎。

- 📮 反馈：[Issues](../../issues) · 欢迎开 Discussions
- 🔄 关注更新：点 **Watch** 即可收到优惠扫描动态
- 📕 中文教程与实战案例：小红书 @老王ai瞎bb

## 📜 开源协议

[MIT](./LICENSE) © laowang-ai-xbb (老王ai瞎bb)

---

<div align="center">

**如果它帮你省了钱，赏个 ⭐ 吧——免费的（token 也一样）。**

</div>
