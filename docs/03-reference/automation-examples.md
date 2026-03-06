# 自动化示例

本文档提供 OpenClaw 自动化任务的实用示例，所有代码均可直接复制使用。

---

## 定时任务示例

### 每日天气报告

使用 cron 定时获取天气并发送到指定频道。

#### 1. 创建天气报告脚本

```bash
#!/bin/bash
# ~/.openclaw/workspace/scripts/daily-weather.sh

LOCATION="Beijing"
CHANNEL="1473539459369799763"  # Discord channel ID

# 获取天气（使用 wttr.in）
WEATHER=$(curl -s "wttr.in/${LOCATION}?format=%c+%t+%w+%h")
DATE=$(date +"%Y-%m-%d %H:%M")

# 发送到 Discord
openclaw message send \
  --channel "$CHANNEL" \
  --text "🌤️ **每日天气报告**

📅 时间：${DATE}
📍 地点：${LOCATION}
🌡️ 天气：${WEATHER}

祝你有美好的一天！"
```

#### 2. 设置 cron 任务

```bash
# 编辑 crontab
crontab -e

# 添加每日早上 7:30 执行
30 7 * * * /home/windflower/.openclaw/workspace/scripts/daily-weather.sh
```

#### 3. 使用 OpenClaw 内置技能（推荐）

```bash
# 直接在 openclaw 命令中调用 weather 技能
openclaw run weather --location "Shanghai" --channel "1473539459369799763"
```

---

### 定时发送日报

每天固定时间发送工作总结或提醒。

#### 1. 创建日报脚本

```bash
#!/bin/bash
# ~/.openclaw/workspace/scripts/daily-report.sh

CHANNEL="1473539459369799763"
DATE=$(date +"%Y-%m-%d")
DAY_OF_WEEK=$(date +"%A")

# 构建日报内容
cat << EOF | openclaw message send --channel "$CHANNEL" --text "$(cat)"
📋 **${DAY_OF_WEEK} 工作日报**

📅 日期：${DATE}

---

**今日完成：**
- [ ] 任务 1
- [ ] 任务 2
- [ ] 任务 3

**明日计划：**
- [ ] 计划 1
- [ ] 计划 2

**遇到的问题：**
- 无

---
_请在下班前填写完成情况_
EOF
```

#### 2. 设置定时发送

```bash
# 工作日早上 9:00 发送
0 9 * * 1-5 /home/windflower/.openclaw/workspace/scripts/daily-report.sh

# 或工作日晚上 18:00 提醒填写
0 18 * * 1-5 openclaw message send \
  --channel "1473539459369799763" \
  --text "⏰ 提醒：请填写今日工作日报"
```

---

### 定时备份

定期备份重要文件到云存储或本地备份目录。

#### 1. 创建工作区备份脚本

```bash
#!/bin/bash
# ~/.openclaw/workspace/scripts/backup-workspace.sh

WORKSPACE="/home/windflower/.openclaw/workspace"
BACKUP_DIR="/home/windflower/backups"
DATE=$(date +"%Y%m%d_%H%M%S")
BACKUP_FILE="${BACKUP_DIR}/workspace_backup_${DATE}.tar.gz"

# 创建备份目录
mkdir -p "$BACKUP_DIR"

# 压缩备份
tar -czf "$BACKUP_FILE" \
  --exclude="*.log" \
  --exclude="node_modules" \
  --exclude=".git" \
  -C "$(dirname $WORKSPACE)" "$(basename $WORKSPACE)"

# 保留最近 7 天的备份
find "$BACKUP_DIR" -name "workspace_backup_*.tar.gz" -mtime +7 -delete

# 发送备份通知
openclaw message send \
  --channel "1473539459369799763" \
  --text "✅ 工作区备份完成

📦 文件：${BACKUP_FILE}
📊 大小：$(du -h $BACKUP_FILE | cut -f1)"
```

#### 2. 设置定时任务

```bash
# 每天凌晨 2:00 备份
0 2 * * * /home/windflower/.openclaw/workspace/scripts/backup-workspace.sh

# 每周一上午 10:00 备份到 Feishu 云文档
0 10 * * 1 /home/windflower/.openclaw/workspace/scripts/backup-to-feishu.sh
```

---

## 自动回复示例

### Discord 自动回复

监听特定消息并自动回复。

#### 1. 基础关键词回复

```bash
#!/bin/bash
# ~/.openclaw/workspace/scripts/discord-auto-reply.sh

CHANNEL="1473539459369799763"

# 监听消息（需要配合消息监听器使用）
# 当检测到 "你好" 时回复
if [[ "$MESSAGE_CONTENT" =~ 你好 ]]; then
  openclaw message send \
    --channel "$CHANNEL" \
    --reply-to "$MESSAGE_ID" \
    --text "👋 你好！有什么我可以帮助你的吗？"
fi

# 当检测到 "帮助" 时回复帮助菜单
if [[ "$MESSAGE_CONTENT" =~ 帮助|help ]]; then
  openclaw message send \
    --channel "$CHANNEL" \
    --reply-to "$MESSAGE_ID" \
    --text "📚 **可用命令：**

• \`/weather [地点]\` - 查询天气
• \`/status\` - 查看系统状态
• \`/help\` - 显示此帮助菜单
• \`/docs\` - 查看文档链接

需要更多帮助请 @管理员"
fi
```

#### 2. 使用 message 工具监听

```bash
# 持续监听频道消息（后台运行）
openclaw message read \
  --channel "1473539459369799763" \
  --limit 10 \
  --after "$LAST_MESSAGE_ID" | while read line; do
  
  # 解析消息内容
  if echo "$line" | grep -q "天气"; then
    LOCATION=$(echo "$line" | grep -oP '(?<=天气 )[a-zA-Z]+')
    openclaw run weather --location "${LOCATION:-Beijing}" --channel "$CHANNEL"
  fi
done
```

---

### 飞书自动回复

在 Feishu 群组中自动响应。

#### 1. 飞书机器人配置

```bash
#!/bin/bash
# ~/.openclaw/workspace/scripts/feishu-auto-reply.sh

CHAT_ID="oc_XXXXXXXXXXXXX"  # 飞书群聊 ID

# 回复飞书消息
openclaw message send \
  --channel "feishu:${CHAT_ID}" \
  --text "收到你的消息了！👌"

# 发送富文本消息
openclaw message send \
  --channel "feishu:${CHAT_ID}" \
  --text "📢 **系统通知**

会议将在 **后** 开始

📍 地点：会议室 A
👥 参会人：@所有人

请准时参加！"
```

#### 2. 关键词自动回复

```bash
#!/bin/bash
# ~/.openclaw/workspace/scripts/feishu-keyword-reply.sh

CHAT_ID="oc_XXXXXXXXXXXXX"

case "$KEYWORD" in
  "文档")
    openclaw message send \
      --channel "feishu:${CHAT_ID}" \
      --text "📄 文档链接：
https://bytedance.feishu.cn/docx/XXXXX"
    ;;
  "会议")
    openclaw message send \
      --channel "feishu:${CHAT_ID}" \
      --text "📅 今日会议安排：
• 10:00 - 晨会
• 14:00 - 项目评审
• 16:00 - 技术分享"
    ;;
  "帮助")
    openclaw message send \
      --channel "feishu:${CHAT_ID}" \
      --text "💡 关键词回复：
• 文档 - 查看文档链接
• 会议 - 查看会议安排
• 天气 - 查询天气
• 帮助 - 显示此菜单"
    ;;
esac
```

---

### 关键词触发

基于消息内容触发不同操作。

#### 1. 多关键词监听脚本

```bash
#!/bin/bash
# ~/.openclaw/workspace/scripts/keyword-trigger.sh

CHANNEL="1473539459369799763"
MESSAGE="$1"
MESSAGE_ID="$2"

# 天气查询
if [[ "$MESSAGE" =~ 天气|weather ]]; then
  LOCATION=$(echo "$MESSAGE" | grep -oP '(?<=(天气|weather) )[a-zA-Z\u4e00-\u9fa5]+' || echo "Beijing")
  openclaw run weather --location "$LOCATION" --channel "$CHANNEL"
  
# 文档查询
elif [[ "$MESSAGE" =~ 文档|doc ]]; then
  openclaw message send \
    --channel "$CHANNEL" \
    --reply-to "$MESSAGE_ID" \
    --text "📚 文档中心：
• 用户手册：/docs/user-guide.md
• API 文档：/docs/api-reference.md
• 示例代码：/docs/examples/"

# 状态查询
elif [[ "$MESSAGE" =~ 状态|status ]]; then
  openclaw exec "system-status.sh" --channel "$CHANNEL"
  
# 重启服务
elif [[ "$MESSAGE" =~ 重启|restart ]]; then
  openclaw message send \
    --channel "$CHANNEL" \
    --reply-to "$MESSAGE_ID" \
    --text "⚠️ 确认重启服务？回复 \`确认\` 继续"
fi
```

#### 2. 智能回复（使用 AI）

```bash
#!/bin/bash
# ~/.openclaw/workspace/scripts/ai-auto-reply.sh

CHANNEL="1473539459369799763"
QUESTION="$1"

# 使用 AI 生成回复
RESPONSE=$(openclaw ai ask --model "qwen3.5-plus" --prompt "
用户问题：${QUESTION}
请用简洁友好的语气回复，不超过 100 字。
")

openclaw message send \
  --channel "$CHANNEL" \
  --reply-to "$MESSAGE_ID" \
  --text "$RESPONSE"
```

---

## 工作流示例

### 邮件处理工作流

自动处理收到的邮件并分类。

#### 1. 邮件分类脚本

```bash
#!/bin/bash
# ~/.openclaw/workspace/scripts/email-workflow.sh

MAILBOX="/var/mail/windflower"
PROCESSED_DIR="/home/windflower/mail/processed"

# 读取新邮件
for email in "$MAILBOX"/new/*; do
  [ -f "$email" ] || continue
  
  # 提取邮件内容
  SUBJECT=$(grep "^Subject:" "$email" | cut -d: -f2-)
  FROM=$(grep "^From:" "$email" | cut -d: -f2-)
  BODY=$(cat "$email")
  
  # 根据主题分类
  if [[ "$SUBJECT" =~ 发票|invoice ]]; then
    mkdir -p "$PROCESSED_DIR/finance"
    mv "$email" "$PROCESSED_DIR/finance/"
    openclaw message send \
      --channel "1473539459369799763" \
      --text "📧 收到发票邮件
来自：${FROM}
主题：${SUBJECT}
已归类到财务文件夹"
    
  elif [[ "$SUBJECT" =~ 会议|meeting ]]; then
    mkdir -p "$PROCESSED_DIR/meetings"
    mv "$email" "$PROCESSED_DIR/meetings/"
    # 提取会议时间并添加到日历
    # ... (日历集成代码)
    
  else
    mkdir -p "$PROCESSED_DIR/misc"
    mv "$email" "$PROCESSED_DIR/misc/"
  fi
done
```

---

### 文档整理工作流

自动整理下载的文档到对应目录。

#### 1. 文档自动分类

```bash
#!/bin/bash
# ~/.openclaw/workspace/scripts/doc-organizer.sh

DOWNLOAD_DIR="/home/windflower/Downloads"
DOCS_ROOT="/home/windflower/.openclaw/workspace/docs"

# 扫描下载目录
find "$DOWNLOAD_DIR" -type f \( -name "*.pdf" -o -name "*.md" -o -name "*.docx" \) | while read file; do
  
  FILENAME=$(basename "$file")
  
  # 根据文件名分类
  if [[ "$FILENAME" =~ 合同|contract ]]; then
    DEST="$DOCS_ROOT/legal/contracts"
  elif [[ "$FILENAME" =~ 报告|report ]]; then
    DEST="$DOCS_ROOT/reports"
  elif [[ "$FILENAME" =~ 手册|manual ]]; then
    DEST="$DOCS_ROOT/manuals"
  else
    DEST="$DOCS_ROOT/misc"
  fi
  
  # 创建目录并移动文件
  mkdir -p "$DEST"
  mv "$file" "$DEST/"
  
  # 如果是 Markdown，更新索引
  if [[ "$FILENAME" =~ \.md$ ]]; then
    echo "- [${FILENAME}](${DEST}/${FILENAME})" >> "$DOCS_ROOT/INDEX.md"
  fi
  
  echo "✅ 已整理：${FILENAME} -> ${DEST}"
done

# 发送整理报告
COUNT=$(find "$DOWNLOAD_DIR" -type f \( -name "*.pdf" -o -name "*.md" -o -name "*.docx" \) | wc -l)
openclaw message send \
  --channel "1473539459369799763" \
  --text "📁 文档整理完成
本次整理：${COUNT} 个文件"
```

---

### 代码审查工作流

自动审查提交的代码并发送反馈。

#### 1. Git 钩子集成

```bash
#!/bin/bash
# ~/.openclaw/workspace/scripts/code-review.sh

REPO_DIR="/home/windflower/projects/my-project"
CHANNEL="1473539459369799763"

cd "$REPO_DIR"

# 获取最新提交
LATEST_COMMIT=$(git log -1 --pretty=format:"%h - %s (%an)")
CHANGED_FILES=$(git diff HEAD~1 --name-only)

# 代码检查
ISSUES=""

# 检查是否有调试代码
if git diff HEAD~1 | grep -E "console\.log|print\(|debugger"; then
  ISSUES="${ISSUES}⚠️ 发现调试代码，请移除\n"
fi

# 检查提交信息格式
COMMIT_MSG=$(git log -1 --pretty=format:"%s")
if ! [[ "$COMMIT_MSG" =~ ^(feat|fix|docs|style|refactor|test|chore): ]]; then
  ISSUES="${ISSUES}⚠️ 提交信息格式不规范\n"
fi

# 发送审查结果
if [ -n "$ISSUES" ]; then
  openclaw message send \
    --channel "$CHANNEL" \
    --text "🔍 **代码审查反馈**

提交：${LATEST_COMMIT}

${ISSUES}
请修正后重新提交"
else
  openclaw message send \
    --channel "$CHANNEL" \
    --text "✅ **代码审查通过**

提交：${LATEST_COMMIT}
变更文件：${CHANGED_FILES//$/\\n• }

可以继续合并"
fi
```

#### 2. PR 自动评论

```bash
#!/bin/bash
# ~/.openclaw/workspace/scripts/pr-auto-comment.sh

REPO="windflower/my-project"
PR_NUMBER="$1"

# 运行测试
TEST_RESULT=$(cd /home/windflower/projects/my-project && npm test 2>&1)

if [ $? -eq 0 ]; then
  COMMENT="✅ 所有测试通过！
\`\`\`
${TEST_RESULT:0:500}
\`\`\`"
else
  COMMENT="❌ 测试失败，请修复后重新提交"
fi

# 使用 gh CLI 添加评论
gh pr comment "$PR_NUMBER" --body "$COMMENT" --repo "$REPO"
```

---

## 技能组合示例

### 天气 + 日程提醒

```bash
#!/bin/bash
# ~/.openclaw/workspace/scripts/weather-schedule.sh

CHANNEL="1473539459369799763"
LOCATION="Beijing"

# 获取天气
WEATHER=$(openclaw run weather --location "$LOCATION" --json)
TEMP=$(echo "$WEATHER" | jq '.temperature')
CONDITION=$(echo "$WEATHER" | jq '.condition')

# 获取今日日程
SCHEDULE=$(openclaw calendar list --date today)

# 组合消息
if [[ "$CONDITION" =~ 雨|rain ]] && [[ "$SCHEDULE" =~ 外出|outdoor ]]; then
  ALERT="☔ 提醒：今天有雨，外出请带伞！"
elif [[ "$TEMP" -lt 5 ]]; then
  ALERT="🥶 提醒：气温较低，注意保暖！"
elif [[ "$TEMP" -gt 30 ]]; then
  ALERT="☀️ 提醒：气温较高，注意防暑！"
else
  ALERT=""
fi

openclaw message send \
  --channel "$CHANNEL" \
  --text "📅 **今日简报**

🌤️ 天气：${CONDITION} ${TEMP}°C
${ALERT}
---
${SCHEDULE}"
```

### 文档 + 通知联动

```bash
#!/bin/bash
# ~/.openclaw/workspace/scripts/doc-notify.sh

DOC_PATH="/home/windflower/.openclaw/workspace/docs/important.md"
CHANNEL="1473539459369799763"

# 监控文档变更
LAST_MODIFIED=$(stat -c %Y "$DOC_PATH")
CURRENT_TIME=$(date +%s)
DIFF=$((CURRENT_TIME - LAST_MODIFIED))

# 如果 内有更新
if [ $DIFF -lt 300 ]; then
  DOC_CONTENT=$(head -20 "$DOC_PATH")
  
  openclaw message send \
    --channel "$CHANNEL" \
    --text "📄 **文档已更新**

文件：important.md
时间：$(date)

${DOC_CONTENT}

[查看详情](file://${DOC_PATH})"
fi
```

---

## 本节要点

### 关键要点

1. **定时任务**：使用 cron 或系统定时器执行周期性任务
2. **自动回复**：监听消息关键词，触发预设响应
3. **工作流**：串联多个步骤，实现复杂自动化
4. **技能组合**：整合多个工具，发挥协同效应

### 最佳实践

- ✅ 脚本添加错误处理和日志记录
- ✅ 敏感信息使用环境变量或配置文件
- ✅ 定期清理临时文件和旧日志
- ✅ 重要操作添加确认步骤
- ✅ 自动化失败时发送告警通知

### 下一步

- 尝试修改示例脚本适配你的需求
- 组合多个示例创建自定义工作流
- 分享你的自动化脚本到社区

---

_文档版本：1.0 | 最后更新：2026-03-06_
