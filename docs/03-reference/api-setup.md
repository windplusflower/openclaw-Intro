# API 配置指南

欢迎使用 OpenClaw！本指南将帮助你配置各种 AI 服务商的 API，让你的智能助手能够正常运作。无论你是第一次使用，还是想要切换服务商，都能在这里找到详细的步骤说明。

---

## 📚 基础概念：什么是 API 和 API Key？

### 什么是 API？

**API**（Application Programming Interface，应用程序编程接口）就像是**餐厅的服务员**。

想象你去餐厅吃饭：
- 你不需要亲自去厨房做饭（那太复杂了）
- 你只需要告诉服务员你想吃什么
- 服务员把你的需求传达给厨房
- 厨房做好后，服务员把菜端给你

**AI 的 API 也是一样的道理**：
- 你不需要自己搭建一个 AI 模型（那需要超级计算机和海量数据）
- 你只需要通过 API 发送你的问题
- API 把你的问题传给 AI 公司的服务器
- AI 处理完后，通过 API 把回答返回给你

**生活中的 API 例子**：
| 场景 | 类比 |
|------|------|
| 外卖 App | 你下单 → 外卖平台 API → 餐厅 → 骑手送餐 |
| 天气 App | 你打开 App → 调用气象局 API → 获取天气数据 |
| 地图导航 | 输入目的地 → 调用地图 API → 返回路线 |
| OpenClaw | 你输入问题 → 调用 AI API → 返回 AI 回答 |

### 什么是 API Key？

**API Key** 就像是你的**身份证 + 钥匙 + 密码**的组合。

**用餐厅的例子理解**：
- 你是 VIP 会员，有一张**会员卡**（API Key）
- 这张卡证明你是谁（身份认证）
- 这张卡能打开餐厅的门（访问权限）
- 这张卡记录你消费了多少（计费依据）

**API Key 的作用**：

| 作用 | 说明 | 类比 |
|------|------|------|
| **身份认证** | 证明你是谁 | 身份证 |
| **访问控制** | 确定你能使用哪些功能 | 门禁卡 |
| **计费统计** | 记录你的使用量，用于收费 | 电表/水表 |
| **安全防护** | 防止别人冒充你使用 | 密码 |

### 为什么需要 API Key？

**1. 身份认证 - 证明"你是你"**
```
就像寄快递需要写清楚寄件人和收件人一样，
API Key 让 AI 服务知道"这个请求是谁发的"。
```

**2. 计费统计 - "用了多少，付多少钱"**
```
AI 服务是按使用量收费的（按 Token 数量）。
API Key 就像你的"账号"，记录你用了多少，月底一起结算。
```

**3. 权限控制 - "你能做什么"**
```
不同的 API Key 可能有不同的权限：
- 普通用户：只能使用基础模型
- 付费用户：可以使用高级模型
- 管理员：可以管理其他用户
```

**4. 安全防护 - "防止被盗用"**
```
如果你的 API Key 泄露了，别人就能冒充你使用 AI 服务，
产生的费用都算在你的账上！所以 API Key 要像密码一样保管好。
```

### 🔐 API Key 安全须知

**⚠️ 绝对不要做**：
- ❌ 把 API Key 截图发到网上
- ❌ 把 API Key 写在公开代码里（GitHub 等）
- ❌ 把 API Key 发给陌生人
- ❌ 在公共电脑上保存 API Key

**✅ 正确做法**：
- ✅ 保存在本地配置文件里
- ✅ 使用环境变量（不直接写在代码中）
- ✅ 定期更换 API Key（如果怀疑泄露）
- ✅ 如果发现异常使用，立即在平台禁用该 Key

---

## ❓ 常见 Q&A

### Q1: API Key 泄露了怎么办？

**立即采取以下措施**：
1. **马上登录 AI 服务商平台**（如 OpenAI、阿里云百炼等）
2. **删除/禁用泄露的 API Key**
3. **创建新的 API Key**
4. **更新 OpenClaw 配置**，使用新的 Key
5. **检查账单**，确认没有异常消费

> 💡 **小提示**：大多数平台都支持创建多个 API Key，建议定期轮换。

### Q2: 哪里获取 API Key？

| 服务商 | 获取地址 | 大致流程 |
|--------|----------|----------|
| **OpenAI** | platform.openai.com | 注册账号 → 绑定支付方式 → 创建 API Key |
| **Anthropic** | console.anthropic.com | 注册账号 → 验证身份 → 创建 API Key |
| **阿里云百炼** | bailian.console.aliyun.com | 登录阿里云 → 开通百炼服务 → 创建 API-KEY |
| **百度千帆** | cloud.baidu.com | 注册百度智能云 → 开通千帆平台 → 创建应用 |
| **DeepSeek** | platform.deepseek.com | 注册账号 → 充值 → 创建 API Key |

### Q3: API Key 和账号密码有什么区别？

| 对比项 | 账号密码 | API Key |
|--------|----------|---------|
| **用途** | 登录网站/App | 程序调用服务 |
| **使用方式** | 手动输入 | 自动发送 |
| **格式** | 自己设置 | 系统自动生成 |
| **泄露风险** | 高（可能被盗号） | 极高（直接产生费用） |
| **更换频率** | 偶尔 | 建议定期更换 |

### Q4: 一个 API Key 可以在多台设备上使用吗？

**可以，但不建议**。

- 技术上：一个 API Key 可以在多台电脑、多个程序同时使用
- 安全上：如果其中一台设备泄露，所有设备都受影响
- 管理上：难以追踪哪台设备产生了哪些费用

**建议做法**：
- 每台设备使用独立的 API Key
- 给每个 Key 起个描述性的名字（如"MacBook-Home"、"Windows-Office"）

### Q5: API Key 有有效期吗？

**取决于服务商**：
- 大多数 API Key **没有固定有效期**，可以长期使用
- 但服务商可能会**定期要求更新**（如每 6 个月）
- 如果**长期不使用**，部分服务商可能会禁用
- 如果**账号欠费**，API Key 会被立即停用

---

---

## 支持的 AI 服务商

OpenClaw 支持多种主流 AI 服务商，你可以根据需求选择：

### 国际服务商

| 服务商 | 推荐模型 | 特点 |
|--------|----------|------|
| **OpenAI** | gpt-4-turbo | 生态完善，工具调用能力强，适合复杂任务 |
| **Anthropic** | claude-sonnet-4, claude-opus-4.1 | 长上下文处理优秀（200K），代码能力强，适合深度分析 |

### 国内服务商

| 服务商 | 推荐模型 | 特点 |
|--------|----------|------|
| **DeepSeek** | deepseek-v3 | 价格极低，性能优秀，128K 上下文 |
| **阿里通义** | qwen2.5-1m, qwen-max | 多模态能力强，支持 1M 上下文，性价比高 |
| **MiniMax** | minimax-m2.5 | 低价高性能，约$1.1/百万 tokens |
| **Kimi（月之暗面）** | kimi-k2.5 | 长文本处理优秀 |
| **智谱 AI** | glm-5 | 国产大模型，价格亲民 |

### 选择建议

- **新手入门**：推荐从百度文心或阿里通义开始，价格低且中文支持好
- **专业开发**：OpenAI 或 Anthropic 更适合复杂工作流
- **混合使用**：可以配置多个 API，根据任务类型自动切换

---

## OpenAI 配置

### 第一步：获取 API Key

1. 访问 [OpenAI 平台](https://platform.openai.com/)
2. 登录或注册账号（需要国际手机号或邮箱）
3. 点击右上角头像 → **View API keys**
4. 点击 **Create new secret key**
5. 给密钥起个名字（如 "OpenClaw"），点击 **Create**
6. **立即复制密钥**（只会显示一次，丢失需重新生成）

> ⚠️ **重要提示**：API Key 格式为 `sk-` 开头的一长串字符，请妥善保管，不要分享给他人。

### 第二步：配置到 OpenClaw

OpenClaw 支持多种配置方式，选择最适合你的一种：

#### 方式一：环境变量（推荐）

在终端执行以下命令：

```bash
# 临时设置（当前会话有效）
export OPENAI_API_KEY="sk-your-api-key-here"

# 永久设置（添加到 ~/.bashrc 或 ~/.zshrc）
echo 'export OPENAI_API_KEY="sk-your-api-key-here"' >> ~/.bashrc
source ~/.bashrc
```

#### 方式二：配置文件

在 OpenClaw 工作区创建或编辑配置文件：

```bash
# 编辑配置
nano ~/.openclaw/workspace/.env
```

添加以下内容：

```env
OPENAI_API_KEY=sk-your-api-key-here
OPENAI_MODEL=gpt-4-turbo
```

#### 方式三：命令行参数

启动时直接指定：

```bash
openclaw start --api-key sk-your-api-key-here --model gpt-4-turbo
```

### 第三步：测试连接

配置完成后，运行以下命令验证：

```bash
# 简单测试
openclaw test-connection

# 或发送测试消息
openclaw send "你好，请回复一个表情符号"
```

如果看到正常回复，说明配置成功！

### 常见问题

| 问题 | 解决方案 |
|------|----------|
| `Invalid API key` | 检查密钥是否复制完整，有无多余空格 |
| `Rate limit exceeded` | 等待几分钟后重试，或升级到更高配额计划 |
| `Model not found` | 确认模型名称正确，检查账号是否有该模型权限 |
| 连接超时 | 检查网络，可能需要配置代理 |

---

## Anthropic 配置

### 获取 API Key

1. 访问 [Anthropic 控制台](https://console.anthropic.com/)
2. 注册/登录账号
3. 进入 **API Keys** 页面
4. 点击 **Create Key**
5. 复制密钥（格式：`sk-ant-...`）

### 配置方法

```bash
# 环境变量
export ANTHROPIC_API_KEY="sk-ant-your-key-here"
export ANTHROPIC_MODEL="claude-sonnet-4"

# 或写入配置文件
echo 'ANTHROPIC_API_KEY=sk-ant-your-key-here' >> ~/.openclaw/workspace/.env
echo 'ANTHROPIC_MODEL=claude-sonnet-4' >> ~/.openclaw/workspace/.env
```

### 测试连接

```bash
openclaw test-connection --provider anthropic
```

### 注意事项

- Anthropic 的 API 有严格的速率限制，新用户建议从 `claude-haiku` 开始
- 长文档处理时，建议使用 `claude-sonnet` 平衡性能和成本

---

## 国内服务商配置

### 百度文心（ERNIE）

#### 获取凭证

1. 访问 [百度智能云](https://cloud.baidu.com/)
2. 进入 **千帆大模型平台**
3. 创建应用，获取 **API Key** 和 **Secret Key**

#### 配置

```bash
# 环境变量
export BAIDU_API_KEY="your-api-key"
export BAIDU_SECRET_KEY="your-secret-key"
export BAIDU_MODEL="ernie-4.0-turbo"

# 配置文件
cat >> ~/.openclaw/workspace/.env << EOF
BAIDU_API_KEY=your-api-key
BAIDU_SECRET_KEY=your-secret-key
BAIDU_MODEL=ernie-4.0-turbo
EOF
```

### 阿里通义（Qwen）

#### 获取凭证

1. 访问 [阿里云百炼](https://bailian.console.aliyun.com/)
2. 开通 **模型服务**
3. 创建 API-KEY

#### 配置

```bash
# 环境变量
export DASHSCOPE_API_KEY="sk-your-dashscope-key"
export DASHSCOPE_MODEL="qwen-max"

# 配置文件
cat >> ~/.openclaw/workspace/.env << EOF
DASHSCOPE_API_KEY=sk-your-dashscope-key
DASHSCOPE_MODEL=qwen-max
EOF
```

### 国内服务商优势

- ✅ 无需代理，直连访问
- ✅ 中文理解更准确
- ✅ 价格更亲民（约为国际服务商的 1/3）
- ✅ 支持支付宝/微信支付

---

## 多 API 配置

OpenClaw 支持同时配置多个 API，实现智能切换和负载均衡。

### 配置示例

创建高级配置文件 `~/.openclaw/workspace/.env.multi`：

```env
# 主 API（默认使用）
PRIMARY_PROVIDER=openai
OPENAI_API_KEY=sk-primary-key
OPENAI_MODEL=gpt-4-turbo

# 备用 API
FALLBACK_PROVIDER=anthropic
ANTHROPIC_API_KEY=sk-ant-fallback-key
ANTHROPIC_MODEL=claude-sonnet-4

# 国内 API（用于简单任务节省成本）
DOMESTIC_PROVIDER=baidu
BAIDU_API_KEY=baidu-key
BAIDU_SECRET_KEY=baidu-secret
BAIDU_MODEL=ernie-4.0-turbo

# 路由规则
# simple: 使用国内 API
# complex: 使用主 API
# creative: 使用备用 API
ROUTING_ENABLED=true
```

### 使用场景

| 任务类型 | 推荐 API | 原因 |
|----------|----------|------|
| 日常问答 | 百度文心 | 成本低，响应快 |
| 代码生成 | OpenAI / 通义 | 代码能力强 |
| 长文档分析 | Anthropic | 上下文窗口大 |
| 创意写作 | Anthropic / OpenAI | 表达更自然 |

### 自动切换

启用智能路由后，OpenClaw 会根据任务复杂度自动选择：

```bash
# 启用路由
openclaw config set routing.enabled true
openclaw config set routing.strategy auto
```

---

## 费用对比（2026 年）

以下是各服务商的大致价格（以输入 + 输出综合计算）：

### 国际服务商（美元/百万 Tokens，2026 年 3 月）

> ⚠️ **注意**：以下模型信息因网络限制无法实时验证，标注为「待验证」。建议访问官方文档获取最新信息。

| 模型 | 输入价格 | 输出价格 | 上下文窗口 | 状态 |
|------|----------|----------|------------|------|
| GPT-5.4 | $2.50 | $15.00 | 1.05M | 待验证 |
| GPT-5.4 Pro | $30.00 | $180.00 | 1.05M | 待验证 |
| Claude Opus 4.6 | $5.00 | $25.00 | 1M | 待验证 |
| Claude Sonnet 4.6 | $3.00 | $15.00 | 1M | 待验证 |
| Gemini 3.1 Pro | $2.00 | $12.00 | 1M | 待验证 |

**官方文档参考**：
- OpenAI: https://platform.openai.com/docs/models
- Anthropic: https://docs.anthropic.com/en/docs/about-claude/models
- Google: https://ai.google.dev/gemini-api/docs/models

### 国内服务商（人民币/百万 Tokens）

> ⚠️ **注意**：以下模型信息因网络限制无法实时验证，标注为「待验证」。建议访问官方文档获取最新信息。

| 模型 | 输入价格 | 输出价格 | 上下文窗口 | 状态 |
|------|----------|----------|------------|------|
| DeepSeek V3 | 约¥1-2 | 约¥1-2 | 128K-1M | 待验证 |
| MiniMax M2.5 | 约¥8 | 约¥8 | 约 256K | 待验证 |
| Kimi K2.5 | 低价 | 低价 | 约 256K | 待验证 |
| GLM-5 | 低价 | 低价 | 约 128K | 待验证 |
| 通义 Max | ¥40 | ¥120 | 约 128K | 待验证 |
| 通义 Plus | ¥4 | ¥12 | 约 128K | 待验证 |

**官方文档参考**：
- DeepSeek: https://platform.deepseek.com
- MiniMax: https://www.minimaxi.com
- Kimi: https://platform.moonshot.cn
- 智谱 AI: https://open.bigmodel.cn
- 阿里云百炼: https://bailian.console.aliyun.com

> 💡 **重要趋势**：中国开源模型价格远低于国外模型（约 30-60 倍差价）。2026 年 2 月，中国模型调用量首次超过美国。

### 成本估算示例

> ⚠️ **重要提醒**：以下估算基于「单次请求」的简单场景。实际使用中，AI 助手会进行多次工具调用，真实消耗可能是估算值的 **10-50 倍**！详见 [Token 概念](../01-ai-intro/02-token-concept.md) 中的详细说明。

假设每天使用 10 万 Tokens（约 50 次简单对话）：

- **DeepSeek V3**：约 ¥0.1-0.2/天（简单场景）/ **实际可能 ¥1-10/天**
- **MiniMax M2.5**：约 ¥0.8/天（简单场景）/ **实际可能 ¥8-40/天**
- **GPT-5.4**：约 $0.25/天 ≈ ¥1.8/天（简单场景）/ **实际可能 ¥18-90/天**
- **Claude Opus 4.6**：约 $0.50/天 ≈ ¥3.6/天（简单场景）/ **实际可能 ¥36-180/天**
- **Gemini 3.1 Pro**：约 $0.14/天 ≈ ¥1.0/天（简单场景）/ **实际可能 ¥10-50/天**

> 💡 **省钱技巧**：优先使用国内模型（如 DeepSeek V3），综合成本可降低 90% 以上。

---

## 本节要点

恭喜你完成了 API 配置的学习！让我们回顾一下关键点：

### ✅ 核心要点

1. **选择服务商**：根据需求选择国际或国内服务商
2. **获取密钥**：在对应平台创建并复制 API Key
3. **配置方式**：推荐环境变量或配置文件
4. **测试验证**：使用 `test-connection` 确认配置正确
5. **多 API 策略**：可配置多个 API 实现成本优化

### 📋 快速检查清单

- [ ] 已选择适合的 AI 服务商
- [ ] 已获取 API Key 并安全保存
- [ ] 已配置环境变量或配置文件
- [ ] 已通过连接测试
- [ ] 了解各服务商的价格差异

### 🚀 下一步

配置完成后，你可以：

1. 继续阅读其他文档，学习 OpenClaw 的高级功能
2. 尝试发送第一条消息，体验智能助手
3. 探索插件系统，扩展更多能力
4. 加入社区，与其他用户交流经验

### 🆘 需要帮助？

如果遇到问题：

- 查看官方文档：`docs/README.md`
- 检查常见问题：`docs/faq.md`
- 提交 Issue：GitHub 仓库
- 社区讨论：Discord / 微信群

---

**配置愉快！🎉**

> 提示：本指南会定期更新，建议收藏或订阅更新通知。
