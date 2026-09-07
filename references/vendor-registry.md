# Vendor Registry — coverage map only: who to scan, never what they charge

This registry answers ONE question before every FULL hunt: **"Did my search
cover every class of provider that can hand out free / low-cost LLM API
tokens?"** It is a *coverage map*, not a credibility endorsement and not a
price table. Trust and scoring come from `scoring.md`.

> **No quota / price / rate numbers live in this file.** Volatile facts
> belong only in `assets/vendor-cache.md` (with a verified-on date) and may
> be printed only after live verification this run — see the canonical
> freshness contract in `deal-hunting.md` §0.

> Why this file exists: pure real-time search only covers whatever the caller
> happened to remember that run. Providers like **AMD** and **NVIDIA** — GPU
> clouds that hand out free inference credits — are real free-token sources
> but easy to forget. This map makes coverage **checkable**, not luck-based.

---

## How to use it (mandatory, every FULL hunt)

1. Before searching, read the class list below.
2. Run **at least one query per class** (templates in `deal-hunting.md` §2).
3. After collecting results, run the **coverage self-check** (§ below) — if a
   class has zero candidates, say so explicitly in the output rather than
   silently omitting it.

> **Credibility filter:** every listed vendor has a verifiable formal company
> background (listed/major company · subsidiary of one · government-backed ·
> notable VC backing · reputable founding team). Free-tier policy still
> changes daily — every deal line must be live-verified before showing.

> **Reachability labels:** overseas vendors may carry a 直连/需代理 tag in
> output ONLY per `deal-hunting.md` §3.2 — never inferred from being
> overseas.

> **Official-link whitelist:** each class table's "官方入口 / Official link"
> column is the authoritative link source. Every clickable URL on a card or the
> HTML report must be that vendor's official domain from here — never a
> search-result URL, and (module ②) never a third-party price/aggregator site.

> **Per-card model naming:** a card's "免费 / Free" line names that platform's
> **strongest free model this run** (versioned), gated by `deal-hunting.md`
> §3.3 — only if a source shows that model on THIS platform's free tier.

---

## Module map (three delivery forms, three modules)

| Registry class | Renders in |
|---|---|
| C1 GPU cloud · C2 inference · C3 (API 侧) · C4 frontier · C5 aggregators | **Module ①** API token 平台（{i18n:get_key}） |
| C7 app-bundled + C3/C2 厂商的**消费级聊天产品** | **Module ②** 免费 AI 产品（{i18n:get_use}，免 Key） |
| C6 memberships | **Module ③** 会员计划（{i18n:membership}） |

**One vendor may occupy TWO modules — as two separate entries, never one
merged card**: 智谱 → BigModel API（open.bigmodel.cn，①）+ 智谱清言
（chatglm.cn，②）; DeepSeek → platform.deepseek.com（①，付费）+
chat.deepseek.com（②，免费）; Kimi → platform.moonshot.cn（①）+
kimi.moonshot.cn（②）. Each entry links to its OWN official domain
(delivery-form gate, `deal-hunting.md` §1).

---

## Class map

### C1. GPU cloud / inference-cloud free tiers ← high-value, easy to forget

Free inference credits from hardware vendors + hyperscaler clouds.

| Vendor | Backing (why it qualifies) | Official link | Verify each run |
|---|---|---|---|
| NVIDIA (NIM / build.nvidia.com) | NVIDIA Corp., listed, global GPU leader | build.nvidia.com | free credits exist? size? RPM cap? business-email uplift? |
| AMD (ROCm / partner inference tiers) | AMD Corp., listed | amd.com | any current free/partner inference tier? terms? |
| AWS (Bedrock via Free Tier) | Amazon, listed | aws.amazon.com/free | new-account credits current? size/expiry? Bedrock coverage? |
| Microsoft Azure (AI Foundry / Azure AI) | Microsoft, listed | azure.microsoft.com/free | trial credits? always-free models? expiry? PTU option? |
| Google Cloud (Vertex AI + Gemini API free tier) | Alphabet, listed | cloud.google.com/free · aistudio.google.com | trial credits? Gemini free-tier caps per model? data-training region note? |
| GMI Cloud | VC-backed GPU cloud (H100/H200 infra) | gmicloud.ai | free endpoints still up? which models? card needed? |
| Lambda · RunPod · Baseten · Modal · Replicate | VC-backed infra startups | respective sites | signup credits current? sizes? (treat as secondary) |
| Newer/smaller GPU clouds: DataCrunch · Jarvis Labs · E2E Networks (listed, India) · TensorDock · Latitude.sh | VC-backed or listed infra (verify each) | respective sites | signup/free credits current? sizes? card required? (volatile — expect churn) |
| Telecom-affiliated clouds (intl): SK Telecom/KT Cloud · NTT · T-Systems / Open Telekom Cloud · Orange | subsidiaries of major telecom groups | respective portals | any free LLM/inference credits at all? terms? (unproven in many cases — verify before promising) |

### C2. Dedicated inference providers (fast / cheap / open models)

| Vendor | Backing | Official link | Verify each run |
|---|---|---|---|
| Groq | Groq Inc., VC-backed (LPU silicon) | console.groq.com | free tier exists? card-free? current RPM/RPD caps? model catalog? |
| Cerebras | Cerebras Systems, VC-backed, wafer-scale chips | cloud.cerebras.ai | free tier? daily token cap? current catalog (volatile — never hardcode model names)? |
| Google AI Studio (Gemini) | Alphabet | aistudio.google.com | free-tier request caps per model? data-training note? |
| Mistral La Plateforme | Mistral AI, major-VC-backed | console.mistral.ai | Experiment tier alive? catalog incl. Codestral/Devstral? data-training default? |
| OpenRouter | Aggregator + router | openrouter.ai | free-suffix model count? deposit-gated higher tier terms? |
| Cloudflare Workers AI | Cloudflare, listed | cloudflare.com | free daily allowance current? model list? |
| Hugging Face Inference Providers | HF, known open-source community company | huggingface.co | free monthly inference credit current? routing partners? |
| GitHub Models | Microsoft (GitHub), listed | github.com/marketplace/models | free tier for any GitHub account? per-plan rate limits (Copilot uplift)? catalog? OpenAI-compatible endpoint (models.inference.ai.azure.com)? |
| Together AI | VC-backed open-model infra | together.ai | signup credit current? size/expiry? free serverless models? non-commercial clause? |
| Fireworks AI | VC-backed inference infra | fireworks.ai | signup credit current? serverless free quota? card required? |
| Databricks | Databricks Inc., listed (lakehouse) | databricks.com | free serverless / Community tier with Foundation Models APIs? trial credits? (re-classify vs C1 hyperscalers each run) |
| Kluster AI | VC-backed, EU-hosted inference | kluster.ai | free tier alive? EU-hosting claim current? caps? card needed? |
| Ollama Cloud | Ollama team (open-source local runtime) | ollama.com | cloud free tier exists? quota? non-OpenAI API format (own SDK) — flag in card? still primarily local? |
| DeepInfra · Hyperbolic · Nebius · Novita · SambaNova · Cohere · AI21 · Scaleway · OVH | VC-backed / listed infra | respective sites | trial/free credits current? sizes? non-commercial clauses? |

### C3. Chinese / domestic model APIs (China-relevant)

| 厂商 | 背景 | 官方入口 | 本轮核实 |
|---|---|---|---|
| 智谱 AI (GLM) | 清华系，知名创业团队，多轮融资 | open.bigmodel.cn | 新用户额度现状？免费 Flash 系列档现状（并发限制）？邀请活动？ |
| DeepSeek | 深度求索，幻方量化背景 | platform.deepseek.com | **官方 API 无免费档（2026-09-05 核实）**——按量付费；"免费 DeepSeek API"只在第三方平台，逐家过 §3.3。消费端网页/App 归 C7·模块② |
| 阿里云百炼 (通义 Qwen) | 阿里巴巴旗下 | dashscope.console.aliyun.com | 新用户额度？每模型免费额度与期限？Token Plan 档位？ |
| 字节火山引擎 (豆包/Seed) | 字节跳动旗下 | console.volcengine.com/ark | 每日免费额度现状（是否按天刷新）？Coding Plan？ |
| 腾讯混元 | 腾讯旗下 | cloud.tencent.com/product/tclm | lite 免费档现状？新用户额度与有效期？ |
| 月之暗面 Kimi | 知名独角兽 | platform.moonshot.cn | 免费档限频现状？认证赠额？上下文长度？ |
| 硅基流动 SiliconFlow | 知名创业平台 | cloud.siliconflow.cn | 免费 RPM 档覆盖哪些模型？新用户赠额？ |
| ModelScope 魔搭 | 阿里达摩院旗下 | modelscope.cn | 每日免费调用次数现状？深度推理档？多模态？ |
| 百度千帆 (ERNIE) | 百度旗下 | cloud.baidu.com/product/wenxinworkshop | 新客额度与有效期？QPS？ |
| 科大讯飞星火 | 科大讯飞（上市） | xinghuo.xfyun.cn | 个人/企业免费包额度与期限？Lite API？ |
| MiniMax · 阶跃星辰 · 昆仑万维天工 · 商汤日日新 · 360智脑 · 小米 MiMo | 各自知名公司背书 | respective portals | 政策变动频繁，每次现查（含新活动） |
| 运营商系云：移动云（九天）· 天翼云（电信）· 联通云（元景） | 三大运营商旗下 | respective portals | 大模型 API 免费额度现状？新用户条件？（额度政策变动快，数字一律现查） |

> C3 列的都是 **API 侧**（模块①）。同厂商的消费级聊天产品（智谱清言、
> DeepSeek 网页/App、Kimi 网页/App、腾讯元宝、通义…）在 C7·模块② 单列，
> 两侧证据互不外推（`deal-hunting.md` §1 交付形态闸门）。

### C4. Frontier-lab official access (OpenAI / Anthropic / Google…)

| Vendor | Backing | Official link | Verify each run |
|---|---|---|---|
| Google (Gemini API / AI Studio / Gemini CLI) | Alphabet | aistudio.google.com | free tier per C2 row; CLI availability |
| Anthropic (Claude) | major-VC-backed | anthropic.com | any short-term credit promo now? (no standing free tier) |
| OpenAI | Microsoft-aligned | platform.openai.com | any current promo credits? (no standing free tier) |
| xAI (Grok) · Cohere · Mistral · Meta (via partners) | known / big funding | respective sites | trial keys alive? non-commercial clauses? |

### C5. Cheap OpenAI-compatible aggregators / relays (🟡 vet hard)

- Watch-list only: one-api/new-api panel channels, various relay resellers.
- Listed because users ask for "cheapest possible"; almost always 🟡/🔴.
  Radar queries: `deal-hunting.md` §2.2.
- Victims of gamed forums — score from evidence only (`scoring.md`).
- 提示：很多所谓"白菜价 10 倍低价 key"实为盗刷/共享 key，🔴 且涉嫌违法
  （`safety.md` §3）。

### C6. AI membership subscriptions & region pricing (module ③)

Scope: **any AI subscription** — chat, image, video, audio, music, 3D.
Render order follows the three shelves of `ranking-template.md` §2 module ③:
**official discounts first** (education / annual / first-year / promo — see
the "Verify each run" column), **carrier bundles second**, **cross-region
prices last** (🟡, banner + worst-case line before any steps).

**Official-link whitelist (module ③ CTAs — the only linkable domains):**
ChatGPT Plus/Pro → chatgpt.com · Claude Pro/Max → claude.ai · Gemini
Advanced → gemini.google.com · Perplexity Pro → perplexity.ai · Copilot Pro →
github.com/features/copilot · Midjourney → midjourney.com · Suno → suno.com ·
ElevenLabs → elevenlabs.io · NotebookLM+ → notebooklm.google.com ·
可灵/即梦 → klingai.com / jimeng.jianying.com. Third-party price trackers
(opentherank, geosub, aisubprice…) are citation-only, never hrefs.

| Product | Owner | Verify each run |
|---|---|---|
| ChatGPT Plus/Pro · Copilot Pro · Claude Pro/Max · Gemini Advanced · Perplexity Pro · Midjourney · NotebookLM+ · Suno · Kling/可灵/即梦 · ElevenLabs | respective majors / known startups | official price · education/first-year/annual discounts · region-price spread + ToS stance (🟡/🔴, banner mandatory) |
| Carrier-bundled AI memberships (e.g. SoftBank × Perplexity Pro) | telecom carriers × AI vendors | bundle alive? eligibility (plan/region)? effective cost? |

### C7. Free AI products — sign in and use, no API key (module ②)

Consumer chat products + coding apps/CLIs that bundle free model access —
the user signs in and uses it directly; **no API key involved**. Highest
value for beginners; verify every run, **per surface** (网页 / 电脑客户端 /
手机 App) and per free model VERSION (`deal-hunting.md` §2.8).

| Product | Backing | Official link (consumer entry) | Verify each run |
|---|---|---|---|
| DeepSeek 网页/App | 深度求索 | chat.deepseek.com | 各端免费模型版本（对话/深度思考/联网）？每日上限？注意：官方 API 无免费档（①侧付费） |
| 豆包 | 字节跳动 | www.doubao.com | 网页/App/电脑端免费功能（对话/写作/画图）与模型版本？上限？ |
| 智谱清言 | 智谱 | chatglm.cn | 免费模型版本（含画图/视频）？与 BigModel API（①侧）分列 |
| Kimi 网页/App | 月之暗面 | kimi.moonshot.cn | 免费档模型版本与上限？platform.moonshot.cn 属①侧 |
| 腾讯元宝 · 通义 · 夸克AI | 腾讯 / 阿里 | yuanbao.tencent.com · tongyi.aliyun.com | 各端免费模型与上限，每轮现查 |
| GitHub Copilot (Free tier) | Microsoft/GitHub, listed | github.com/features/copilot | free tier alive? monthly chat/completion caps? model list? |
| Gemini CLI | Alphabet | github.com/google-gemini/gemini-cli | free quota via personal Google account current? caps? |
| Qwen Code | 阿里巴巴 | qwenlm.github.io | free OAuth quota current? caps? |
| iFlow CLI | 心動系创业公司 | platform.iflow.cn | free model quota current? which models? |
| Windsurf · Trae · OpenCode · OpenClaw 等代理/编程应用 | known vendors / VC-backed | respective sites | built-in free models/credits current? caps? card needed? |

Note: C7 entries answer "use free models without an API key" — registration
flows for them skip the key-capture steps entirely (`auto-register.md`), and
the close uses {i18n:footer_next_use}, never the get-key wording.

---

## Coverage self-check (single source of truth)

Render the coverage line from the one canonical string `{i18n:coverage_line}`
(`references/i18n/<lang>.json`) — do **not** maintain a second copy of the
coverage wording here. This file's only job is to define the 7 classes.

_(If any class found nothing fresh, append e.g. "GPU-cloud: no current
verified free tier found this scan." — never silently drop it.)_

---

## Seed back-fill (回灌) — into the cache, not into this file

When a discovery source (`discovery-sources.md`) surfaces a provider you have
never seen:

1. Verify with ≥2 independent sources OR the official page.
2. Confirmed → write it into `assets/vendor-cache.md` (right class, today's
   date, risk tier, source) — **not into this registry**. Keep it in the
   session cache too and flag "NEW" in this run's ranking.
3. Do NOT add scammy / one-snippet-only / pure-promo claims. Unverified →
   discard or keep in the cache's `unverified_heard_of` note — never in the
   ranked table.
4. **Backing check:** before seeding, the vendor must clear at least one of —
   listed/major company · subsidiary of one · government-backed · notable VC
   · reputable founding team. Unknown-shell relays never qualify, whatever
   they promise.

**Map maintenance:** add/remove rows here only when a whole class genuinely
changes; bump the skill's `updated` stamp when editing. Day-to-day volatility
is the cache's job, not this map's.
