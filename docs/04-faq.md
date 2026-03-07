# 综合常见问题

## 欢迎！👋

欢迎阅读 OpenClaw 常见问题解答！

本文档汇总了用户在使用 OpenClaw 过程中最常见的问题和解答。如果您在使用过程中遇到问题，可以先在这里查找答案。

---

## 基础问题

### Q1: OpenClaw 是什么？

OpenClaw 是一个运行在您本地环境中的 AI 助手框架。它允许您通过命令行、Discord、飞书等多种渠道与 AI 进行交互，并支持通过技能系统扩展功能。

### Q2: OpenClaw 和网页版 AI 有什么区别？

- **网页版 AI**：只能通过浏览器访问，功能受限于网页界面
- **OpenClaw**：运行在本地，可以访问您的文件系统、执行命令、集成各种工具，功能更强大

### Q3: 我需要编程基础吗？

不需要。OpenClaw 设计为零基础用户可用，所有操作都有详细说明。当然，如果您有编程基础，可以更深入地定制和扩展功能。

---

## 安装问题

### Q4: 安装失败怎么办？

**macOS 用户**：
- 确保已安装 Homebrew：`brew --version`
- 检查网络连接
- 查看详细错误信息

**Windows 用户**：
- 确保已安装 Winget：`winget --version`
- 以管理员身份运行 PowerShell
- 查看详细错误信息

### Q5: API Key 如何配置？

1. 获取 API Key（从 OpenAI、Anthropic 等服务商）
2. 编辑配置文件（位置见 [配置文件位置](./03-reference/config-locations.md)）
3. 重启 OpenClaw

详细步骤请参考 [API 配置指南](./03-reference/api-setup.md)。

---

## 使用问题

### Q6: 如何管理多个会话？

使用会话管理命令：
- 创建新会话：`/session new <名称>`
- 切换会话：`/session switch <名称>`
- 列出会话：`/session list`
- 删除会话：`/session delete <名称>`

详细说明请参考 [会话管理](./02-openclaw-guide/04-session-management.md)。

### Q7: 如何配置 Discord/飞书？

**Discord**：
1. 创建 Discord 机器人
2. 获取 Bot Token
3. 配置到 OpenClaw

**飞书**：
1. 创建飞书机器人
2. 获取 App ID 和 Secret
3. 配置到 OpenClaw

详细说明请参考 [渠道配置](./02-openclaw-guide/05-channel-setup.md)。

### Q8: 技能是什么？如何使用？

技能是 OpenClaw 的扩展功能模块，可以让 AI 执行特定任务（如搜索网页、操作飞书文档等）。

使用方法：
1. 加载技能：`/skill load <技能名>`
2. 使用技能：在对话中自然提及技能功能

详细说明请参考 [技能系统](./02-openclaw-guide/06-skill-system.md)。

---

## 技术问题

### Q9: AI 回答不准确怎么办？

AI 可能会"胡说"（幻觉），这是大模型的固有特性。建议：
- 提供清晰的上下文
- 要求 AI 提供来源
- 对重要信息进行验证

详细说明请参考 [AI 为什么会胡说](./01-ai-intro/03-ai-hallucination.md)。

### Q10: 命令执行失败怎么办？

1. 检查命令语法
2. 检查权限
3. 查看详细错误信息
4. 参考 [问题排查指南](./03-reference/troubleshooting.md)

### Q11: 如何查看日志？

日志位置：
- **macOS**: `~/.openclaw/logs/`
- **Windows**: `%USERPROFILE%\.openclaw\logs\`

---

## 资源汇总

### 文档链接

| 资源 | 说明 |
|------|------|
| [OpenClaw 官方文档](https://openclaw.com/docs) | 完整的 API 参考和指南 |
| [AI 入门](./01-ai-intro/) | AI 基础概念介绍 |
| [OpenClaw 指南](./02-openclaw-guide/) | OpenClaw 使用指南 |
| [参考手册](./03-reference/) | 命令、配置、API 参考 |
| [常见问题 FAQ](./03-reference/faq.md) | 常见问题解答 |

### 社区链接

| 平台 | 用途 |
|------|------|
| Discord 社区 | 实时讨论和问题求助 |
| GitHub 仓库 | 代码贡献和问题追踪 |
| 开发者论坛 | 深度技术讨论 |
| 技能市场 | 发现和分享技能 |

### 官方资源

- **GitHub**: `github.com/openclaw/openclaw`
- **文档**: `openclaw.com/docs`
- **技能市场**: `clawhub.com`
- **官方博客**: `blog.openclaw.com`

---

## 需要更多帮助？

如果本文档没有解答您的问题，可以：

1. 查看 [问题排查指南](./03-reference/troubleshooting.md)
2. 在 GitHub 提交 Issue
3. 加入 Discord 社区求助
4. 联系官方支持

---

*最后更新：2026 年 3 月*
