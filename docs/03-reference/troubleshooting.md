# 问题排查指南

在使用 OpenClaw 过程中，遇到问题时不要慌张。本指南将帮助你系统性地定位和解决问题。

## 排查流程

遵循以下四步排查流程，大多数问题都能得到解决：

### 1. 查看日志

日志是排查问题的第一手资料。OpenClaw 的日志记录了系统运行的详细信息。

**查看实时日志：**
```bash
# 查看最近的日志
tail -f ~/.openclaw/logs/openclaw.log

# 查看特定级别的日志
tail -f ~/.openclaw/logs/openclaw.log | grep -i "error"
```

**查看历史日志：**
```bash
# 查看今天的日志
cat ~/.openclaw/logs/openclaw-$(date +%Y-%m-%d).log

# 搜索特定错误
grep -n "connection failed" ~/.openclaw/logs/*.log
```

**关键日志信息：**
- `ERROR` - 严重错误，需要立即处理
- `WARN` - 警告信息，可能影响功能
- `INFO` - 一般运行信息
- `DEBUG` - 调试信息，用于深入排查

### 2. 检查配置

配置错误是最常见的问题来源。

**检查配置文件：**
```bash
# 查看主配置文件
cat ~/.openclaw/config.yaml

# 验证配置语法
openclaw config validate
```

**常见配置检查点：**
- API Key 是否正确填写
- 渠道连接参数是否完整
- 文件路径是否存在
- 端口是否被占用

### 3. 测试连接

验证各个组件的连接状态。

**测试命令：**
```bash
# 检查网关状态
openclaw gateway status

# 测试渠道连接
openclaw channels test

# 检查技能加载
openclaw skills list
```

**网络连接测试：**
```bash
# 测试 API 连通性
curl -I https://api.example.com

# 检查端口占用
netstat -tlnp | grep <端口号>
```

### 4. 寻求帮助

如果以上步骤无法解决问题：

1. 整理错误日志和配置信息（脱敏后）
2. 查看官方文档和常见问题
3. 在社区或 Issue 中提问
4. 提供复现步骤和环境信息

---

## 常见问题及解决

### 安装问题

#### 问题 1：安装脚本执行失败

**现象：** 运行安装脚本时出现权限错误或命令未找到

**可能原因：**
- 缺少执行权限
- 系统缺少必要依赖
- 网络问题导致下载失败

**解决方案：**
```bash
# 添加执行权限
chmod +x install.sh

# 使用 sudo 运行
sudo ./install.sh

# 检查依赖
which node python3 git

# 手动安装依赖
apt-get update && apt-get install -y nodejs python3 git
```

#### 问题 2：Node.js 版本不兼容

**现象：** 启动时报错 "Unsupported Node.js version"

**可能原因：** OpenClaw 需要特定版本的 Node.js

**解决方案：**
```bash
# 查看当前版本
node --version

# 使用 nvm 安装合适版本
nvm install 22
nvm use 22

# 或下载指定版本
wget https://nodejs.org/dist/v22.22.0/node-v22.22.0-linux-x64.tar.xz
```

#### 问题 3：依赖安装失败

**现象：** `npm install` 或 `pnpm install` 失败

**可能原因：**
- 网络问题（特别是国内访问 npm 仓库）
- 权限问题
- 磁盘空间不足

**解决方案：**
```bash
# 使用国内镜像
npm config set registry https://registry.npmmirror.com

# 清理缓存后重试
npm cache clean --force
npm install

# 检查磁盘空间
df -h

# 使用 pnpm（更节省空间）
npm install -g pnpm
pnpm install
```

---

### 配置问题

#### 问题 1：配置文件格式错误

**现象：** 启动时报 YAML 解析错误

**可能原因：**
- 缩进不正确
- 缺少冒号或引号
- 使用了制表符而非空格

**解决方案：**
```bash
# 使用在线 YAML 验证器
# 或使用 yq 工具验证
yq eval '.' ~/.openclaw/config.yaml

# 常见错误示例及修正
# 错误：
api_key: abc123
channels:
- type: discord
  token: xyz

# 正确：
api_key: "abc123"
channels:
  - type: discord
    token: "xyz"
```

#### 问题 2：API Key 无效

**现象：** 调用 API 时返回 401/403 错误

**可能原因：**
- Key 填写错误
- Key 已过期或被撤销
- Key 权限不足

**解决方案：**
1. 重新生成 API Key
2. 检查 Key 的权限范围
3. 确认 Key 未过期
4. 在配置文件中正确填写（注意引号）

#### 问题 3：路径配置错误

**现象：** 文件操作失败，提示路径不存在

**可能原因：**
- 使用了相对路径但工作目录不对
- 路径中包含特殊字符
- 目录权限不足

**解决方案：**
```bash
# 使用绝对路径
workspace: "/home/windflower/.openclaw/workspace"

# 检查路径是否存在
ls -la /home/windflower/.openclaw/workspace

# 创建缺失的目录
mkdir -p /home/windflower/.openclaw/workspace

# 检查权限
chmod 755 /home/windflower/.openclaw
```

---

### 渠道问题

#### 问题 1：Discord 连接失败

**现象：** 无法连接到 Discord，日志显示认证失败

**可能原因：**
- Bot Token 错误
- Bot 未邀请到服务器
- 缺少必要的权限

**解决方案：**
```bash
# 验证 Token 格式
# Discord Token 应以 "MT" 或 "N" 开头

# 检查 Bot 权限
# 需要：发送消息、读取消息、嵌入链接等

# 重新邀请 Bot
# 使用 OAuth2 URL 生成器，选择正确的权限

# 测试连接
openclaw channels test discord
```

#### 问题 2：消息发送失败

**现象：** 可以连接但无法发送消息

**可能原因：**
- 频道 ID 错误
- Bot 在该频道没有权限
- 消息内容违反平台规则

**解决方案：**
1. 确认频道 ID 正确（右键复制 ID，需开启开发者模式）
2. 检查 Bot 角色权限
3. 检查消息长度和内容限制
4. 查看日志中的具体错误信息

#### 问题 3：WebSocket 频繁断开

**现象：** 连接不断断开重连

**可能原因：**
- 网络不稳定
- 防火墙/代理干扰
- 服务端限制

**解决方案：**
```bash
# 检查网络连接
ping -c 4 discord.com

# 检查防火墙
sudo ufw status

# 配置重试参数
gateway:
  reconnect_interval: 5000
  max_reconnect_attempts: 10

# 使用稳定的网络环境
```

---

### 技能问题

#### 问题 1：技能加载失败

**现象：** 启动时提示技能加载错误

**可能原因：**
- 技能目录结构不正确
- 缺少 SKILL.md 文件
- 依赖未安装

**解决方案：**
```bash
# 检查技能目录结构
ls -la ~/.openclaw/workspace/skills/<skill-name>/

# 确保有 SKILL.md
cat ~/.openclaw/workspace/skills/<skill-name>/SKILL.md

# 安装技能依赖
cd ~/.openclaw/workspace/skills/<skill-name>/
npm install

# 重新加载技能
openclaw skills reload
```

#### 问题 2：技能执行超时

**现象：** 技能执行时间过长被强制终止

**可能原因：**
- 技能逻辑复杂
- 外部 API 响应慢
- 死循环

**解决方案：**
```yaml
# 调整超时配置
skills:
  default_timeout: 60000  # 60 秒
  max_timeout: 300000     # 

# 优化技能代码
# 添加进度日志
# 使用异步操作
```

#### 问题 3：技能权限不足

**现象：** 技能无法访问某些资源

**可能原因：**
- 安全策略限制
- 文件权限问题
- 缺少必要配置

**解决方案：**
```bash
# 检查安全配置
cat ~/.openclaw/security.yaml

# 调整权限（谨慎操作）
# 在安全范围内授予必要权限

# 检查文件权限
chmod 644 ~/.openclaw/workspace/skills/<skill-name>/*
```

---

## 日志分析

### 日志位置

```
~/.openclaw/logs/
├── openclaw.log              # 主日志
├── openclaw-2026-03-06.log   # 按日期分割的日志
├── gateway.log               # 网关日志
└── skills.log                # 技能日志
```

### 日志级别说明

| 级别 | 说明 | 处理建议 |
|------|------|----------|
| ERROR | 严重错误 | 立即处理，系统可能无法正常运行 |
| WARN | 警告 | 关注并适时处理，可能影响部分功能 |
| INFO | 信息 | 正常记录，用于了解系统状态 |
| DEBUG | 调试 | 开发时使用，排查详细问题 |

### 常见错误模式

**连接错误：**
```
ERROR [gateway] Connection failed: ECONNREFUSED
→ 检查目标服务是否运行
→ 检查防火墙设置
→ 验证连接参数
```

**认证错误：**
```
ERROR [discord] Authentication failed: 401 Unauthorized
→ 检查 Token 是否正确
→ 检查 Token 是否过期
→ 重新生成凭证
```

**资源错误：**
```
ERROR [fs] ENOENT: no such file or directory
→ 检查路径是否正确
→ 创建缺失的目录
→ 检查权限设置
```

### 日志分析技巧

```bash
# 统计错误数量
grep -c "ERROR" ~/.openclaw/logs/*.log

# 查看错误时间分布
grep "ERROR" ~/.openclaw/logs/*.log | cut -d' ' -f1-2 | sort | uniq -c

# 提取特定组件的日志
grep "\[gateway\]" ~/.openclaw/logs/openclaw.log

# 实时过滤错误
tail -f ~/.openclaw/logs/openclaw.log | grep --line-buffered "ERROR\|WARN"
```

---

## 寻求帮助

### 自助资源

在提问之前，请先尝试以下资源：

1. **官方文档** - 最权威的信息来源
2. **常见问题 (FAQ)** - 高频问题的解答
3. **错误代码查询** - 根据错误代码查找解决方案
4. **社区讨论** - 其他用户的经验分享

### 提问的艺术

当需要寻求帮助时，请提供以下信息：

**必需信息：**
- OpenClaw 版本号
- 操作系统及版本
-  Node.js 版本
- 完整的错误信息（包含堆栈）
- 问题复现步骤

**可选信息：**
- 相关配置文件（脱敏后）
- 日志片段
- 已尝试的解决方案
- 环境截图

**提问模板：**
```markdown
## 问题描述
[简要描述遇到的问题]

## 环境信息
- OpenClaw 版本：x.x.x
- 操作系统：Ubuntu 24.04
- Node.js 版本：v22.22.0

## 错误信息
```
[粘贴完整的错误日志]
```

## 复现步骤
1. ...
2. ...
3. ...

## 已尝试的解决方案
- [ ] 重启服务
- [ ] 检查配置
- [ ] 更新依赖
```

### 联系渠道

- **GitHub Issues** - 报告 Bug 和功能请求
- **Discord 社区** - 实时交流和快速问答
- **邮件列表** - 正式的技术讨论
- **文档评论区** - 针对特定文档的疑问

### 等待回复期间

在等待帮助时，你可以：

1. 尝试回退到稳定版本
2. 使用备用方案绕过问题
3. 继续收集更多信息
4. 记录详细的排查过程

---

## 附录：快速检查清单

遇到问题时，按此清单逐项检查：

- [ ] 查看最新日志，记录错误信息
- [ ] 确认配置文件语法正确
- [ ] 验证所有 API Key 和凭证
- [ ] 检查网络连接状态
- [ ] 确认必要服务正在运行
- [ ] 检查磁盘空间和内存
- [ ] 验证文件权限设置
- [ ] 尝试重启服务
- [ ] 查看是否有已知问题
- [ ] 准备提问所需信息

---

*最后更新：2026-03-06*
*本文档会随 OpenClaw 更新而维护，请确保查看最新版本*
