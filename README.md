# AI Radar - Claude Code Skill

Hi, 我是Scarlett 👋

我是一个对 AI 行业充满好奇心的产品人。每天早上打开电脑，我都面临着同一个问题：昨晚 AI 世界又发生了什么？

Sam Altman 又发了什么推？Karpathy 在聊什么新想法？Sequoia 的播客又请了谁？a16z 在关注什么新趋势？这些信息散落在 YouTube、Twitter、播客等十几个平台上，光是手动刷一遍，就要花掉将近一个小时。

所以我做了 AI Radar。

Why AI Radar?
这个工具的设计理念很简单：让 AI 帮你追踪 AI。

我不想再做一个需要注册、需要付费、甚至需要打开另一个 App 的信息产品。AI Radar 只是一个纯净的 Markdown 文件——你只需把它放进 Claude Code 的 commands 目录，输入 /ai-radar，等待两分钟，一份覆盖 12 个 YouTube 频道、5 个顶级 AI 播客、22 位行业 KOL 推文的中文日报就生成了。

极简且免费：没有后端，没有数据库，没有订阅费。

完全透明：RSSHub 实例是自己的，数据流向百分之百透明。

高度定制：你可以自由增减 KOL、替换播客源、调整输出格式——因为它就是一个你能完全看懂并随时修改的纯文本。

我相信，最好的工具是那些你拥有它，而不是它拥有你的工具。

最后
如果这个小东西每天能帮你省下哪怕 10 分钟的信息筛选时间，我就会很开心。

我们正处在一个不可思议的时代——AI 每天都在创造新的可能性。而我们能做的最好的事情，就是保持关注、保持学习、保持建造。

Happy building 🚀

— ScarlettLiu（刘静）2026.04.22

正文介绍：

AI 行业每日情报雷达。一个 [Claude Code](https://claude.ai/claude-code) 的 Slash Command，自动抓取 AI 领域 KOL 的最新访谈、演讲、推文和播客动态，生成中文日报。

## 数据源

| 类型 | 数量 | 来源 |
|------|------|------|
| YouTube 频道 | 12 个 | OpenAI, Anthropic, DeepMind, NVIDIA, TED, a16z, 20VC, Lex Fridman 等 |
| AI 播客 | 5 个 | Latent Space, Training Data (Sequoia), No Priors, Unsupervised Learning, Data Driven NYC |
| X/Twitter KOL | 22 位 | Karpathy, Sam Altman, Swyx, Aaron Levie, Garry Tan, Amanda Askell 等 |

## 安装

1. 将 `ai-radar.md` 复制到你的 Claude Code commands 目录：

```bash
# macOS / Linux
cp ai-radar.md ~/.claude/commands/ai-radar.md

# Windows
copy ai-radar.md %USERPROFILE%\.claude\commands\ai-radar.md
```

2. 在 Claude Code 中使用 `/ai-radar` 即可生成日报。

## 前置条件

本 skill 依赖一个 [RSSHub](https://github.com/DIYgod/RSSHub) 实例来抓取数据。

1. **部署 RSSHub**：参考 [RSSHub 部署文档](https://docs.rsshub.app/deploy/)，推荐使用 Zeabur / Vercel / Docker
2. **修改 skill 文件**：将 `ai-radar.md` 中的 RSSHub base URL (`https://scarlettliu.zeabur.app`) 替换为你自己的实例地址

### Twitter/X 数据源（可选）

需要在 RSSHub 实例中配置 Twitter 认证。推荐使用浏览器 Cookie 方式：

1. 在浏览器中登录 [x.com](https://x.com)
2. F12 → Application → Cookies → `https://x.com` → 复制 `auth_token` 值
3. 在 RSSHub 实例中设置环境变量：`TWITTER_AUTH_TOKEN=你的值`

也支持 Twitter API v1.1（需要 4 个环境变量，详见 skill 文件）。

## 输出示例

日报包含以下板块：

- **今日头条速览** — 当日最重大的 3-5 条 AI 事件
- **播客深度摘要** — 每期播客的核心观点提炼（中文）
- **YouTube 频道精选** — 近 7 天 AI 相关视频，含中文标题和摘要
- **Twitter KOL 动态** — 22 位 AI 领域 KOL 的最新推文

支持输出到终端、飞书文档或本地 Markdown 文件。

## 自定义

你可以在 `ai-radar.md` 中：
- 添加/删除 YouTube 频道、播客源或 Twitter KOL
- 修改 RSSHub 实例地址
- 调整输出格式和语言

## License

MIT
