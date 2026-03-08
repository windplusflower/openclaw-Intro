# macOS 安装 OpenClaw

> 在 Mac 上安装 OpenClaw

---

## 📋 系统要求

| 要求 | 说明 |
|------|------|
| **系统** | macOS 10.15 (Catalina) 或更高 |
| **包管理器** | Homebrew（推荐） |
| **网络** | 能访问 GitHub 和 AI 服务 API |
| **权限** | 需要管理员权限安装 |

---

## 🚀 官方推荐安装方法：Onboard 安装

OpenClaw 提供官方 `onboard` 命令，安装后让 AI 帮你完成所有配置！

### 步骤 1：安装 Homebrew（如果未安装）

```bash
# 检查是否已安装 Homebrew
brew --version

# 如果提示找不到命令，需要安装 Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 安装完成后，添加 Homebrew 到 PATH（M1/M2/M3 Mac）
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

# 或者 Intel Mac
echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/usr/local/bin/brew shellenv)"
```

### 步骤 2：安装 OpenClaw

```bash
# 安装 OpenClaw
brew install openclaw

# 验证安装
openclaw version
```

### 步骤 3：运行 Onboard 向导（推荐！）

```bash
# 启动配置向导
openclaw onboard
```

这个向导会：
- ✅ 检测你的系统环境
- ✅ 引导你配置 API Key
- ✅ 测试连接是否正常
- ✅ 完成基础设置

---

## 💬 让 AI 帮你完成配置（不要手动改！）

安装完成后，**不要手动编辑配置文件**！直接告诉 OpenClaw 你想要什么：

### 示例 1：配置百炼 API

```
你：帮我配置百炼 API
AI：好的，请提供你的百炼 API Key（从 https://bailian.console.aliyun.com 获取）
你：sk-xxxxxxxxxxxxxxxx
AI：已配置百炼 API，正在测试连接... 连接成功！
```

### 示例 2：配置上下文压缩

```
你：帮我设置上下文压缩
AI：已为你启用上下文压缩功能。当对话超过 4000 tokens 时会自动压缩历史记录。
```

### 示例 3：配置多个 API

```
你：我想同时配置 OpenAI 和百炼
AI：好的，请依次提供两个 API Key...
```

### 示例 4：配置 Discord 机器人

```
你：帮我配置 Discord 机器人
AI：请提供你的 Discord Bot Token...
```

> 💡 **核心理念**：让 AI 帮你做，不要手动改配置文件！

---

## 📥 备选：一键脚本安装

如果你更喜欢脚本安装：

```bash
# 下载安装脚本并执行
curl -fsSL https://openclaw.ai/install | bash

# 按照提示完成安装
# 然后运行 onboard 向导
openclaw onboard
```

---

## 🎯 开始使用 OpenClaw

安装完成后，你有两种方式与 OpenClaw 对话：

### 方式一：使用 TUI（终端界面）

```bash
# 启动终端对话界面
openclaw tui

# 然后直接输入你的问题
你好
```

### 方式二：使用 Web Dashboard（推荐）

1. 打开浏览器访问：`http://localhost:3000`（或你的配置地址）
2. 在 Dashboard 中直接与 AI 对话
3. 可以查看会话历史、Token 消耗等

### 测试对话

无论使用哪种方式，都可以直接输入：

```
你好，帮我配置一下 API
```

AI 会引导你完成后续配置。

---

## 🔍 问题排查

### 问题 1：brew 命令找不到

```bash
# 解决方案：安装 Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 问题 2：openclaw 命令找不到

```bash
# 解决方案：检查 PATH
echo $PATH

# 添加 Homebrew 到 PATH（M1/M2/M3 Mac）
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
source ~/.zprofile

# Intel Mac
echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zprofile
source ~/.zprofile
```

### 问题 3：权限错误

```bash
# 解决方案：修复权限
sudo chown -R $(whoami) /opt/homebrew
```

### 问题 4：网络连接失败

```bash
# 检查网络连接
ping github.com

# 如果使用代理，配置代理
export https_proxy=http://127.0.0.1:7890
export http_proxy=http://127.0.0.1:7890
```

### 问题 5：onboard 向导无法启动

```bash
# 手动启动配置
openclaw config --wizard

# 或者启动 TUI 后告诉 AI 你的问题
openclaw tui
# 然后输入："帮我检查配置"
```

---

## 📝 实践示例

### 示例 1：完成安装和配置

```bash
# 1. 安装 Homebrew（如果需要）
brew --version

# 2. 安装 OpenClaw
brew install openclaw

# 3. 运行 onboard 向导
openclaw onboard

# 4. 根据向导提示，输入你的 API Key

# 5. 启动终端对话界面
openclaw tui

# 6. 测试对话
你好
```

### 示例 2：让 AI 帮你配置百炼 API

```bash
# 启动终端对话界面
openclaw tui

# 然后直接说：
帮我配置百炼 API，我的 Key 是 sk-xxxxxxxx
```

### 示例 3：让 AI 帮你设置上下文压缩

```bash
# 启动终端对话界面
openclaw tui

# 然后直接说：
帮我开启上下文压缩功能
```

---

## 💡 实用技巧

### 技巧 1：快速启动

```bash
# 添加别名到 ~/.zshrc
echo 'alias oc="openclaw"' >> ~/.zshrc
source ~/.zshrc

# 现在可以用 oc 命令快速启动
oc
```

### 技巧 2：查看日志

```bash
# 查看 OpenClaw 日志
tail -f ~/.openclaw/logs/openclaw.log
```

### 技巧 3：更新 OpenClaw

```bash
# 更新 OpenClaw
brew update
brew upgrade openclaw

# 查看版本
openclaw version
```

### 技巧 4：让 AI 帮你排查问题

```bash
# 如果遇到问题，启动 TUI 后问 AI
openclaw tui
# 然后输入："帮我检查配置是否正确"
```

---

## 📚 延伸阅读

- [Windows 安装](./03-install-windows.md) - Windows 用户看这里
- [会话管理](./04-session-management.md) - 学习管理会话
- [API 配置指南](../03-reference/api-setup.md) - 了解 API 配置详情

---

## ✅ 本节要点

**你学到了**：

- ✅ macOS 系统要求
- ✅ 使用 Homebrew 安装 OpenClaw
- ✅ 使用 `openclaw onboard` 向导完成配置
- ✅ **核心理念：让 AI 帮你配置，不要手动改文件**
- ✅ 常用配置对话示例
- ✅ 问题排查方法

**核心理念**：

```
❌ 不要这样做：
- 手动编辑 ~/.openclaw/config.json
- 手动修改 .env 文件
- 查阅文档找配置参数

✅ 应该这样做：
- 直接告诉 AI："帮我配置百炼 API"
- 直接告诉 AI："帮我设置上下文压缩"
- 让 AI 帮你完成所有配置
```

**下一节**：[Windows 安装](./03-install-windows.md)
