# 技能系统

> 加载和使用扩展技能

欢迎来到技能系统章节！通过本章，你将学会如何加载、使用和创建 OpenClaw 技能，让你的助手变得更强大。

---

## 什么是技能

### 技能的定义

**技能（Skill）** 是 OpenClaw 的扩展功能模块，就像给助手安装"插件"一样。每个技能都封装了特定的能力，让助手能够完成更多类型的任务。

简单来说：**技能 = 助手的新能力**

### 技能的作用

- 🔍 **扩展功能**：让助手能够搜索网页、查询天气、管理文件等
- 🛠️ **自动化任务**：批量处理重复性工作
- 📦 **模块化设计**：每个技能独立工作，互不干扰
- 🎯 **按需加载**：只启用你需要的功能

### 内置技能 vs 自定义技能

| 类型 | 说明 | 示例 |
|------|------|------|
| **内置技能** | OpenClaw 自带的技能，开箱即用 | 文件读写、网页搜索、天气查询 |
| **自定义技能** | 用户自己创建的技能，满足个性化需求 | 特定 API 调用、自定义工作流 |

---

## 技能位置

### 技能目录在哪里

技能文件存储在工作区的 `skills/` 目录中：

```bash
# macOS / Linux
cd ~/.openclaw/workspace/skills/

# Windows (PowerShell)
cd $env:USERPROFILE\.openclaw\workspace\skills\

# Windows (CMD)
cd %USERPROFILE%\.openclaw\workspace\skills\
```

### 技能文件结构

每个技能是一个独立的文件夹，结构如下：

```
skill-name/
├── SKILL.md          # 技能说明文件（必需）
├── script.sh         # 执行脚本（可选）
├── script.py         # Python 脚本（可选）
└── assets/           # 资源文件（可选）
```

**SKILL.md 示例：**
```markdown
## 技能名称
简短描述技能功能

## 使用方法
说明如何调用此技能

## 参数
列出支持的参数
```

### 技能命名规范

- ✅ **推荐**：使用小写字母和连字符，如 `web-search`、`file-manager`
- ❌ **避免**：大写字母、空格、特殊字符
- 📝 **原则**：见名知意，简洁清晰

---

## 加载技能

### 自动加载技能

OpenClaw 启动时会自动扫描 `skills/` 目录，加载所有包含 `SKILL.md` 的技能文件夹。

**无需手动操作**，只要技能文件放在正确位置即可。

### 手动加载技能

如果需要重新加载技能（比如新建了技能）：

```bash
# 方法 1：重启 OpenClaw
openclaw restart

# 方法 2：在对话中触发
/refresh-skills
```

### 查看已加载技能

```bash
# 列出所有可用技能
openclaw skills list

# 查看技能详情
openclaw skills show <skill-name>
```

---

## 常用技能

### 搜索技能

**技能名称**：`web-search`

**功能**：使用搜索引擎查找信息

**使用方法**：
```
搜索：[关键词]
```

**示例**：
```
搜索：OpenClaw 安装教程
搜索：Python 最佳实践
```

### 天气技能

**技能名称**：`weather`

**功能**：查询当前天气和预报

**使用方法**：
```
天气 [城市名]
```

**示例**：
```
天气 北京
天气 Shanghai
天气 Tokyo
```

### 文件管理技能

**技能名称**：`file-manager`

**功能**：读取、写入、编辑文件

**使用方法**：
```
读取文件：[路径]
写入文件：[路径] [内容]
编辑文件：[路径] [修改内容]
```

**示例**：
```
读取文件：~/notes/todo.md
写入文件：~/notes/new.md 这是新内容
```

### 代码执行技能

**技能名称**：`code-exec`

**功能**：安全地执行代码片段

**使用方法**：
```
执行代码：[语言] [代码]
```

**示例**：
```
执行代码：python print("Hello, World!")
执行代码：bash ls -la
```

---

## 使用技能

### 如何调用技能

技能调用非常自然，就像和人对话一样：

1. **直接描述需求**：助手会自动匹配技能
   ```
   帮我查一下今天的天气
   ```

2. **使用技能前缀**：明确指定技能
   ```
   搜索：最新 AI 新闻
   ```

3. **组合指令**：多个技能协同工作
   ```
   先搜索 OpenClaw 文档，然后保存到 ~/notes/
   ```

### 技能参数

某些技能支持参数来细化操作：

```bash
# 搜索技能参数
搜索：[关键词] --limit 5 --freshness pd

# 参数说明
--limit     结果数量（默认 10）
--freshness 时间范围（pd=今天，pw=本周，pm=本月）
```

### 技能组合使用

强大的地方在于技能可以组合：

**示例工作流**：
```
1. 搜索：Python 教程 --limit 3
2. 读取第一个链接的内容
3. 总结关键知识点
4. 保存到 ~/learning/python-notes.md
```

---

## 自定义技能

### 创建技能文件

**步骤 1：创建技能文件夹**
```bash
# macOS / Linux
mkdir -p ~/.openclaw/workspace/skills/my-skill

# Windows (PowerShell)
New-Item -ItemType Directory -Force $env:USERPROFILE\.openclaw\workspace\skills\my-skill
```

**步骤 2：创建 SKILL.md**
```bash
# macOS / Linux
cat > ~/.openclaw/workspace/skills/my-skill/SKILL.md << 'EOF'
# 我的技能

## 功能描述
这是一个自定义技能

## 使用方法
/my-command [参数]

## 示例
/my-command hello
EOF

# Windows (PowerShell)
@"
# 我的技能

## 功能描述
这是一个自定义技能

## 使用方法
/my-command [参数]

## 示例
/my-command hello
"@ | Out-File -FilePath "$env:USERPROFILE\.openclaw\workspace\skills\my-skill\SKILL.md" -Encoding utf8
```

### 技能模板

**基础模板**：
```markdown
# 技能名称

## 描述
[一句话说明技能用途]

## 使用方法
[命令格式]

## 参数
- `--param1`: 说明
- `--param2`: 说明

## 示例
[使用示例]

## 注意事项
[需要用户知道的事项]
```

### 测试技能

创建技能后，测试是否正常工作：

```bash
# 1. 刷新技能列表
openclaw skills refresh

# 2. 查看技能是否加载
openclaw skills list | grep my-skill

# 3. 在对话中测试
/my-command test
```

---

## 实践示例

### 示例 1：加载内置技能

**说明**：确认内置技能正常工作

**步骤**：
1. 打开 OpenClaw 对话
2. 输入：`查看可用技能`
3. 确认看到 `web-search`、`weather`、`file-manager` 等技能
4. 输入：`天气 北京` 测试天气技能

**预期结果**：收到北京天气信息

### 示例 2：使用搜索技能

**说明**：了解搜索技能的使用

**步骤**：
1. 输入：`搜索：OpenClaw 技能系统`
2. 查看返回的搜索结果
3. 尝试添加参数：`搜索：OpenClaw --limit 3 --freshness pw`
4. 比较不同参数的结果差异

**预期结果**：获得相关的搜索结果列表

### 示例 3：创建简单技能

**说明**：创建第一个自定义技能

**步骤**：
1. 创建技能文件夹：`my-greeting`
2. 创建 SKILL.md 文件，内容如下：
   ```markdown
   # 问候技能

   ## 功能
   向用户发送个性化问候

   ## 使用方法
   /greet [名字]
   ```
3. 刷新技能：`openclaw skills refresh`
4. 测试：`/greet Windflower`

**预期结果**：收到个性化问候消息

---

## 常见问题

### 技能不工作怎么办

**排查步骤**：

1. **检查技能文件是否存在**
   ```bash
   ls ~/.openclaw/workspace/skills/<skill-name>/SKILL.md
   ```

2. **检查 SKILL.md 格式**
   - 确保文件名为 `SKILL.md`（大小写敏感）
   - 确保文件是有效的 Markdown 格式

3. **重新加载技能**
   ```bash
   openclaw skills refresh
   ```

4. **查看错误日志**
   ```bash
   openclaw logs | grep skill
   ```

### 技能冲突怎么办

如果两个技能名称相同或功能冲突：

1. **重命名冲突技能**
   ```bash
   mv ~/.openclaw/workspace/skills/conflict-skill ~/.openclaw/workspace/skills/conflict-skill-old
   ```

2. **禁用不需要的技能**
   - 在技能文件夹中创建 `.disabled` 文件
   - 或将技能文件夹移出 `skills/` 目录

3. **修改技能优先级**
   - 在 SKILL.md 中添加 `priority: high/low`

### 如何删除技能

**方法 1：完全删除**
```bash
# macOS / Linux
rm -rf ~/.openclaw/workspace/skills/<skill-name>

# Windows (PowerShell)
Remove-Item -Recurse -Force "$env:USERPROFILE\.openclaw\workspace\skills\<skill-name>"
```

**方法 2：临时禁用**
```bash
# 创建禁用标记
touch ~/.openclaw/workspace/skills/<skill-name>/.disabled
```

**注意**：删除内置技能可能导致功能缺失，建议先禁用测试。

---

## 本节要点

本章我们学习了：

✅ **什么是技能**：OpenClaw 的扩展功能模块

✅ **技能位置**：存储在 `~/.openclaw/workspace/skills/` 目录

✅ **加载方式**：自动加载和手动刷新

✅ **常用技能**：搜索、天气、文件管理、代码执行

✅ **使用方法**：自然语言调用、参数传递、技能组合

✅ **自定义技能**：创建、模板、测试

✅ **问题排查**：常见问题的解决方法

---

## 下一节

完成本章后，你已经掌握了技能系统的基础知识。

**下一节预告**：`07-advanced-skills.md` - 高级技能开发

- **让 AI 帮你创建技能**（不需要自己写代码）
- 调用外部 API
- 技能间的通信与协作
- 发布和分享你的技能

---

> 💡 **小提示**：想创建新技能？**直接告诉 AI**："帮我创建一个查询天气的技能"，AI 会帮你完成所有工作！
