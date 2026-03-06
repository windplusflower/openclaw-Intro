# API 配置指南

欢迎使用 OpenClaw！本指南将帮助你配置各种 AI 服务商的 API，让你的智能助手能够正常运作。无论你是第一次使用，还是想要切换服务商，都能在这里找到详细的步骤说明。

---

## 支持的 AI 服务商

OpenClaw 支持多种主流 AI 服务商，你可以根据需求选择：

### 国际服务商

| 服务商 | 推荐模型 | 特点 |
|--------|----------|------|
| **OpenAI** | gpt-4o, gpt-4o-mini | 生态完善，工具调用能力强，适合复杂任务 |
| **Anthropic** | claude-sonnet-4-20250514, claude-opus-4-20250514 | 长上下文处理优秀，代码能力强，适合深度分析 |

### 国内服务商

| 服务商 | 推荐模型 | 特点 |
|--------|----------|------|
| **百度文心** | ernie-4.0-turbo | 中文理解优秀，价格亲民，适合日常使用 |
| **阿里通义** | qwen-max, qwen-plus | 多模态能力强，代码生成优秀，性价比高 |

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
OPENAI_MODEL=gpt-4o
```

#### 方式三：命令行参数

启动时直接指定：

```bash
openclaw start --api-key sk-your-api-key-here --model gpt-4o
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
export ANTHROPIC_MODEL="claude-sonnet-4-20250514"

# 或写入配置文件
echo 'ANTHROPIC_API_KEY=sk-ant-your-key-here' >> ~/.openclaw/workspace/.env
echo 'ANTHROPIC_MODEL=claude-sonnet-4-20250514' >> ~/.openclaw/workspace/.env
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
OPENAI_MODEL=gpt-4o

# 备用 API
FALLBACK_PROVIDER=anthropic
ANTHROPIC_API_KEY=sk-ant-fallback-key
ANTHROPIC_MODEL=claude-sonnet-4-20250514

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

## 费用对比

以下是各服务商的大致价格（以输入 + 输出综合计算）：

### 国际服务商（美元/百万 Tokens）

| 模型 | 输入价格 | 输出价格 | 适用场景 |
|------|----------|----------|----------|
| GPT-4o | $2.50 | $10.00 | 高精度任务 |
| GPT-4o-mini | $0.15 | $0.60 | 日常使用 |
| Claude-Sonnet | $3.00 | $15.00 | 复杂分析 |
| Claude-Haiku | $0.80 | $4.00 | 快速响应 |

### 国内服务商（人民币/百万 Tokens）

| 模型 | 输入价格 | 输出价格 | 适用场景 |
|------|----------|----------|----------|
| 文心 4.0 | ¥8.00 | ¥8.00 | 通用任务 |
| 文心 Turbo | ¥4.00 | ¥4.00 | 日常对话 |
| 通义 Max | ¥12.00 | ¥12.00 | 专业场景 |
| 通义 Plus | ¥4.00 | ¥4.00 | 性价比之选 |

### 成本估算示例

假设每天使用 10 万 Tokens（约 50 次对话）：

- **GPT-4o-mini**：约 $0.075/天 ≈ ¥0.54/天
- **文心 Turbo**：约 ¥0.40/天
- **通义 Plus**：约 ¥0.40/天

> 💡 **省钱技巧**：简单任务用国内 API，复杂任务切换到国际 API，综合成本可降低 60% 以上。

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
