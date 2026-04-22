---
description: AI 行业日报/信息雷达 - 追踪 AI 领域 KOL 的最新访谈、演讲、推文和播客动态
allowed-tools: [Read, Bash, WebFetch, Write, Grep, Glob]
---

# AI Radar - Daily AI Intelligence Digest

生成每日 AI 行业情报日报。从 YouTube 频道、AI 播客、X (Twitter) KOL 三大数据源抓取内容，经过筛选、匹配、翻译后生成中文日报。

## 前置条件

本 skill 依赖一个 [RSSHub](https://github.com/DIYgod/RSSHub) 实例来抓取数据。

**必需配置：** 将下方的 `RSSHub base URL` 替换为你自己的 RSSHub 实例地址。

**Twitter/X 数据源（可选）：** 需要在 RSSHub 实例中配置 Twitter 认证。推荐使用浏览器 Cookie 方式（最简单、无额度限制）：

1. 在浏览器中登录 [x.com](https://x.com)
2. 按 F12 → Application → Cookies → `https://x.com`
3. 复制 `auth_token` cookie 的值
4. 在 RSSHub 实例中设置环境变量：`TWITTER_AUTH_TOKEN=你的auth_token值`

也可使用 Twitter API v1.1 密钥（需要 4 个环境变量）：
- `TWITTER_CONSUMER_KEY` — API Key
- `TWITTER_CONSUMER_SECRET` — API Key Secret
- `TWITTER_ACCESS_TOKEN` — Access Token
- `TWITTER_ACCESS_SECRET` — Access Token Secret

> 如未配置 Twitter，skill 会正常运行但跳过 Twitter 板块，在日报中标注"接入中"。

## 数据源总览

| 类型 | 数量 | 说明 |
|------|------|------|
| YouTube 频道 | 12 个 | 通过 RSSHub 抓取 |
| AI 播客 | 5 个 | 直接订阅 RSS |
| X/Twitter KOL | 22 位 | 通过 RSSHub Twitter 路由抓取 |

---

## 1. YouTube 频道 KOL 追踪

### KOL 列表

| Name | Role | Company | Keywords |
|------|------|---------|----------|
| Kevin Weil | CPO | OpenAI | Kevin Weil, OpenAI CPO, OpenAI product |
| Christopher Petregal | Founder & CEO | Granola | Christopher Petregal, Chris Petregal, Granola AI |
| Nan Yu | Head of Product | Linear | Nan Yu, Linear product |
| Raiza Martin | Former Product Lead | Google (NotebookLM) | Raiza Martin, NotebookLM |
| Josh Woodward | VP Google Labs & Gemini | Google | Josh Woodward, Google Labs |
| Amanda Askell | Character Lead for Claude | Anthropic | Amanda Askell, Claude character, Claude personality |

### YouTube 频道列表

RSSHub base URL: `https://scarlettliu.zeabur.app`

**AI 播客与访谈频道**
- `/youtube/user/@lexfridman` — Lex Fridman (AI 长访谈)
- `/youtube/user/@NoPriorsPodcast` — No Priors (AI/ML 创业播客)
- `/youtube/user/@a16z` — a16z (VC/AI 内容)
- `/youtube/user/@20VC` — 20VC Harry Stebbings (VC/创始人播客)
- `/youtube/user/@LennysPodcast` — Lenny's Podcast (产品/技术)
- `/youtube/user/@ycombinator` — Y Combinator (创业/AI)

**公司官方频道**
- `/youtube/user/@OpenAI` — OpenAI
- `/youtube/user/@anthropic-ai` — Anthropic
- `/youtube/user/@GoogleDeepMind` — Google DeepMind
- `/youtube/user/@NVIDIA` — NVIDIA
- `/youtube/user/@Linear` — Linear

**演讲与会议**
- `/youtube/user/@TED` — TED

---

## 2. AI 播客 (Podcasts)

直接订阅以下 5 个 AI 播客的 RSS feed，抓取最新单集的标题、描述和发布时间。

| 播客 | 主理人/机构 | RSS Feed URL |
|------|-------------|--------------|
| Latent Space | Swyx (AI Engineer 播客) | `https://www.latent.space/feed` |
| Training Data | Sequoia Capital (Sonya Huang, Pat Grady) | `https://feeds.megaphone.fm/trainingdata` |
| No Priors AI | AI 快速新闻 | `https://rss.art19.com/no-priors-ai` |
| Unsupervised Learning | Daniel Miessler (安全/AI/文化) | `https://www.omnycontent.com/d/playlist/070af456-729b-4a0f-9c09-a6c100397b59/3b159371-276d-429e-ae86-a6c1003b01c4/7b61d4e1-bd3d-4d3f-97c2-a6c1003b01c9/podcast.rss` |
| Data Driven NYC | Matt Turck / FirstMark | `https://feeds.soundcloud.com/users/soundcloud:users:206857405/sounds.rss` |

**抓取方式：**
```bash
curl -s --max-time 15 "{RSS_FEED_URL}"
```

解析 `<item>` 中的 `<title>`, `<description>` (或 `<itunes:summary>`), `<pubDate>`, `<link>` (或 `<enclosure>`)。

**播客摘要要求：** 每期播客需提供完整的中文摘要（3-5 个核心观点 bullet points），不能只写一句话。保留嘉宾姓名、身份背景和关键数据。

---

## 3. X (Twitter) KOL 追踪

通过 RSSHub 的 Twitter 路由抓取 22 位 AI 领域 KOL 的推文。

**RSSHub Twitter 路由：** `/twitter/user/{screen_name}`

> **前置条件：** RSSHub 实例需配置 Twitter API。如未配置会返回 `ConfigNotFoundError: Twitter API is not configured`，此时在日报中标注 "Twitter 板块接入中" 并列出 KOL 名单。

### KOL 列表（22 位）

| # | KOL | Twitter Handle | 身份 |
|---|-----|---------------|------|
| 1 | Andrej Karpathy | @karpathy | 前 OpenAI 核心成员，AI 大牛 |
| 2 | Swyx | @swyx | Latent Space 主理人，AI 开发者 |
| 3 | Josh Woodward | @josh_woodward | VP Google Labs & Gemini |
| 4 | Kevin Weil | @kevinweil | OpenAI CPO |
| 5 | Peter Yang | @petergyang | AI 产品人 |
| 6 | Madhu Guru | @madhu_guru | AI 从业者 |
| 7 | Amanda Askell | @amandaaskell | Anthropic Claude 性格设计负责人 |
| 8 | Google Labs | @GoogleLabs | 机构号 |
| 9 | Amjad Masad | @amasad | Replit 创始人 |
| 10 | Guillermo Rauch | @rauchg | Vercel 创始人 |
| 11 | Alex Albert | @alexalbert__ | Anthropic |
| 12 | Aaron Levie | @levie | Box 创始人 |
| 13 | Ryo Lu | @ryolu_ | AI 从业者 |
| 14 | Garry Tan | @garrytan | Y Combinator CEO |
| 15 | Matt Turck | @mattturck | FirstMark 投资人, Data Driven NYC |
| 16 | Zara Zhang | @zara_zhang | AI 领域 |
| 17 | Nikunj Kothari | @nikunjk | AI 从业者 |
| 18 | Peter Steinberger | @steipete | AI Agent 开发者 |
| 19 | Dan Shipper | @danshipper | Every 主编 |
| 20 | Aditya Agarwal | @adityaag | AI 从业者 |
| 21 | Sam Altman | @sama | OpenAI CEO |
| 22 | Claude | @AnthropicAI | Anthropic 机构号 |

**抓取方式：**
```bash
curl -s --max-time 15 "https://scarlettliu.zeabur.app/twitter/user/{screen_name}"
```

**推文摘要要求：** 推特内容通常较短，尽量保留原貌。只做必要的中文注释，不过度概括。

---

## Workflow

### Step 1: 并行抓取所有数据源

同时发起以下请求（使用并行 Bash 调用）：

**YouTube（12 个频道）：**
```bash
curl -s --max-time 15 "https://scarlettliu.zeabur.app{route}"
```

**播客（5 个 RSS feed）：**
```bash
curl -s --max-time 15 "{podcast_rss_url}"
```

**Twitter（25 个 KOL）：**
```bash
curl -s --max-time 15 "https://scarlettliu.zeabur.app/twitter/user/{handle}"
```

对所有响应解析 XML，提取 `<item>` 条目中的 `<title>`, `<link>`, `<pubDate>`, `<description>`。

### Step 2: 筛选与匹配

1. **时间过滤**：只保留最近 7 天内的内容
2. **KOL 直接匹配**：检查标题/描述是否包含 KOL 列表中的姓名或关键词
3. **AI 相关内容**：用关键词正则匹配 AI 相关内容（AI, GPT, LLM, Claude, Gemini, OpenAI, Anthropic, DeepMind, AGI, foundation model, transformer, generative, robotics, agent, inference, GPU, NVIDIA, ChatGPT, agentic, reasoning, startup, SaaS 等）
4. **重要性排序**：按日期倒序 + 重大事件置顶

### Step 3: 生成中文日报

**格式要求（严格遵守）：**

- **所有英文标题必须翻译为中文**
- **摘要信息量要丰富**：每条至少 2-3 句话，包含核心观点、关键数据、人物背景
- **播客摘要更详细**：3-5 个 bullet points 的核心观点提炼
- **推文尽量保留原貌**：因为推特本身就短，加必要的中文注释即可
- **最关键的信息和事件放在最上面**

**输出结构：**

```markdown
# AI Radar Daily Digest — {YYYY.MM.DD}（{星期}）

> AI 行业每日情报雷达 | 自动生成于 {date}
> 数据源：12 个 YouTube 频道 + 5 个 AI 播客 + 25 位推特 KOL

---

## 今日头条速览

> （3-5 条当日/近日最重大的事件，每条 1-2 句中文概述，用加粗标题）

---

## 播客深度摘要

（按播客分组，每期提供完整中文摘要）

### {播客名} — {主理人/机构}
**{单集中文标题}** — {日期}
[收听链接]({url})
（3-5 个核心观点 bullet points）

---

## YouTube 频道精选（近 7 天）

（按频道分组，每条含中文标题 + 2-3 句摘要）

### {频道名}
**{视频中文标题}** — {嘉宾/作者}, {日期}
[观看]({url})
{中文摘要}

---

## X (Twitter) KOL 动态

（按 KOL 分组，展示近期推文）

### {KOL Name} (@{handle}) — {身份}
- {推文内容，保留原貌} — {日期}
  {必要时加中文注释}

---

## 数据源状态

| 类型 | 源 | 状态 | 7天内容 |
|------|----|------|---------|
（列出所有数据源的抓取状态）

---

*Powered by AI Radar | 数据自动抓取 + AI 生成摘要*
```

### Step 4: 输出日报

**默认行为：** 将日报内容直接输出到对话中。

**如果用户要求保存到飞书：** 使用飞书 MCP 工具创建新文档，标题为 `AI Radar Daily Digest — {YYYY.MM.DD}`。如果内容过长，分段使用 `doc_append` 写入。写入完成后推送通知告知用户文档链接。

**如果用户要求保存为文件：** 写入 `~/ai-radar-reports/YYYY-MM-DD.md`。
