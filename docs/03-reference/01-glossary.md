# 名词解释附录 - 小白扫盲指南

> 傻傻分不清楚？看这一篇就够了！

---

## 🤔 为什么需要这一章？

AI 领域有太多相似的名词，小白很容易懵逼：

- 😵 "OpenClaw 和 Nanobot 有什么区别？"
- 😵 "CLI-Anything 是什么鬼？"
- 😵 "Cursor 和 Claude Code 是一回事吗？"
- 😵 "MCP、Agent、Skill 都是啥？"

**这一章帮你彻底搞懂！**

---

## 📋 名词分类总览

我们将这些名词分为 **5 大类**：

| 类别 | 说明 | 包含名词 |
|------|------|---------|
| 🤖 **AI 助手框架** | 运行 AI 助手的平台/框架 | OpenClaw、Nanobot、ClawHub |
| 🛠️ **AI 工具/协议** | AI 与外部交互的标准/工具 | MCP、Skill、CLI-Anything |
| 💻 **AI 编辑器/IDE** | 集成 AI 的代码编辑器 | Cursor、Claude Code、Windsurf |
| 🏢 **公司/组织** | 开发这些技术的公司或组织 | OpenClaw 团队、HKUDS、Anthropic |
| 🌐 **云服务/平台** | 提供 AI 能力的云平台 | 阿里云百炼、OpenRouter、DashScope |

---

## 🤖 第一类：AI 助手框架

这些是**运行 AI 助手的平台**，让你能在 Discord、飞书、微信等地方和 AI 聊天。

### OpenClaw 🐾

| 项目 | 说明 |
|------|------|
| **是什么** | AI 助手框架（TypeScript 编写） |
| **代码量** | 430,000+ 行 |
| **特点** | 功能全面、生产级、企业级 |
| **适合** | 需要完整功能、稳定性要求高 |
| **缺点** | 太重、太复杂、资源占用大 |
| **官网** | https://openclaw.ai |
| **GitHub** | https://github.com/openclaw/openclaw |

**一句话**：功能强大的重型框架，像"航空母舰"

---

### Nanobot 🤖

| 项目 | 说明 |
|------|------|
| **是什么** | AI 助手框架（Python 编写） |
| **代码量** | ~4,000 行（比 OpenClaw 小 100 倍） |
| **特点** | 轻量级、简洁、易定制 |
| **适合** | 学习研究、资源受限环境、快速原型 |
| **缺点** | 较新（2026-02 发布）、功能较少 |
| **开发者** | 香港大学数据科学实验室（HKUDS） |
| **GitHub** | https://github.com/HKUDS/nanobot |

**一句话**：OpenClaw 的极简替代品，像"轻便摩托车"

---

### ClawHub 📦

| 项目 | 说明 |
|------|------|
| **是什么** | OpenClaw 的技能商店/市场 |
| **功能** | 发布、安装、更新 OpenClaw 技能 |
| **类比** | 像"App Store"或"npm 仓库" |
| **官网** | https://clawhub.com |

**一句话**：OpenClaw 的技能应用商店

---

### OpenCode 💻

| 项目 | 说明 |
|------|------|
| **是什么** | 开源终端 AI 编程助手（类似 Claude Code） |
| **代码量** | 120K+ GitHub stars |
| **特点** | 终端原生、免费开源、支持多种 LLM |
| **适合** | 程序员、开发者、需要 AI 辅助编程 |
| **官网** | https://opencode.ai |
| **GitHub** | https://github.com/opencode-ai/opencode |

**一句话**：开源版的"Claude Code"，终端编程神器

**注意**：OpenCode 和 OpenClaw 是**两个不同的项目**！
- OpenCode = 编程助手（写代码用）
- OpenClaw = AI 助手框架（聊天机器人用）

---

### 其他类似项目

| 名称 | 说明 | 状态 |
|------|------|------|
| **ClawLike** | 类似 OpenClaw 的框架（社区项目） | 小众 |
| **OpenCode** | OpenClaw 的中文名/别名 | 同个东西 |

---

## 🛠️ 第二类：AI 工具/协议

这些是**AI 与外部世界交互的工具和标准**。

### MCP (Model Context Protocol) 🔌

| 项目 | 说明 |
|------|------|
| **是什么** | AI 模型与外部工具通信的协议标准 |
| **类比** | 像"USB 接口"，让 AI 能连接各种工具 |
| **作用** | 标准化 AI 与数据库、API、文件系统的交互 |
| **开发者** | Anthropic（Claude 的开发者） |
| **官网** | https://modelcontextprotocol.io |

**一句话**：AI 界的"USB 接口"，让 AI 能插各种设备

---

### Skill (技能) 🎯

| 项目 | 说明 |
|------|------|
| **是什么** | AI 助手的功能模块/插件 |
| **类比** | 像"手机 APP"或"浏览器扩展" |
| **作用** | 扩展 AI 能力（搜索、文件操作、API 调用等） |
| **OpenClaw** | 通过 ClawHub 安装 |
| **Nanobot** | 通过 skills/ 目录加载 |

**一句话**：AI 的"超能力包"，让 AI 会更多技能

---

### CLI-Anything 🔧

| 项目 | 说明 |
|------|------|
| **是什么** | 自动生成命令行工具的项目 |
| **功能** | 将 GUI 软件转换为 AI 可控制的 CLI |
| **开发者** | 香港大学数据科学实验室（HKUDS） |
| **口号** | "让所有软件都能被 AI 控制" |
| **GitHub** | https://github.com/HKUDS/CLI-Anything |
| **限制** | ⚠️ 需要软件源码，仅支持开源桌面软件 |

**一句话**：给软件自动生成"遥控器"，让 AI 能控制

**注意**：项目非常新（2026-03-08 发布），营销成分较重，建议观望。

---

### 其他工具

| 名称 | 说明 |
|------|------|
| **Jina Reader** | 网页内容抓取工具（https://r.jina.ai/URL） |
| **Tavily Search** | AI 优化的搜索引擎（需要 API key） |
| **web_fetch** | OpenClaw 内置的网页抓取工具 |

---

## 💻 第三类：AI 编辑器/IDE

这些是**集成 AI 功能的代码编辑器**，程序员用的。

### Cursor 💙

| 项目 | 说明 |
|------|------|
| **是什么** | 集成 AI 的代码编辑器（基于 VS Code） |
| **特点** | AI 辅助编程、代码生成、智能补全 |
| **适合** | 程序员、开发者 |
| **官网** | https://cursor.com |
| **价格** | 免费版 + 付费版（$20/月） |

**一句话**：AI 版的 VS Code，程序员神器

---

### Claude Code 🟠

| 项目 | 说明 |
|------|------|
| **是什么** | Anthropic 的 AI 编程助手（命令行工具） |
| **功能** | 在终端用自然语言让 AI 写代码 |
| **适合** | 开发者、命令行用户 |
| **开发者** | Anthropic（Claude 的开发者） |
| **官网** | https://claude.ai/code |

**一句话**：在终端里用 Claude 写代码

---

### Windsurf 🌊

| 项目 | 说明 |
|------|------|
| **是什么** | 集成 AI 的代码编辑器（Codeium 出品） |
| **特点** | 深度 AI 集成、代码理解能力强 |
| **适合** | 程序员、开发者 |
| **官网** | https://codeium.com/windsurf |

**一句话**：另一个 AI 编辑器，和 Cursor 类似

---

### 其他编辑器

| 名称 | 说明 |
|------|------|
| **GitHub Copilot** | GitHub 的 AI 编程助手（VS Code 插件） |
| **Tabnine** | AI 代码补全工具 |
| **Replit AI** | 在线 IDE 的 AI 功能 |
| **Zed AI** | Zed 编辑器的 AI 集成 |

---

## 🏢 第四类：公司/组织

### HKUDS (香港大学数据科学实验室) 🎓

| 项目 | 说明 |
|------|------|
| **是什么** | 香港大学数据科学研究所 |
| **开发项目** | Nanobot、CLI-Anything |
| **特点** | 开源、学术背景、创新项目多 |
| **GitHub** | https://github.com/HKUDS |

**一句话**：开源项目大户，Nanobot 和 CLI-Anything 的开发者

---

### Anthropic 🟠

| 项目 | 说明 |
|------|------|
| **是什么** | AI 公司（OpenAI 前员工创立） |
| **产品** | Claude 系列 AI 模型 |
| **特点** | 注重 AI 安全、对齐 |
| **官网** | https://anthropic.com |

**一句话**：Claude 的开发者，AI 安全派代表

---

### OpenAI 🔵

| 项目 | 说明 |
|------|------|
| **是什么** | AI 公司（ChatGPT 的开发者） |
| **产品** | GPT 系列、ChatGPT、Codex |
| **官网** | https://openai.com |

**一句话**：ChatGPT 的开发者，AI 界老大哥

---

### 其他公司

| 名称 | 说明 |
|------|------|
| **阿里云百炼** | 阿里云的 AI 模型平台（国内直连） |
| **智谱 AI** | 清华系的 AI 公司（GLM 模型） |
| **Moonshot** | 月之暗面（Kimi 的开发者） |
| **Google DeepMind** | Google 的 AI 部门（Gemini 模型） |
| **Microsoft** | 投资 OpenAI，开发 Copilot |

---

## 🌐 第五类：云服务/平台

### 阿里云百炼 (DashScope) ☁️

| 项目 | 说明 |
|------|------|
| **是什么** | 阿里云的 AI 模型服务平台 |
| **提供模型** | Qwen（通义千问）、MiniMax、Kimi、GLM 等 |
| **特点** | 国内直连、无需外网、价格便宜 |
| **官网** | https://dashscope.console.aliyun.com/ |
| **价格** | 约 ¥0.8-4/百万 tokens（输入） |

**一句话**：国内 AI 模型聚合平台，不用翻墙

---

### OpenRouter 🚪

| 项目 | 说明 |
|------|------|
| **是什么** | AI 模型聚合平台（国际） |
| **提供模型** | GPT、Claude、Gemini 等几乎所有主流模型 |
| **特点** | 一个 API 访问所有模型、按量付费 |
| **官网** | https://openrouter.ai |
| **价格** | 约 $2.5-15/百万 tokens（输入） |

**一句话**：AI 模型"大卖场"，一个账号用所有模型

---

### 其他平台

| 名称 | 说明 |
|------|------|
| **OpenAI API** | OpenAI 的官方 API（GPT 系列） |
| **Anthropic API** | Anthropic 的官方 API（Claude 系列） |
| **Google AI** | Google 的 AI 平台（Gemini 系列） |
| **智谱 AI** | 智谱的 API 平台（GLM 系列） |
| **Moonshot API** | 月之暗面的 API（Kimi） |

---

## 🔍 快速对比表

### AI 助手框架对比

| 特性 | OpenClaw | Nanobot |
|------|----------|---------|
| **代码量** | 430k+ 行 | ~4k 行 |
| **语言** | TypeScript | Python |
| **内存** | >1GB | <5MB |
| **启动** | 较慢 | <10ms |
| **定位** | 生产级 | 学习/研究 |
| **适合** | 企业用户 | 开发者/学习者 |

---

### AI 编辑器对比

| 特性 | Cursor | Claude Code | Windsurf |
|------|--------|-------------|----------|
| **类型** | 编辑器 | 命令行工具 | 编辑器 |
| **基础** | VS Code | 终端 | 自研 |
| **AI** | 多模型 | 仅 Claude | Codeium |
| **价格** | $20/月 | 需 Claude 订阅 | 免费 |
| **适合** | 程序员 | 命令行用户 | 程序员 |

---

### AI 模型平台对比（国内）

| 平台 | 模型 | 价格 | 外网 |
|------|------|------|------|
| **阿里云百炼** | Qwen/MiniMax/Kimi | ¥0.8-4/百万 | ❌ 不需要 |
| **智谱 AI** | GLM 系列 | ¥4-8/百万 | ❌ 不需要 |
| **Moonshot** | Kimi | ¥4-21/百万 | ❌ 不需要 |

---

### AI 模型平台对比（国际）

| 平台 | 模型 | 价格 | 外网 |
|------|------|------|------|
| **OpenRouter** | GPT/Claude/Gemini | $2.5-15/百万 | ✅ 需要 |
| **OpenAI API** | GPT 系列 | $2.5-15/百万 | ✅ 需要 |
| **Anthropic API** | Claude 系列 | $5-25/百万 | ✅ 需要 |

---

## 🎯 小白选购指南

### 场景 1：我想在 Discord/飞书和 AI 聊天

**推荐**：
- 追求稳定 → **OpenClaw**
- 想学习/折腾 → **Nanobot**

**不需要**：Cursor、Claude Code（这些是编程用的）

---

### 场景 2：我想让 AI 帮我写代码

**推荐**：
- 图形界面 → **Cursor** 或 **Windsurf**
- 命令行 → **Claude Code**
- 免费替代 → **GitHub Copilot**（免费版）

**不需要**：OpenClaw、Nanobot（这些是聊天机器人框架）

---

### 场景 3：我想让 AI 控制我的软件

**推荐**：
- 有源码的开源软件 → **CLI-Anything**（观望中）
- 有 API 的软件 → 自己写 MCP Server
- 普通用户 → 等成熟方案

**注意**：CLI-Anything 还很新，建议观望

---

### 场景 4：我想用 AI 模型但不知道选哪个平台

**国内用户**：
- 性价比 → **阿里云百炼**（模型多、便宜、不用翻墙）
- Kimi 粉丝 → **Moonshot API**
- GLM 粉丝 → **智谱 AI**

**国际用户**：
- 模型最全 → **OpenRouter**
- 只用 GPT → **OpenAI API**
- 只用 Claude → **Anthropic API**

---

## 📝 常见误区

### ❌ 误区 1："Nanobot 是纳米机器人吗？"
**正解**：有两个含义：
- 🤖 **AI 框架**：HKUDS 开发的 AI 助手框架（本文讨论的）
- 🔬 **纳米机器人**：医学/材料学领域的纳米级机器人

**同名不同物！**

---

### ❌ 误区 2："MCP 是一种 AI 模型吗？"
**正解**：不是！MCP 是**通信协议**，像 USB 接口，不是 AI 模型本身。

---

### ❌ 误区 3："CLI-Anything 能让所有软件被 AI 控制吗？"
**正解**：不能！目前只能处理：
- ✅ 有源码的开源桌面软件
- ❌ 闭源商业软件（Adobe、Office 等）
- ❌ Web 应用
- ❌ 移动应用

**宣传有夸大成分！**

---

## 🎓 知识树总结

```
AI 助手生态
├── 🤖 AI 助手框架
│   ├── OpenClaw（重型、生产级）
│   ├── Nanobot（轻量、学习用）
│   └── ClawHub（技能商店）
│
├── 🛠️ AI 工具/协议
│   ├── MCP（通信协议）
│   ├── Skill（功能插件）
│   └── CLI-Anything（CLI 生成器）
│
├── 💻 AI 编辑器
│   ├── Cursor（VS Code 系）
│   ├── Claude Code（命令行）
│   └── Windsurf（Codeium 系）
│
├── 🏢 公司/组织
│   ├── HKUDS（开源大户）
│   ├── Anthropic（Claude）
│   └── OpenAI（GPT）
│
└── 🌐 云平台
    ├── 阿里云百炼（国内）
    ├── OpenRouter（国际）
    └── 各厂商官方 API
```

---

## 📞 还有疑问？

如果还有名词不理解：

1. **查官方文档**：最准确
2. **问 AI 助手**：让它用大白话解释
3. **搜索 GitHub**：看项目 README
4. **加入社区**：Discord、飞书群等

---

*最后更新：2026-03-10*
