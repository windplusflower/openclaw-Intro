# Windows 安装 OpenClaw

> 在 Windows 上安装 OpenClaw

---

## 📋 系统要求

| 要求 | 说明 |
|------|------|
| **系统** | Windows 10 或更高 |
| **包管理器** | Winget（推荐）或 Scoop |
| **网络** | 能访问 GitHub 和 AI 服务 API |
| **权限** | 需要管理员权限安装 |

---

## 🚀 官方推荐安装方法：Onboard 安装

OpenClaw 提供官方 `onboard` 命令，安装后让 AI 帮你完成所有配置！

### 步骤 1：检查 Winget 是否可用

```powershell
# 检查 Winget 版本
winget --version

# 如果提示找不到命令，需要安装 Winget
# 1. 打开 Microsoft Store
# 2. 搜索 "App Installer"
# 3. 点击安装
# 或者从 GitHub 下载：https://github.com/microsoft/winget-cli/releases
```

### 步骤 2：安装 OpenClaw

```powershell
# 以管理员身份运行 PowerShell（右键 → 以管理员身份运行）

# 安装 OpenClaw
winget install openclaw

# 验证安装
openclaw version
```

### 步骤 3：运行 Onboard 向导（推荐！）

```powershell
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

## 📥 方法二：Scoop 安装

如果你更喜欢 Scoop：

### 步骤 1：安装 Scoop（如果未安装）

```powershell
# 以管理员身份运行 PowerShell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression

# 验证安装
scoop --version
```

### 步骤 2：安装 OpenClaw

```powershell
# 安装 OpenClaw
scoop install openclaw

# 验证安装
openclaw version

# 运行 onboard 向导
openclaw onboard
```

---

## 🎯 初次启动

### 启动 OpenClaw

```powershell
# 启动 OpenClaw
openclaw

# 你应该看到类似输出：
# 🦞 OpenClaw 已启动
# 请输入你的命令：
```

### 测试对话

```powershell
# 在 OpenClaw 中输入
你好

# AI 应该回复
你好！有什么我可以帮助你的吗？
```

---

## 🔍 问题排查

### 问题 1：winget 命令找不到

```powershell
# 解决方案：安装 Winget
# 1. 打开 Microsoft Store
# 2. 搜索 "App Installer"
# 3. 点击安装
```

### 问题 2：openclaw 命令找不到

```powershell
# 解决方案：检查 PATH
echo $env:PATH

# 手动添加 OpenClaw 到 PATH（临时）
$env:PATH += ";C:\Program Files\OpenClaw"

# 永久添加（推荐）
[Environment]::SetEnvironmentVariable("Path", $env:PATH + ";C:\Program Files\OpenClaw", "User")
```

### 问题 3：权限错误

```powershell
# 解决方案：以管理员身份运行 PowerShell
# 右键点击 PowerShell → 以管理员身份运行
```

### 问题 4：网络连接失败

```powershell
# 检查网络连接
ping github.com

# 如果使用代理，配置代理（临时）
$env:HTTPS_PROXY="http://127.0.0.1:7890"
$env:HTTP_PROXY="http://127.0.0.1:7890"

# 永久配置代理
[Environment]::SetEnvironmentVariable("HTTPS_PROXY", "http://127.0.0.1:7890", "User")
[Environment]::SetEnvironmentVariable("HTTP_PROXY", "http://127.0.0.1:7890", "User")
```

### 问题 5：onboard 向导无法启动

```powershell
# 手动启动配置
openclaw config --wizard

# 或者直接告诉 AI 你的问题
openclaw
# 然后输入："帮我检查配置"
```

---

## 📝 实践示例

### 示例 1：完成安装和配置

```powershell
# 1. 检查 Winget
winget --version

# 2. 安装 OpenClaw（管理员权限）
winget install openclaw

# 3. 运行 onboard 向导
openclaw onboard

# 4. 根据向导提示，输入你的 API Key

# 5. 启动 OpenClaw
openclaw

# 6. 测试对话
你好
```

### 示例 2：让 AI 帮你配置百炼 API

```powershell
# 启动 OpenClaw
openclaw

# 然后直接说：
帮我配置百炼 API，我的 Key 是 sk-xxxxxxxx
```

### 示例 3：让 AI 帮你设置上下文压缩

```powershell
# 启动 OpenClaw
openclaw

# 然后直接说：
帮我开启上下文压缩功能
```

---

## 💡 实用技巧

### 技巧 1：创建桌面快捷方式

```powershell
# 创建快捷方式
$WshShell = New-Object -comObject WScript.Shell
$Shortcut = $WshShell.CreateShortcut("$Home\Desktop\OpenClaw.lnk")
$Shortcut.TargetPath = "C:\Program Files\OpenClaw\openclaw.exe"
$Shortcut.Save()
```

### 技巧 2：查看日志

```powershell
# 查看 OpenClaw 日志（实时）
Get-Content $HOME\.openclaw\logs\openclaw.log -Tail 50 -Wait

# 或者使用记事本打开
notepad $HOME\.openclaw\logs\openclaw.log
```

### 技巧 3：更新 OpenClaw

```powershell
# 更新 OpenClaw
winget upgrade openclaw

# 查看版本
openclaw version
```

### 技巧 4：让 AI 帮你排查问题

```powershell
# 如果遇到问题，直接问 AI
openclaw
# 然后输入："帮我检查配置是否正确"
```

---

## 📚 延伸阅读

- [macOS 安装](./02-install-macos.md) - Mac 用户看这里
- [会话管理](./04-session-management.md) - 学习管理会话
- [API 配置指南](../03-reference/api-setup.md) - 了解 API 配置详情

---

## ✅ 本节要点

**你学到了**：

- ✅ Windows 系统要求
- ✅ 使用 Winget 安装 OpenClaw
- ✅ 使用 Scoop 安装 OpenClaw
- ✅ 使用 `openclaw onboard` 向导完成配置
- ✅ **核心理念：让 AI 帮你配置，不要手动改文件**
- ✅ 常用配置对话示例
- ✅ 问题排查方法

**核心理念**：

```
❌ 不要这样做：
- 手动编辑 config.json
- 手动修改 .env 文件
- 查阅文档找配置参数

✅ 应该这样做：
- 直接告诉 AI："帮我配置百炼 API"
- 直接告诉 AI："帮我设置上下文压缩"
- 让 AI 帮你完成所有配置
```

**下一节**：[会话管理](./04-session-management.md)
