# 会话管理

> 管理多个独立的 AI 对话上下文

---

## 📖 什么是会话

### 会话的定义

**会话（Session）** 是 OpenClaw 中一次独立的对话过程。每次你启动 OpenClaw 并与 AI 进行对话，就创建了一个会话。

想象一下：
- 📱 **微信聊天** = 一个会话
- 💬 **每次新话题** = 可以开启新会话
- 📚 **不同项目** = 不同会话

### 为什么需要会话

| 场景 | 单会话问题 | 多会话优势 |
|------|-----------|-----------|
| **多个项目** | 上下文混乱 | 每个项目独立上下文 |
| **长期对话** | 超出长度限制 | 按主题拆分会话 |
| **隐私隔离** | 信息可能泄露 | 会话之间完全隔离 |
| **快速切换** | 需要重新解释 | 保留完整上下文 |

### 会话 vs 聊天历史

```
会话 (Session)          聊天历史 (Chat History)
├── 独立的对话上下文     ├── 当前会话内的消息记录
├── 可以创建/切换/删除   ├── 无法单独管理
├── 有唯一标识符         ├── 按时间顺序排列
└── 上下文相互隔离       └── 属于某个会话
```

**简单理解**：
- **会话** = 不同的聊天窗口
- **历史** = 每个窗口里的聊天记录

---

## ➕ 创建会话

### 创建新会话的命令

#### macOS / Linux

```bash
# 创建新会话（自动命名）
openclaw session new

# 创建并命名会话
openclaw session new --name "project-alpha"

# 创建会话并立即进入
openclaw session new --enter
```

#### Windows (PowerShell)

```powershell
# 创建新会话（自动命名）
openclaw session new

# 创建并命名会话
openclaw session new --name "project-alpha"

# 创建会话并立即进入
openclaw session new --enter
```

### 命名会话的最佳实践

```bash
# ✅ 好的命名
openclaw session new --name "work-project"
openclaw session new --name "learning-python"
openclaw session new --name "daily-chat"

# ❌ 避免的命名
openclaw session new --name "test"      # 太模糊
openclaw session new --name "123"       # 无意义
openclaw session new --name ""          # 空名称
```

### 双平台命令对照表

| 功能 | macOS / Linux | Windows |
|------|--------------|---------|
| 创建会话 | `openclaw session new` | `openclaw session new` |
| 命名会话 | `--name "名称"` | `--name "名称"` |
| 进入会话 | `--enter` | `--enter` |
| 快速创建 | `oc sn` | `oc sn` |

> 💡 **提示**：建议设置别名 `alias oc="openclaw"` 来简化命令

---

## 🔄 切换会话

### 查看会话列表

#### macOS / Linux

```bash
# 查看所有会话
openclaw session list

# 查看活跃会话
openclaw session list --active

# 查看最近使用的会话
openclaw session list --recent
```

#### Windows (PowerShell)

```powershell
# 查看所有会话
openclaw session list

# 查看活跃会话
openclaw session list --active

# 查看最近使用的会话
openclaw session list --recent
```

**输出示例**：
```
会话列表：
  ✅ work-project      (活跃)    最后使用：前
  📁 learning-python              最后使用：前
  💬 daily-chat                   最后使用：昨天
  📊 data-analysis                最后使用：3 天前
```

### 切换到指定会话

#### macOS / Linux

```bash
# 切换到已存在的会话
openclaw session switch "work-project"

# 简写命令
openclaw session use "work-project"

# 快速切换（设置别名后）
oc sw "work-project"
```

#### Windows (PowerShell)

```powershell
# 切换到已存在的会话
openclaw session switch "work-project"

# 简写命令
openclaw session use "work-project"

# 快速切换
oc sw "work-project"
```

### 快速切换技巧

#### 技巧 1：使用会话 ID

```bash
# 查看会话 ID
openclaw session list --verbose

# 通过 ID 切换（更精确）
openclaw session switch "sess_abc123"
```

#### 技巧 2：模糊匹配

```bash
# 支持部分匹配
openclaw session switch "work"    # 匹配 "work-project"
openclaw session switch "python"  # 匹配 "learning-python"
```

#### 技巧 3：快速返回上一个会话

```bash
# 返回上次使用的会话
openclaw session prev

# 或简写
oc sp
```

---

## 📜 查看历史记录

### 查看当前会话历史

#### macOS / Linux

```bash
# 查看当前会话的所有历史
openclaw history

# 查看最近 N 条历史
openclaw history --limit 10

# 带时间戳查看
openclaw history --timestamps
```

#### Windows (PowerShell)

```powershell
# 查看当前会话的所有历史
openclaw history

# 查看最近 N 条历史
openclaw history --limit 10

# 带时间戳查看
openclaw history --timestamps
```

**输出示例**：
```
[2026-03-05 10:30:15] 你：你好，帮我看看这个代码
[2026-03-05 10:30:18] AI：好的，让我看看...
[2026-03-05 10:31:05] 你：这个函数怎么优化？
[2026-03-05 10:31:10] AI：可以考虑以下几点...
```

### 搜索历史记录

```bash
# 搜索包含关键词的历史
openclaw history search "代码优化"

# 在指定会话中搜索
openclaw history search "bug" --session "work-project"

# 搜索最近 N 天的历史
openclaw history search "错误" --days 7
```

### 导出历史记录

#### macOS / Linux

```bash
# 导出当前会话历史到文件
openclaw history export > history.txt

# 导出为 JSON 格式
openclaw history export --format json > history.json

# 导出指定会话历史
openclaw history export --session "work-project" > work-history.txt
```

#### Windows (PowerShell)

```powershell
# 导出当前会话历史到文件
openclaw history export | Out-File -Encoding UTF8 history.txt

# 导出为 JSON 格式
openclaw history export --format json | Out-File -Encoding UTF8 history.json

# 导出指定会话历史
openclaw history export --session "work-project" | Out-File -Encoding UTF8 work-history.txt
```

---

## ⚠️ 上下文长度限制

### 什么是上下文窗口

**上下文窗口（Context Window）** 是 AI 模型一次能处理的文本长度限制。

```
┌─────────────────────────────────────────┐
│          上下文窗口 (8K tokens)          │
├─────────────────────────────────────────┤
│  系统提示词    │  对话历史   │  新消息   │
│   (500 tokens) │ (6000 tokens) │ (1500) │
└─────────────────────────────────────────┘
```

| 模型 | 上下文窗口 | 约等于文字 | 官网来源 |
|------|-----------|-----------|----------|
| **qwen3.5-plus** | 1M tokens | ~800,000 汉字 | [阿里云百炼](https://help.aliyun.com/zh/model-studio/model-pricing) |
| **GPT-5.4** | 1.05M tokens (922K+128K) | ~800,000 汉字 | [OpenRouter](https://openrouter.ai/openai) |
| **Claude Opus 4.6** | 1M tokens | ~800,000 汉字 | [Anthropic](https://www.anthropic.com/claude/opus) |
| **Claude Sonnet 4.6** | 1M tokens | ~800,000 汉字 | [Anthropic](https://www.anthropic.com/claude/opus) |
| **Gemini 3.1 Pro** | 1M tokens | ~800,000 汉字 | [Google AI](https://ai.google.dev/gemini-api/docs/pricing) |
| **kimi-k2.5** | 256K tokens | ~200,000 汉字 | [Moonshot](https://platform.moonshot.ai/docs/pricing/chat) |
| **glm-5** | 202.8K tokens | ~150,000 汉字 | [Z.ai](https://docs.z.ai/guides/overview/pricing) |
| **MiniMax-M2.5** | 196.6K tokens | ~150,000 汉字 | [MiniMax](https://platform.minimax.io/docs/guides/pricing-paygo) |

### 超出限制会怎样

当对话历史超出上下文窗口时：

1. **自动截断** - 最早的对话会被丢弃
2. **可能遗忘** - AI 可能忘记之前的约定
3. **性能下降** - 响应可能变慢

**警告信号**：
```
⚠️  警告：上下文长度已达 85%
💡  建议：开启新会话或清理历史
```

### 如何管理上下文长度

#### 方法 1：定期开启新会话

```bash
# 每 20-30 轮对话创建新会话
openclaw session new --name "project-phase-2"
```

#### 方法 2：清理当前会话历史

```bash
# 清理最近的 N 条消息
openclaw history trim --keep 20

# 清理所有历史（保留会话）
openclaw history clear --confirm
```

#### 方法 3：使用摘要功能

```bash
# 生成当前会话摘要
openclaw session summarize

# 基于摘要开启新会话
openclaw session new --context "summary.txt"
```

---

## 🧹 会话清理

### 删除单个会话

#### macOS / Linux

```bash
# 删除指定会话
openclaw session delete "old-project"

# 强制删除（不确认）
openclaw session delete "old-project" --force

# 删除并导出历史
openclaw session delete "old-project" --export
```

#### Windows (PowerShell)

```powershell
# 删除指定会话
openclaw session delete "old-project"

# 强制删除（不确认）
openclaw session delete "old-project" --force

# 删除并导出历史
openclaw session delete "old-project" --export
```

> ⚠️ **警告**：删除后会话无法恢复，建议先导出历史！

### 清理所有会话

```bash
# 清理所有非活跃会话
openclaw session cleanup

# 清理超过 N 天未使用的会话
openclaw session cleanup --older-than 30

# 保留最近 N 个会话，清理其余
openclaw session cleanup --keep-recent 5
```

### 自动清理配置

在配置文件中设置自动清理：

#### macOS / Linux

```bash
# 编辑配置文件
nano ~/.openclaw/config.json

# 添加自动清理配置
{
  "session": {
    "auto_cleanup": true,
    "cleanup_days": 30,
    "keep_recent": 10
  }
}
```

#### Windows

```powershell
# 编辑配置文件
notepad $env:USERPROFILE\.openclaw\config.json

# 添加相同的配置
```

---

## 📝 实践示例

### 示例 1：创建和切换会话

```bash
# 步骤 1：创建三个会话
openclaw session new --name "work"
openclaw session new --name "study"
openclaw session new --name "chat"

# 步骤 2：查看会话列表
openclaw session list

# 步骤 3：切换到 work 会话
openclaw session switch "work"

# 步骤 4：验证当前会话
openclaw session info

# 步骤 5：返回上一个会话
openclaw session prev
```

### 示例 2：管理多个项目

```bash
# 场景：同时处理两个项目

# 项目 A：网站开发
openclaw session new --name "website-dev"
# ... 进行网站开发对话 ...
openclaw history export > website-notes.txt

# 切换到项目 B：数据分析
openclaw session switch "data-analysis"
# 或
openclaw session new --name "data-analysis"

# ... 进行数据分析对话 ...

# 快速切换回项目 A
openclaw session switch "website-dev"
```

### 示例 3：清理旧会话

```bash
# 步骤 1：查看所有会话
openclaw session list

# 步骤 2：导出重要会话历史
openclaw history export --session "old-project" > backup.txt

# 步骤 3：删除不再需要的会话
openclaw session delete "test-session"

# 步骤 4：运行自动清理
openclaw session cleanup --older-than 7

# 步骤 5：确认清理结果
openclaw session list
```

---

## ❓ 常见问题

### Q1: 会话丢失怎么办？

**可能原因**：
- 会话被意外删除
- 配置文件损坏
- 切换了用户账户

**解决方案**：
```bash
# 1. 检查会话目录
ls -la ~/.openclaw/sessions/

# 2. 查看备份（如果有）
ls -la ~/.openclaw/backups/

# 3. 从导出文件恢复
openclaw session restore --from "backup.txt"

# 4. 联系支持
openclaw support --issue "session-lost"
```

**预防措施**：
- 定期导出重要会话历史
- 使用版本控制管理配置文件
- 不要手动删除会话文件

### Q2: 如何备份会话？

#### macOS / Linux

```bash
# 备份所有会话
cp -r ~/.openclaw/sessions/ ~/backups/sessions-$(date +%Y%m%d)/

# 备份单个会话
openclaw history export --session "important" > ~/backups/important-session.txt

# 使用脚本自动备份
cat > backup-sessions.sh << EOF
#!/bin/bash
BACKUP_DIR=~/backups/sessions-\$(date +%Y%m%d)
mkdir -p \$BACKUP_DIR
cp -r ~/.openclaw/sessions/ \$BACKUP_DIR/
echo "备份完成：\$BACKUP_DIR"
EOF
chmod +x backup-sessions.sh
./backup-sessions.sh
```

#### Windows (PowerShell)

```powershell
# 备份所有会话
Copy-Item -Path "$env:USERPROFILE\.openclaw\sessions" -Destination "$env:USERPROFILE\backups\sessions-$(Get-Date -Format 'yyyyMMdd')" -Recurse

# 备份单个会话
openclaw history export --session "important" | Out-File -Encoding UTF8 "$env:USERPROFILE\backups\important-session.txt"
```

### Q3: 会话有数量限制吗？

**答案**：理论上没有限制，但建议管理。

| 会话数量 | 影响 | 建议 |
|---------|------|------|
| < 10 | 无影响 | ✅ 健康 |
| 10-50 | 轻微影响 | ⚠️ 定期清理 |
| 50-100 | 列表变慢 | ⚠️ 需要整理 |
| > 100 | 性能下降 | ❌ 立即清理 |

**最佳实践**：
- 保持活跃会话 < 10 个
- 总会话数 < 50 个
- 每月清理一次旧会话

---

## ✅ 本节要点

**你学到了**：

- ✅ 什么是会话及其重要性
- ✅ 创建和命名会话的方法
- ✅ 在会话之间切换的技巧
- ✅ 查看和管理历史记录
- ✅ 理解上下文长度限制
- ✅ 清理和维护会话
- ✅ 备份和恢复会话

**关键命令速查**：

```bash
# 会话管理
oc session new --name "名称"    # 创建会话
oc session list                 # 查看列表
oc session switch "名称"        # 切换会话
oc session delete "名称"        # 删除会话

# 历史管理
oc history                      # 查看历史
oc history export               # 导出历史
oc history search "关键词"      # 搜索历史
```

---

## ➡️ 下一节

[渠道配置](./05-channel-setup.md) - 配置 Discord、飞书、钉钉等消息渠道

---

## 📎 附录：完整命令参考

### 会话命令

| 命令 | 功能 | 示例 |
|------|------|------|
| `session new` | 创建新会话 | `oc session new --name "work"` |
| `session list` | 列出会话 | `oc session list --recent` |
| `session switch` | 切换会话 | `oc session switch "work"` |
| `session delete` | 删除会话 | `oc session delete "old"` |
| `session info` | 查看信息 | `oc session info` |
| `session prev` | 返回上一个 | `oc session prev` |

### 历史命令

| 命令 | 功能 | 示例 |
|------|------|------|
| `history` | 查看历史 | `oc history --limit 10` |
| `history search` | 搜索历史 | `oc history search "bug"` |
| `history export` | 导出历史 | `oc history export > file.txt` |
| `history trim` | 修剪历史 | `oc history trim --keep 20` |
| `history clear` | 清空历史 | `oc history clear --confirm` |
