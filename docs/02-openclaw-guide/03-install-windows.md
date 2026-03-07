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

## 🔧 方法一：Winget 安装（推荐）

### 步骤 1：检查 Winget 是否可用

```powershell
# 检查 Winget 版本
winget --version

# 如果提示找不到命令，需要安装 Winget
# 访问 Microsoft Store 搜索"App Installer"
# 或者从 GitHub 下载：https://github.com/microsoft/winget-cli/releases
```

### 步骤 2：安装 OpenClaw

```powershell
# 安装 OpenClaw
winget install openclaw

# 验证安装
openclaw version
```

### 步骤 3：配置 API Key

```powershell
# 创建配置目录
mkdir $HOME\.openclaw

# 创建配置文件
@{
    api_key = "你的 API Key"
} | ConvertTo-Json | Out-File -Encoding UTF8 $HOME\.openclaw\config.json

# 验证配置
cat $HOME\.openclaw\config.json
```

---

## 📥 方法二：Scoop 安装

### 步骤 1：安装 Scoop（如果未安装）

```powershell
# 安装 Scoop
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
```

---

## 📥 方法三：手动安装

### 步骤 1：下载安装包

```powershell
# 访问 GitHub Releases
# https://github.com/openclaw-ai/openclaw/releases

# 下载最新的 Windows 安装包
# 通常是 openclaw-windows-x64.zip
```

### 步骤 2：解压并配置

```powershell
# 1. 解压到 C:\Program Files\OpenClaw
# 2. 添加到系统 PATH

# 创建配置目录
mkdir $HOME\.openclaw

# 创建配置文件
@{
    api_key = "你的 API Key"
} | ConvertTo-Json | Out-File -Encoding UTF8 $HOME\.openclaw\config.json
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

## ⚙️ 配置渠道

### 配置 Discord（可选）

```powershell
# 编辑配置文件
notepad $HOME\.openclaw\config.json

# 添加 Discord 配置
{
  "api_key": "你的 API Key",
  "channels": {
    "discord": {
      "token": "你的 Discord Bot Token"
    }
  }
}

# 重启 OpenClaw
openclaw restart
```

### 配置飞书（可选）

```powershell
# 编辑配置文件
notepad $HOME\.openclaw\config.json

# 添加飞书配置
{
  "api_key": "你的 API Key",
  "channels": {
    "feishu": {
      "app_id": "你的飞书 App ID",
      "app_secret": "你的飞书 App Secret"
    }
  }
}

# 重启 OpenClaw
openclaw restart
```

---

## 🔍 问题排查

### 问题 1：winget 命令找不到

```powershell
# 解决方案：安装 Winget
# 1. 打开 Microsoft Store
# 2. 搜索"App Installer"
# 3. 点击安装
```

### 问题 2：openclaw 命令找不到

```powershell
# 解决方案：检查 PATH
echo $env:PATH

# 手动添加 OpenClaw 到 PATH
$env:PATH += ";C:\Program Files\OpenClaw"
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

# 如果使用代理，配置代理
$env:HTTPS_PROXY="http://127.0.0.1:7890"
$env:HTTP_PROXY="http://127.0.0.1:7890"
```

---

## 📝 实践示例

### 示例 1：完成安装

```powershell
# 1. 检查 Winget
winget --version

# 2. 安装 OpenClaw
winget install openclaw

# 3. 验证安装
openclaw version

# 4. 启动 OpenClaw
openclaw

# 5. 测试对话
你好
```

### 示例 2：配置 API Key

```powershell
# 1. 创建配置目录
mkdir $HOME\.openclaw

# 2. 创建配置文件
@{
    api_key = "你的 API Key"
} | ConvertTo-Json | Out-File -Encoding UTF8 $HOME\.openclaw\config.json

# 3. 验证配置
cat $HOME\.openclaw\config.json
```

### 示例 3：配置渠道

```powershell
# 1. 编辑配置文件
notepad $HOME\.openclaw\config.json

# 2. 添加渠道配置（可选）

# 3. 重启 OpenClaw
openclaw restart
```

---

## 💡 实用技巧

### 技巧 1：快速启动

```powershell
# 创建快捷方式
$WshShell = New-Object -comObject WScript.Shell
$Shortcut = $WshShell.CreateShortcut("$Home\Desktop\OpenClaw.lnk")
$Shortcut.TargetPath = "C:\Program Files\OpenClaw\openclaw.exe"
$Shortcut.Save()
```

### 技巧 2：查看日志

```powershell
# 查看 OpenClaw 日志
Get-Content $HOME\.openclaw\logs\openclaw.log -Tail 50 -Wait
```

### 技巧 3：更新 OpenClaw

```powershell
# 更新 OpenClaw
winget upgrade openclaw

# 查看版本
openclaw version
```

---

## 📚 延伸阅读

- [macOS 安装](02-install-macos.md) - Mac 用户看这里
- [会话管理](04-session-management.md) - 了解会话管理

---

## ✅ 本节要点

**你学到了**：

- ✅ Windows 系统要求
- ✅ Winget 安装方法
- ✅ Scoop 安装方法
- ✅ 手动安装方法
- ✅ 配置 API Key
- ✅ 配置渠道
- ✅ 问题排查方法

**下一节**：[会话管理](04-session-management.md)
