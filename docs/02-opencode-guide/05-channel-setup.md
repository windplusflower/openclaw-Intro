# 渠道配置

> 配置 Discord、飞书、钉钉等消息渠道

渠道是 OpenClaw 与用户沟通的桥梁。通过配置不同的渠道，你可以让 OpenClaw 在 Discord、飞书、钉钉等平台上与你互动。

---

## 什么是渠道

### 渠道的定义

**渠道（Channel）** 是 OpenClaw 接收消息和发送响应的通信路径。简单来说，渠道就是 OpenClaw"出现"的地方。

想象一下：
- 📱 微信是一个渠道
- 💬 Discord 是一个渠道
- 📧 邮件是一个渠道
- 📞 电话是一个渠道

OpenClaw 可以同时"出现"在多个渠道中，在不同平台上为你服务。

### 支持的渠道类型

OpenClaw 支持多种主流通信平台：

| 渠道类型 | 适用场景 | 配置难度 |
|---------|---------|---------|
| **Discord** | 个人使用、社区管理、游戏相关 | ⭐⭐ 简单 |
| **飞书 (Feishu)** | 企业协作、团队沟通 | ⭐⭐⭐ 中等 |
| **钉钉 (DingTalk)** | 企业办公、考勤管理 | ⭐⭐⭐ 中等 |
| **Telegram** | 隐私优先的即时通讯 | ⭐⭐ 简单 |
| **微信** | 日常沟通（需企业微信） | ⭐⭐⭐⭐ 较复杂 |

> 💡 **提示**：本教程重点讲解 Discord、飞书和钉钉的配置方法。其他渠道的配置思路类似。

### 渠道 vs 会话

很多初学者容易混淆"渠道"和"会话"的概念：

```
渠道 (Channel)          会话 (Session)
    │                       │
    ▼                       ▼
  平台/载体              具体对话
  (在哪里沟通)          (和谁沟通)
  
例子：                  例子：
- Discord 服务器         - 与用户 A 的私聊
- 飞书群组              - 与用户 B 的群聊
- 钉钉部门              - 频道中的特定话题
```

**关键区别：**
- 渠道是**平台级别**的配置（如：整个 Discord 服务器）
- 会话是**对话级别**的概念（如：某次具体聊天）
- 一个渠道可以包含多个会话
- 配置渠道后，OpenClaw 才能在该渠道中创建会话

---

## Discord 配置

Discord 是最受欢迎的配置渠道之一，适合个人使用和社区管理。

### 创建 Discord Bot

**步骤 1：访问 Discord 开发者门户**

打开浏览器，访问：https://discord.com/developers/applications

**步骤 2：创建新应用**

1. 点击右上角 **"New Application"** 按钮
2. 输入应用名称（如：`MyOpenClawBot`）
3. 勾选同意条款
4. 点击 **"Create"**

**步骤 3：创建 Bot**

1. 在左侧菜单选择 **"Bot"**
2. 点击 **"Add Bot"** 按钮
3. 确认添加（点击 **"Yes, do it!"**）

**步骤 4：配置 Bot 权限**

在 Bot 页面，向下滚动找到 **"Privileged Gateway Intents"**：
- ✅ 启用 **MESSAGE CONTENT INTENT**（允许读取消息内容）
- ✅ 启用 **PRESENCE INTENT**（可选，查看用户状态）
- ✅ 启用 **SERVER MEMBERS INTENT**（可选，查看成员信息）

### 获取 Bot Token

**步骤 1：重置/查看 Token**

1. 在 Bot 页面，找到 **"Token"** 区域
2. 点击 **"Reset Token"**（如果是第一次，会显示 **"View Token"**）
3. 系统会显示一串字符，这就是你的 Bot Token

**步骤 2：安全保存 Token**

⚠️ **重要安全提示：**
- Token 相当于 Bot 的密码
- **不要**截图分享
- **不要**上传到代码仓库
- 立即复制到安全的地方（密码管理器或加密笔记）

```
```

### 配置到 OpenClaw

**步骤 1：找到配置文件**

OpenClaw 的渠道配置通常位于：

**macOS:**
```bash
cd ~/.openclaw/workspace
code config.yaml
```

**Windows:**
```powershell
cd $env:USERPROFILE\.openclaw\workspace
code config.yaml
```

**步骤 2：添加 Discord 配置**

在配置文件中添加以下内容：

```yaml
channels:
  discord:
    enabled: true
    token: "你的_BOT_TOKEN_粘贴在这里"
    # 可选配置
    prefix: "!"           # 命令前缀
    default_channel: ""   # 默认频道 ID
```

**步骤 3：邀请 Bot 到服务器**

1. 返回 Discord 开发者门户
2. 左侧菜单选择 **"OAuth2"** → **"URL Generator"**
3. 选择 scopes：
   - ✅ `bot`
   - ✅ `applications.commands`（如果需要斜杠命令）
4. 选择 Bot Permissions：
   - ✅ `Send Messages`
   - ✅ `Read Message History`
   - ✅ `Manage Messages`（可选）
5. 复制生成的 URL
6. 在浏览器打开 URL，选择要添加的服务器
7. 点击 **"Authorize"**

### 测试 Discord 渠道

**步骤 1：重启 OpenClaw**

配置完成后，需要重启 OpenClaw 使配置生效：

**macOS:**
```bash
# 如果使用 PM2
pm2 restart openclaw

# 或者直接重启
openclaw restart
```

**Windows:**
```powershell
# 如果使用 PM2
pm2 restart openclaw

# 或者在 PowerShell 中
openclaw restart
```

**步骤 2：发送测试消息**

1. 在 Discord 服务器中，找到 Bot 所在的频道
2. 发送消息：`!help` 或 `@BotName help`
3. 如果 Bot 回复，说明配置成功！✅

**步骤 3：检查日志**

如果 Bot 没有响应，查看日志：

**macOS:**
```bash
tail -f ~/.openclaw/logs/openclaw.log
```

**Windows:**
```powershell
Get-Content -Path "$env:USERPROFILE\.openclaw\logs\openclaw.log" -Tail -Wait
```

---

## 飞书配置

飞书适合企业团队协作场景，配置稍复杂但功能强大。

### 创建飞书应用

**步骤 1：访问飞书开发者平台**

打开浏览器，访问：https://open.feishu.cn/app

**步骤 2：登录开发者账号**

- 使用飞书账号扫码登录
- 需要是企业管理员或开发者角色

**步骤 3：创建企业自建应用**

1. 点击 **"创建企业自建应用"**
2. 填写应用信息：
   - 应用名称：`OpenClaw 助手`
   - 应用图标：上传一个图标（可选）
   - 应用描述：`智能助手`
3. 点击 **"创建"**

### 获取 App ID 和 Secret

**步骤 1：查看凭证**

1. 创建完成后，进入应用管理页面
2. 左侧菜单选择 **"凭证与基础信息"**
3. 记录以下信息：
   - **App ID**（应用 ID）
   - **App Secret**（应用密钥）

**步骤 2：配置权限**

1. 左侧菜单选择 **"权限管理"**
2. 添加以下权限：
   - ✅ `im:message`（发送和接收消息）
   - ✅ `im:chat`（管理会话）
   - ✅ `contact:user:readonly`（读取用户信息，可选）
3. 点击 **"申请权限"**，等待管理员审批

**步骤 3：配置事件订阅**

1. 左侧菜单选择 **"事件订阅"**
2. 启用 **"启用事件订阅"**
3. 配置订阅地址（Webhook URL）：
   ```
   https://你的域名/api/feishu/webhook
   ```
   > 💡 如果没有公网域名，可以使用 ngrok 等内网穿透工具

4. 搜索并添加事件：
   - ✅ `接收消息`
   - ✅ `消息已读`（可选）

### 配置到 OpenClaw

**步骤 1：编辑配置文件**

**macOS:**
```bash
cd ~/.openclaw/workspace
code config.yaml
```

**Windows:**
```powershell
cd $env:USERPROFILE\.openclaw\workspace
code config.yaml
```

**步骤 2：添加飞书配置**

```yaml
channels:
  feishu:
    enabled: true
    app_id: "cli_xxxxxxxxxxxxxxx"
    app_secret: "xxxxxxxxxxxxxxxxxxxxxxxxx"
    verification_token: "xxxxxxxxxxxxx"  # 事件订阅中的验证令牌
    encrypt_key: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"  # 如果启用了加密
```

**步骤 3：添加到飞书群组**

1. 在飞书中创建一个群组
2. 点击群组右上角 **"..."** → **"添加机器人"**
3. 选择你创建的应用
4. 点击 **"添加"**

### 测试飞书渠道

**步骤 1：重启 OpenClaw**

```bash
# macOS
openclaw restart

# Windows
openclaw restart
```

**步骤 2：发送测试消息**

1. 在飞书群组中 @OpenClaw 助手
2. 发送消息：`帮助` 或 `help`
3. 检查是否收到回复

**步骤 3：调试工具**

飞书开发者平台提供调试工具：
- 访问 **"事件订阅"** 页面
- 查看 **"订阅调试"** 标签
- 可以看到事件推送记录和响应状态

---

## 钉钉配置

钉钉配置与飞书类似，适合企业办公场景。

### 创建钉钉应用

**步骤 1：访问钉钉开发者平台**

打开浏览器，访问：https://open-dev.dingtalk.com/

**步骤 2：登录并创建应用**

1. 使用钉钉扫码登录
2. 点击 **"创建应用"**
3. 选择 **"企业内部开发"**
4. 填写应用信息：
   - 应用名称：`OpenClaw 助手`
   - 应用图标：上传图标
   - 应用描述：`智能助手`

### 获取 App Key 和 Secret

**步骤 1：查看凭证**

1. 进入应用详情页
2. 在 **"基础信息"** 标签页找到：
   - **AppKey**（客户端 ID）
   - **AppSecret**（客户端密钥）

**步骤 2：配置权限**

1. 选择 **"权限管理"** 标签页
2. 添加权限：
   - ✅ 机器人消息
   - ✅ 会话管理
   - ✅ 用户信息（可选）
3. 提交申请，等待审批

**步骤 3：配置机器人**

1. 选择 **"机器人"** 标签页
2. 点击 **"添加机器人"**
3. 选择 **"消息机器人"**
4. 配置：
   - 机器人名称：`OpenClaw`
   - 头像：上传头像
   - 消息接收模式：选择 **"接收所有消息"** 或 **"只接收@消息"**

### 配置到 OpenClaw

**步骤 1：编辑配置文件**

**macOS:**
```bash
cd ~/.openclaw/workspace
code config.yaml
```

**Windows:**
```powershell
cd $env:USERPROFILE\.openclaw\workspace
code config.yaml
```

**步骤 2：添加钉钉配置**

```yaml
channels:
  dingtalk:
    enabled: true
    app_key: "dingxxxxxxxxxxxxxx"
    app_secret: "xxxxxxxxxxxxxxxxxxxxxxxxx"
    agent_id: "123456789"  # 如果有多个应用
```

**步骤 3：添加到钉钉群组**

1. 在钉钉中创建或选择一个群组
2. 点击群设置 → **"智能群助手"**
3. 点击 **"添加机器人"**
4. 选择你创建的应用
5. 完成添加

### 测试钉钉渠道

**步骤 1：重启 OpenClaw**

```bash
# macOS
openclaw restart

# Windows
openclaw restart
```

**步骤 2：发送测试消息**

1. 在钉钉群组中 @OpenClaw
2. 发送：`测试` 或 `help`
3. 检查回复

**步骤 3：查看日志**

钉钉有详细的推送日志：
- 访问应用管理后台
- 选择 **"版本管理"** → **"日志查询"**
- 查看消息推送记录

---

## 多渠道管理

### 同时配置多个渠道

OpenClaw 支持同时运行在多个渠道上。配置示例：

```yaml
channels:
  discord:
    enabled: true
    token: "DISCORD_TOKEN_HERE"
    prefix: "!"
  
  feishu:
    enabled: true
    app_id: "cli_xxxxxxxxxxxxxxx"
    app_secret: "xxxxxxxxxxxxxxxxxxxxxxxxx"
  
  dingtalk:
    enabled: true
    app_key: "dingxxxxxxxxxxxxxx"
    app_secret: "xxxxxxxxxxxxxxxxxxxxxxxxx"
```

**配置要点：**
- ✅ 每个渠道的 `enabled` 设为 `true`
- ✅ 确保每个渠道的凭证正确
- ✅ 可以为不同渠道设置不同的前缀或行为

### 渠道优先级

当多个渠道同时收到消息时，OpenClaw 会并行处理。但你可以通过配置设置优先级：

```yaml
channels:
  # 高优先级渠道（优先响应）
  discord:
    enabled: true
    priority: 1
    token: "..."
  
  # 中优先级
  feishu:
    enabled: true
    priority: 2
    app_id: "..."
  
  # 低优先级
  dingtalk:
    enabled: true
    priority: 3
    app_key: "..."
```

**优先级规则：**
- 数字越小，优先级越高
- 优先级影响资源分配和响应速度
- 不影响消息接收，只影响处理顺序

### 渠道切换

**临时禁用某个渠道：**

```yaml
channels:
  discord:
    enabled: false  # 临时禁用
    token: "..."
  
  feishu:
    enabled: true   # 保持启用
    app_id: "..."
```

**热重载配置（无需重启）：**

某些部署支持配置热重载：

**macOS:**
```bash
openclaw reload config
```

**Windows:**
```powershell
openclaw reload config
```

---

## 实践示例

### 示例 1：配置 Discord

**目标：** 成功配置 Discord 渠道并收到 Bot 回复

**步骤：**
1. 创建 Discord Bot（参考上文）
2. 获取 Bot Token
3. 编辑 `config.yaml` 添加 Discord 配置
4. 邀请 Bot 到你的测试服务器
5. 重启 OpenClaw
6. 发送 `!help` 测试

**检查清单：**
- [ ] Bot 已添加到服务器
- [ ] 配置文件语法正确
- [ ] Token 没有复制错误
- [ ] OpenClaw 日志无报错
- [ ] Bot 成功回复消息

**内容说明：** 15-

---

### 示例 2：配置飞书

**目标：** 成功配置飞书渠道并在群组中使用

**步骤：**
1. 创建飞书企业自建应用
2. 获取 App ID 和 Secret
3. 配置事件订阅（可使用 ngrok 测试）
4. 编辑配置文件添加飞书信息
5. 将 Bot 添加到飞书群组
6. 重启 OpenClaw 并测试

**检查清单：**
- [ ] 应用已创建并审批通过
- [ ] 事件订阅地址可访问
- [ ] 权限已申请并通过
- [ ] 配置文件中凭证正确
- [ ] 群组中@Bot 有响应

**内容说明：** 25-

---

### 示例 3：配置多渠道

**目标：** 同时配置 Discord 和飞书，理解多渠道管理

**步骤：**
1. 完成练习 1 和练习 2
2. 在配置文件中同时启用两个渠道
3. 设置不同优先级
4. 重启 OpenClaw
5. 分别在两个平台发送消息
6. 观察响应时间和行为差异

**进阶任务：**
- 尝试在 Discord 和飞书发送相同指令
- 比较两个渠道的响应速度
- 测试渠道间状态是否同步

**内容说明：** 30-

---

## 常见问题

### Token 泄露怎么办

**紧急处理步骤：**

1. **立即重置 Token**
   - Discord：开发者门户 → Bot → Reset Token
   - 飞书：应用管理 → 凭证与基础信息 → 重置 Secret
   - 钉钉：应用管理 → 基础信息 → 重置 Secret

2. **更新配置文件**
   ```bash
   # 编辑配置文件
   code ~/.openclaw/workspace/config.yaml
   
   # 粘贴新 Token
   # 保存并重启
   ```

3. **重启 OpenClaw**
   ```bash
   openclaw restart
   ```

4. **检查异常活动**
   - 查看日志是否有异常请求
   - 检查 Bot 是否发送了异常消息

**预防措施：**
- ✅ 使用密码管理器存储 Token
- ✅ 配置文件加入 `.gitignore`
- ✅ 使用环境变量代替明文配置
- ✅ 定期轮换 Token（建议每 90 天）

---

### 渠道不工作怎么办

**排查步骤：**

**1. 检查配置语法**

```bash
# 验证 YAML 语法
# macOS
python3 -c "import yaml; yaml.safe_load(open('~/.openclaw/workspace/config.yaml'))"

# Windows
python -c "import yaml; yaml.safe_load(open('$env:USERPROFILE\.openclaw\workspace\config.yaml'))"
```

**2. 查看日志**

```bash
# macOS
tail -100 ~/.openclaw/logs/openclaw.log | grep -i error

# Windows
Get-Content "$env:USERPROFILE\.openclaw\logs\openclaw.log" -Tail 100 | Select-String "error"
```

**3. 检查网络连接**

```bash
# 测试 API 连通性
curl -I https://discord.com/api
curl -I https://open.feishu.cn/open-apis
curl -I https://oapi.dingtalk.com
```

**4. 验证凭证**

- 确认 Token/Secret 没有复制错误
- 检查是否有空格或换行
- 确认应用权限已审批

**5. 重启服务**

```bash
openclaw restart
```

**常见错误代码：**

| 错误 | 原因 | 解决方案 |
|-----|------|---------|
| 401 Unauthorized | Token 无效 | 重置 Token |
| 403 Forbidden | 权限不足 | 申请对应权限 |
| 429 Too Many Requests | 请求限流 | 等待后重试 |
| 500 Internal Error | 服务端错误 | 联系平台支持 |

---

### 如何删除渠道配置

**方法 1：禁用渠道**

编辑配置文件，将 `enabled` 设为 `false`：

```yaml
channels:
  discord:
    enabled: false  # 禁用但保留配置
    token: "..."
```

**方法 2：删除配置**

直接从配置文件中删除整个渠道块：

```yaml
# 删除前
channels:
  discord:
    enabled: true
    token: "..."
  feishu:
    enabled: true

# 删除后
channels:
  feishu:
    enabled: true
```

**方法 3：删除应用**

如果要彻底删除渠道：

1. 在配置文件中删除配置
2. 重启 OpenClaw
3. 到对应平台删除应用/Bot
   - Discord：开发者门户 → 删除应用
   - 飞书：应用管理 → 删除应用
   - 钉钉：应用管理 → 删除应用

**⚠️ 注意事项：**
- 删除配置前备份配置文件
- 删除应用后无法恢复历史消息
- 通知相关用户渠道将停用

---

## 本节要点

📝 **关键知识点：**

1. **渠道是什么**
   - 渠道是 OpenClaw 的通信路径
   - 支持 Discord、飞书、钉钉等多个平台
   - 渠道 ≠ 会话（渠道是平台，会话是对话）

2. **配置流程**
   - 创建平台应用/Bot
   - 获取凭证（Token/Secret）
   - 编辑配置文件
   - 重启 OpenClaw
   - 测试验证

3. **多渠道管理**
   - 可同时配置多个渠道
   - 支持优先级设置
   - 可动态启用/禁用

4. **安全要点**
   - Token 要保密存储
   - 定期轮换凭证
   - 泄露后立即重置

---

## 下一节

👉 **06-advanced-configuration.md** - 高级配置

在下一节中，你将学习：
- 环境变量配置
- 多实例部署
- 负载均衡
- 性能优化
- 监控与告警

---

## 附录：快速参考

### 配置文件位置

| 系统 | 路径 |
|-----|------|
| macOS | `~/.openclaw/workspace/config.yaml` |
| Windows | `%USERPROFILE%\.openclaw\workspace\config.yaml` |
| Linux | `~/.openclaw/workspace/config.yaml` |

### 常用命令

```bash
# 重启 OpenClaw
openclaw restart

# 查看日志
openclaw logs

# 验证配置
openclaw config:check

# 热重载
openclaw reload config
```

### 官方文档链接

- [Discord 开发者文档](https://discord.com/developers/docs)
- [飞书开放平台](https://open.feishu.cn/document)
- [钉钉开放平台](https://open.dingtalk.com/document)

---

*最后更新：2026-03-05*  
*文档版本：1.0*
