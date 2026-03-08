# 常见问题 FAQ

本文档汇集了 OpenClaw 使用过程中最常见的问题和解决方案。如果你遇到问题，请先在这里查找。

---

## 安装相关

### Q: 安装失败怎么办？

**A:** 安装失败通常有以下几种原因：

1. **网络问题**
   - 检查网络连接是否正常
   - 如果使用 npm 安装，尝试切换镜像源：
     ```bash
     npm config set registry https://registry.npmmirror.com
     ```
   - 对于 Git 克隆失败，检查是否能访问 GitHub

2. **权限问题**
   - 确保有足够的文件系统权限
   - 在 Linux/Mac 上，可能需要使用 `sudo` 或调整目录权限
   - 在 Windows 上，以管理员身份运行终端

3. **Node.js 版本不兼容**
   - OpenClaw 需要 Node.js v18 或更高版本
   - 检查版本：`node --version`
   - 升级 Node.js：推荐使用 nvm (Node Version Manager)

4. **依赖冲突**
   - 删除 `node_modules` 文件夹和 `package-lock.json`
   - 重新运行 `npm install`

5. **磁盘空间不足**
   - 检查磁盘空间：`df -h`
   - 清理不必要的文件后重试

如果以上方法都无效，请查看安装日志中的具体错误信息，或在 GitHub Issues 中搜索类似问题。

---

### Q: 命令找不到怎么办？

**A:** "command not found" 错误通常是因为 OpenClaw 没有正确添加到系统 PATH 中。

**解决方案：**

1. **确认安装位置**
   ```bash
   # 查找 openclaw 可执行文件
   find ~ -name "openclaw" -type f 2>/dev/null
   ```

2. **添加到 PATH**
   
   Linux/Mac (添加到 `~/.bashrc` 或 `~/.zshrc`):
   ```bash
   export PATH="$HOME/.openclaw/bin:$PATH"
   source ~/.bashrc  # 或 source ~/.zshrc
   ```
   
   Windows (PowerShell):
   ```powershell
   $env:Path += ";C:\Users\你的用户名\.openclaw\bin"
   ```

3. **使用完整路径运行**
   ```bash
   ~/.openclaw/bin/openclaw --help
   ```

4. **重新安装**
   ```bash
   npm install -g openclaw
   ```

5. **验证安装**
   ```bash
   openclaw --version
   openclaw help
   ```

如果仍然找不到命令，检查 npm 的全局安装目录是否在 PATH 中：
```bash
npm config get prefix
```

---

## 配置相关

### Q: API Key 在哪里获取？

**A:** OpenClaw 支持多种 AI 模型，不同模型的 API Key 获取方式不同：

**1. 通义千问 (阿里云百炼)**
- 访问：https://bailian.console.aliyun.com/
- 登录阿里云账号
- 进入「API-KEY 管理」
- 创建新的 API Key
- 复制并保存（只显示一次）

**2. OpenAI**
- 访问：https://platform.openai.com/api-keys
- 登录 OpenAI 账号
- 点击「Create new secret key」
- 复制并保存

**3. DeepSeek**
- 访问：https://platform.deepseek.com/
- 登录后进入 API 管理页面
- 创建 API Key

**4. 其他模型**
- 参考对应平台的官方文档
- 通常在「设置」或「开发者」页面可以找到

**⚠️ 安全提示：**
- API Key 具有账号权限，请妥善保管
- 不要提交到代码仓库
- 定期轮换 Key 以提高安全性
- 使用环境变量存储，不要硬编码在配置文件中

---

### Q: 配置文件在哪里？

**A:** OpenClaw 的配置文件位于用户主目录下：

**配置文件路径：**
```
~/.openclaw/config.json
```

**完整路径示例：**
- Linux/Mac: `/home/用户名/.openclaw/config.json`
- Windows: `C:\Users\用户名\.openclaw\config.json`

**查看配置：**
```bash
cat ~/.openclaw/config.json
```

**编辑配置：**
```bash
# 使用你喜欢的编辑器
nano ~/.openclaw/config.json
# 或
code ~/.openclaw/config.json
# 或
vim ~/.openclaw/config.json
```

**配置结构示例：**
```json
{
  "model": {
    "provider": "bailian",
    "apiKey": "sk-xxx",
    "defaultModel": "qwen3.5-plus"
  },
  "channels": {
    "discord": {
      "botToken": "xxx",
      "channelId": "xxx"
    },
    "feishu": {
      "appId": "xxx",
      "appSecret": "xxx"
    }
  },
  "workspace": "/home/用户名/.openclaw/workspace"
}
```

**修改配置后需要重启 OpenClaw：**
```bash
openclaw gateway restart
```

---

## 使用相关

### Q: 如何切换会话？

**A:** OpenClaw 支持多会话管理，切换方式取决于你使用的渠道：

**1. Discord 频道**
- 每个 Discord 频道是一个独立会话
- 切换到不同频道即可切换会话
- 使用频道列表选择目标频道

**2. 飞书群聊**
- 每个飞书群聊是独立会话
- 在不同群聊中发送消息即可切换

**3. 命令行会话**
```bash
# 列出所有会话
openclaw sessions list

# 创建新会话
openclaw sessions create --name "新会话名"

# 切换会话
openclaw sessions switch --name "目标会话名"

# 查看当前会话
openclaw sessions current
```

**4. 使用标签/上下文**
在某些界面中，可以通过标签页或上下文选择器切换会话。

**会话隔离：**
- 每个会话有独立的记忆和上下文
- 切换会话不会丢失之前的对话
- 会话数据保存在 `~/.openclaw/sessions/` 目录

---

### Q: 如何加载技能？

**A:** OpenClaw 的技能系统允许你扩展功能。加载技能有以下几种方式：

**1. 自动加载**
- 放在 `~/.openclaw/workspace/skills/` 目录的技能会自动加载
- 重启 OpenClaw 后生效

**2. 手动加载**
```bash
# 加载单个技能
openclaw skills load ./my-skill

# 加载所有技能
openclaw skills load-all
```

**3. 使用 ClawHub 安装技能**
```bash
# 搜索技能
clawhub search 技能名

# 安装技能
clawhub install 技能名

# 更新技能
clawhub update 技能名

# 列出已安装技能
clawhub list
```

**4. 技能目录结构**
```
my-skill/
├── SKILL.md        # 技能描述和触发条件
├── index.js        # 技能主逻辑
├── package.json    # 依赖配置
└── assets/         # 资源文件（可选）
```

**5. 验证技能加载**
```bash
# 查看已加载技能列表
openclaw skills list

# 查看技能状态
openclaw skills status 技能名
```

**技能不生效的排查：**
1. 检查 SKILL.md 中的描述是否正确
2. 确认技能目录在正确的路径
3. 查看 OpenClaw 日志是否有错误
4. 重启 OpenClaw Gateway

---

## 渠道相关

### Q: Discord 不工作怎么办？

**A:** Discord 集成问题通常有以下几种情况：

**1. Bot 无响应**
- 检查 Bot Token 是否正确
- 确认 Bot 已邀请到服务器
- 检查 Bot 是否有发送消息权限

**2. 权限问题**
- 进入服务器设置 → 角色
- 确保 OpenClaw Bot 角色有以下权限：
  - 发送消息
  - 读取消息历史
  - 添加反应
  - 嵌入链接

**3. 配置检查**
```json
{
  "channels": {
    "discord": {
      "botToken": "MTIzNDU2Nzg5MDEyMzQ1Njc4OQ.xxx.xxx",
      "channelId": "1234567890123456789"
    }
  }
}
```

**4. 常见问题**
- **Token 过期**：重新生成 Bot Token
- **频道 ID 错误**：在 Discord 中启用开发者模式，右键频道复制 ID
- **Gateway 未运行**：`openclaw gateway status` 检查状态

**5. 调试方法**
```bash
# 查看 Gateway 日志
openclaw gateway logs

# 重启 Gateway
openclaw gateway restart

# 测试连接
openclaw channels test discord
```

**6. 隐私设置**
- 确保服务器允许 Bot 访问
- 检查是否有消息过滤规则阻止 Bot

---

### Q: 飞书配置失败怎么办？

**A:** 飞书（Feishu/Lark）集成需要正确配置应用权限。

**1. 创建飞书应用**
- 访问：https://open.feishu.cn/app
- 创建企业自建应用
- 获取 App ID 和 App Secret

**2. 配置权限**
在飞书开放平台，添加以下权限：
- `im:message` - 发送消息
- `im:chat` - 读取群聊信息
- `contact:contact` - 读取联系人（可选）
- `wiki:wiki` - 访问知识库（如需）
- `drive:drive` - 访问云文档（如需）

**3. 发布应用**
- 完成权限配置后，点击「发布」
- 将应用添加到需要使用的群聊

**4. 配置 OpenClaw**
```json
{
  "channels": {
    "feishu": {
      "appId": "cli_xxxxxxxxxxxxxxxx",
      "appSecret": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    }
  }
}
```

**5. 常见问题**
- **权限不足**：检查应用是否已发布并添加到群聊
- **回调地址错误**：确保回调 URL 配置正确
- **加密密钥**：如果启用了消息加密，需要配置 Verification Token

**6. 调试**
```bash
# 测试飞书连接
openclaw channels test feishu

# 查看应用权限
openclaw feishu scopes
```

**7. 获取帮助**
- 飞书开放平台文档：https://open.feishu.cn/document/
- 检查应用事件订阅配置

---

## 费用相关

### Q: OpenClaw 收费吗？

**A:** OpenClaw 本身是**开源免费**的。

**免费部分：**
- ✅ OpenClaw 核心框架
- ✅ 基础技能系统
- ✅ 本地会话管理
- ✅ 社区技能（ClawHub）

**可能产生费用的部分：**
- ❗ AI 模型 API 调用（按使用量计费）
- ❗ 第三方服务（如 Discord、飞书的企业版功能）
- ❗ 云服务器托管（如果部署在云端）

**总结：**
- OpenClaw 软件免费
- 你需要为自己使用的 AI 模型付费
- 类似「手机免费，话费自理」的模式

---

### Q: API 费用多少？

**A:** API 费用取决于你使用的模型提供商和调用量。

**主流模型价格参考（2026 年 3 月 8 日官网验证，每 1M tokens）：**

#### 国外模型（美元定价）

| 模型 | 输入价格 | 输出价格 | 上下文窗口 | 官网来源 |
|------|---------|---------|------------|----------|
| GPT-5.4 | $2.50 | $15.00 | 1.05M | [OpenRouter](https://openrouter.ai/openai) |
| GPT-5.4 Pro | $30.00 | $180.00 | 1M | [PortKey](https://portkey.ai) |
| Claude Opus 4.6 | $5.00 | $25.00 | 1M | [Anthropic](https://www.anthropic.com/claude/opus) |
| Claude Sonnet 4.6 | $3.00 | $15.00 | 1M | [Anthropic](https://www.anthropic.com/claude/opus) |
| Gemini 3.1 Pro | $2.00 (<200K)<br>$4.00 (>200K) | $12.00 (<200K)<br>$18.00 (>200K) | 1M | [Google AI](https://ai.google.dev/gemini-api/docs/pricing) |

**备注：**
- GPT-5.4 超过 272K 有 2x 价格加成
- Gemini 3.1 Pro 超过 200K 有 2x 价格加成

#### 国内模型 - 官方平台（美元）

| 模型 | 平台 | 输入价格 | 输出价格 | 上下文窗口 | 官网来源 |
|------|------|---------|---------|------------|----------|
| MiniMax-M2.5 | MiniMax 官方 | $0.30 | $1.20 | 196.6K | [MiniMax](https://platform.minimax.io/docs/guides/pricing-paygo) |
| kimi-k2.5 | Moonshot 官方 | $0.60<br>($0.10 缓存命中) | $3.00 | 256K | [Moonshot](https://platform.moonshot.ai/docs/pricing/chat) |
| glm-5 | Z.ai 官方 | $1.00<br>($0.20 缓存输入) | $3.20 | 202.8K | [Z.ai](https://docs.z.ai/guides/overview/pricing) |

#### 国内模型 - 阿里云百炼（人民币，中国内地部署）

| 模型 | 上下文窗口 | 输入价格 | 输出价格 | 折合美元 |
|------|------------|---------|---------|----------|
| qwen3.5-plus | 1M | ¥0.80/1M | ¥4.80/1M | $0.11/$0.67 |
| kimi-k2.5 | 256K | ¥4.00/1M | ¥21.00/1M | $0.55/$2.92 |
| glm-5 | 202.8K | ¥4.00/1M | ¥18.00/1M | $0.55/$2.50 |
| MiniMax-M2.5 | 196.6K | ¥2.10/1M | ¥8.40/1M | $0.29/$1.17 |

**备注：**
- 阿里云百炼中国内地部署最便宜
- kimi-k2.5 和 glm-5 有缓存价格，缓存命中时更便宜
- 汇率参考：1 USD ≈ 7.2 CNY

> 💡 **重要趋势**：中国开源模型价格远低于国外模型（约 30-60 倍差价）。2026 年 2 月，中国模型调用量首次超过美国。

**费用估算示例：**
- 一次典型对话：约 1000-3000 tokens
- 使用 DeepSeek V3：约 ¥0.003-0.01/次
- 每天 100 次对话：约 ¥0.3-1/天
- 每月费用：约 ¥10-30（国内模型）

**省钱技巧：**
1. 使用性价比高的模型（如 Qwen-Plus、DeepSeek V3）
2. 合理设置上下文长度，避免不必要的 token 消耗
3. 对于简单任务，使用小模型
4. 监控使用量，设置预算提醒
5. 利用免费额度（各平台通常有新手赠送）

**查看用量：**
- 阿里云百炼控制台
- OpenAI Platform Usage 页面
- 各平台都有用量统计和账单

---

## 其他问题

### Q: 如何更新 OpenClaw？

**A:** 
```bash
# npm 安装更新
npm update -g openclaw

# 或重新安装
npm install -g openclaw@latest

# 验证版本
openclaw --version
```

---

### Q: 如何查看日志？

**A:**
```bash
# 查看 Gateway 日志
openclaw gateway logs

# 实时跟踪日志
openclaw gateway logs --follow

# 查看最近 100 行
openclaw gateway logs --lines 100
```

日志文件位置：`~/.openclaw/logs/`

---

### Q: 如何备份数据？

**A:** 备份以下目录：
```bash
# 配置
~/.openclaw/config.json

# 工作区（重要！）
~/.openclaw/workspace/

# 会话数据
~/.openclaw/sessions/

# 技能
~/.openclaw/skills/
```

建议定期备份到云存储或外部硬盘。

---

### Q: 遇到问题如何求助？

**A:** 
1. **查看文档**：先阅读官方文档和本 FAQ
2. **搜索 Issues**：在 GitHub 搜索类似问题
3. **提交 Issue**：提供详细信息和错误日志
4. **社区讨论**：加入 OpenClaw 社区群聊

**提交 Issue 时请包含：**
- OpenClaw 版本
- 操作系统和版本
- Node.js 版本
- 完整的错误信息
- 复现步骤

---

### Q: 可以贡献代码吗？

**A:** 当然可以！OpenClaw 是开源项目。

- GitHub: 搜索 OpenClaw 仓库
- 提交 PR 前请阅读贡献指南
- 欢迎提交 Bug 报告、功能建议、文档改进

---

## 未找到答案？

如果本 FAQ 没有解决你的问题：

1. 查看完整文档：`openclaw docs`
2. 访问官方文档网站
3. 在社区中提问
4. 提交 GitHub Issue

---

*最后更新：2026 年 3 月*
*维护者：OpenClaw 社区*
