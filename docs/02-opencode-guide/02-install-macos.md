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

## 🔧 方法一：Homebrew 安装（推荐）

### 步骤 1：安装 Homebrew（如果未安装）

```bash
# 检查是否已安装 Homebrew
brew --version

# 如果提示找不到命令，需要安装 Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 安装完成后，添加 Homebrew 到 PATH
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

### 步骤 2：安装 OpenClaw

```bash
# 安装 OpenClaw
brew install opencode

# 验证安装
opencode version
```

### 步骤 3：配置 API Key

```bash
# 创建配置目录
mkdir -p ~/.openclaw

# 创建配置文件
cat > ~/.openclaw/config.json << EOF
{
  "api_key": "你的 API Key"
}
EOF

# 验证配置
opencode version
```

---

## 📥 方法二：一键脚本安装

### 运行安装脚本

```bash
# 下载安装脚本并执行
curl -fsSL https://opencode.ai/install | bash

# 按照提示完成安装
```

### 验证安装

```bash
# 检查版本
opencode version

# 查看帮助
opencode --help
```

---

## 🎯 初次启动

### 启动 OpenClaw

```bash
# 启动 OpenClaw
opencode

# 你应该看到类似输出：
# 🦞 OpenClaw 已启动
# 请输入你的命令：
```

### 测试对话

```bash
# 在 OpenClaw 中输入
你好

# AI 应该回复
你好！有什么我可以帮助你的吗？
```

---

## ⚙️ 配置渠道

### 配置 Discord（可选）

```bash
# 编辑配置文件
nano ~/.openclaw/config.json

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
opencode restart
```

### 配置飞书（可选）

```bash
# 编辑配置文件
nano ~/.openclaw/config.json

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
opencode restart
```

---

## 🔍 问题排查

### 问题 1：brew 命令找不到

```bash
# 解决方案：安装 Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 问题 2：opencode 命令找不到

```bash
# 解决方案：检查 PATH
echo $PATH

# 添加 Homebrew 到 PATH
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
source ~/.zprofile
```

### 问题 3：权限错误

```bash
# 解决方案：使用 sudo（谨慎）
sudo brew install opencode

# 或者修复权限
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

---

## 📝 实践示例

### 示例 1：完成安装

```bash
# 1. 安装 Homebrew（如果需要）
brew --version

# 2. 安装 OpenClaw
brew install opencode

# 3. 验证安装
opencode version

# 4. 启动 OpenClaw
opencode

# 5. 测试对话
你好
```

### 示例 2：配置 API Key

```bash
# 1. 创建配置目录
mkdir -p ~/.openclaw

# 2. 创建配置文件
cat > ~/.openclaw/config.json << EOF
{
  "api_key": "你的 API Key"
}
EOF

# 3. 验证配置
cat ~/.openclaw/config.json
```

### 示例 3：配置渠道

```bash
# 1. 编辑配置文件
nano ~/.openclaw/config.json

# 2. 添加渠道配置（可选）

# 3. 重启 OpenClaw
opencode restart
```

---

## 💡 实用技巧

### 技巧 1：快速启动

```bash
# 添加别名到 ~/.zshrc
echo 'alias oc="opencode"' >> ~/.zshrc
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
brew upgrade opencode

# 查看版本
opencode version
```

---

## 📚 延伸阅读

- [Windows 安装](03-install-windows.md) - Windows 用户看这里
- [会话管理](04-session-management.md) - 学习管理会话

---

## ✅ 本节要点

**你学到了**：

- ✅ macOS 系统要求
- ✅ Homebrew 安装方法
- ✅ 一键脚本安装方法
- ✅ 配置 API Key
- ✅ 配置渠道
- ✅ 问题排查方法

**下一节**：[Windows 安装](03-install-windows.md)
