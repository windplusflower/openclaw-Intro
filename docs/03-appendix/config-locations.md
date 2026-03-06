# 配置文件位置

本文档提供 OpenClaw 配置文件、日志、技能和会话数据的完整位置参考，支持 macOS 和 Windows 双平台快速查阅。

---

## 配置文件目录

OpenClaw 的所有用户级配置和数据存储在用户主目录下的 `.openclaw/` 文件夹中。

| 系统 | 配置目录 | 完整路径示例 |
|------|---------|-------------|
| macOS | `~/.openclaw/` | `/Users/yourname/.openclaw/` |
| Windows | `C:\Users\用户名\.openclaw\` | `C:\Users\Windflower\.openclaw\` |
| Linux | `~/.openclaw/` | `/home/yourname/.openclaw/` |

> 💡 **提示**：`.` 开头的文件夹在 macOS/Linux 上默认隐藏，使用 `ls -la` 或在 Finder 中按 `Cmd+Shift+.` 显示。

---

## 主要配置文件

### config.json - 主配置文件

**位置**：`~/.openclaw/config.json`

**用途**：存储 OpenClaw 核心配置，包括：
- 默认模型设置
- API 密钥配置
- 全局行为选项
- 会话超时设置

**示例结构**：
```json
{
  "default_model": "qwen3.5-plus",
  "thinking": "off",
  "shell": "bash",
  "timezone": "Asia/Shanghai"
}
```

---

### channels.json - 渠道配置

**位置**：`~/.openclaw/channels.json`

**用途**：定义消息渠道连接信息，包括：
- Discord 服务器和频道 ID
- Feishu 应用配置
- 其他消息平台凭证

**示例结构**：
```json
{
  "discord": {
    "guild_id": "123456789",
    "channels": ["channel-id-1", "channel-id-2"]
  },
  "feishu": {
    "app_id": "cli_xxx",
    "app_secret": "xxx"
  }
}
```

---

### skills.json - 技能配置

**位置**：`~/.openclaw/skills.json`

**用途**：管理已安装技能的启用状态和配置：
- 技能启用/禁用开关
- 技能特定参数
- 自定义技能路径

**示例结构**：
```json
{
  "enabled": ["weather", "github", "feishu-doc"],
  "disabled": ["legacy-skill"],
  "custom_paths": ["/path/to/custom/skills"]
}
```

---

## 日志文件位置

### 会话日志

**位置**：`~/.openclaw/logs/`

**文件命名**：`session-YYYY-MM-DD.log`

**用途**：记录每次会话的详细执行日志，包括：
- 工具调用记录
- 错误和警告信息
- 性能指标

**查看日志**：
```bash
# macOS/Linux
tail -f ~/.openclaw/logs/session-$(date +%Y-%m-%d).log

# Windows (PowerShell)
Get-Content ~/.openclaw/logs/session-$(Get-Date -Format yyyy-MM-dd).log -Tail 50 -Wait
```

### 错误日志

**位置**：`~/.openclaw/logs/error.log`

**用途**：集中记录所有错误信息，便于排查问题。

---

## 技能文件位置

### 内置技能

**位置**：`~/.openclaw/workspace/skills/`

**结构**：
```
skills/
├── weather/
│   ├── SKILL.md
│   └── ...
├── github/
│   ├── SKILL.md
│   └── ...
└── feishu-doc/
    ├── SKILL.md
    └── ...
```

### 自定义技能

**位置**：可在 `skills.json` 中配置额外路径

**推荐位置**：
- macOS: `~/Documents/openclaw-skills/`
- Windows: `C:\Users\用户名\Documents\openclaw-skills\`

---

## 会话数据位置

### 记忆文件

**位置**：`~/.openclaw/workspace/memory/`

**文件命名**：`YYYY-MM-DD.md`

**用途**：存储每日会话记忆和上下文信息。

### 长期记忆

**位置**：`~/.openclaw/workspace/MEMORY.md`

**用途**： curated 长期记忆，跨会话持久化重要信息。

### 会话状态

**位置**：`~/.openclaw/workspace/memory/heartbeat-state.json`

**用途**：跟踪心跳检查状态和周期性任务进度。

---

## 备份和迁移

### 完整备份

**macOS/Linux**：
```bash
# 备份整个配置目录
tar -czf openclaw-backup-$(date +%Y%m%d).tar.gz ~/.openclaw/

# 或使用 rsync 增量备份
rsync -av ~/.openclaw/ /backup/location/openclaw/
```

**Windows (PowerShell)**：
```powershell
# 压缩备份
Compress-Archive -Path "$env:USERPROFILE\.openclaw" -DestinationPath "C:\Backup\openclaw-backup-$(Get-Date -Format yyyyMMdd).zip"

# 或使用 robocopy 增量备份
robocopy "%USERPROFILE%\.openclaw" "D:\Backup\openclaw" /MIR
```

### 迁移到新设备

1. **导出配置**：在旧设备上执行完整备份
2. **传输文件**：将备份文件复制到新设备
3. **恢复配置**：
   - macOS/Linux: `tar -xzf openclaw-backup.tar.gz -C ~/`
   - Windows: 解压到 `C:\Users\用户名\`
4. **验证路径**：检查所有路径是否适配新系统
5. **更新凭证**：如有必要，更新 API 密钥和渠道配置

### 跨平台同步注意事项

⚠️ **路径分隔符**：
- macOS/Linux 使用 `/`
- Windows 使用 `\`（或在 PowerShell 中用 `/`）

⚠️ **权限差异**：
- macOS/Linux 注意文件执行权限
- Windows 注意文件锁定和占用

⚠️ **环境变量**：
- macOS/Linux: `$HOME`, `~`
- Windows: `%USERPROFILE%`

---

## 快速参考表

| 内容类型 | 相对路径 | macOS 示例 | Windows 示例 |
|---------|---------|-----------|-------------|
| 主配置 | `~/.openclaw/config.json` | `/Users/windflower/.openclaw/config.json` | `C:\Users\windflower\.openclaw\config.json` |
| 日志目录 | `~/.openclaw/logs/` | `/Users/windflower/.openclaw/logs/` | `C:\Users\windflower\.openclaw\logs\` |
| 技能目录 | `~/.openclaw/workspace/skills/` | `/Users/windflower/.openclaw/workspace/skills/` | `C:\Users\windflower\.openclaw\workspace\skills\` |
| 记忆文件 | `~/.openclaw/workspace/memory/` | `/Users/windflower/.openclaw/workspace/memory/` | `C:\Users\windflower\.openclaw\workspace\memory\` |

---

## 常见问题

### Q: 找不到 `.openclaw` 文件夹？

**A**：该文件夹默认隐藏。
- macOS Finder: 按 `Cmd+Shift+.` 切换隐藏文件显示
- Windows 资源管理器: 查看 → 勾选"隐藏的项目"
- 终端：直接使用 `cd ~/.openclaw` 访问

### Q: 如何重置所有配置？

**A**：删除或重命名配置目录，OpenClaw 会在下次启动时重新创建：
```bash
# macOS/Linux
mv ~/.openclaw ~/.openclaw.backup

# Windows (PowerShell)
Rename-Item -Path "$env:USERPROFILE\.openclaw" -NewName ".openclaw.backup"
```

### Q: 配置文件损坏如何恢复？

**A**：
1. 从备份恢复（见备份和迁移章节）
2. 如无备份，删除损坏的配置文件，OpenClaw 会生成默认配置
3. 重新配置必要的 API 密钥和渠道信息

---

## 本节小结

- **配置目录**：所有配置存储在 `~/.openclaw/`，跨平台一致
- **核心文件**：`config.json`（主配置）、`channels.json`（渠道）、`skills.json`（技能）
- **日志位置**：`~/.openclaw/logs/`，按日期分文件存储
- **技能管理**：内置技能在 `workspace/skills/`，自定义技能可配置额外路径
- **会话数据**：记忆文件在 `workspace/memory/`，长期记忆在 `MEMORY.md`
- **备份建议**：定期备份整个 `.openclaw/` 目录，迁移时注意路径和权限差异

掌握配置文件位置是管理 OpenClaw 的基础。建议将本文档加入书签，需要时快速查阅。

---

*文档版本：1.0 | 最后更新：2026-03-06*
