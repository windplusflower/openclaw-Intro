# 终端入门

> 克服对终端的恐惧

---

## 💻 什么是终端

**终端**（Terminal）是你与电脑"直接对话"的界面。

### 通俗理解

| 界面类型 | 比喻 | 例子 |
|----------|------|------|
| **图形界面** | 餐厅菜单（点菜） | 窗口、按钮、图标 |
| **终端** | 直接跟厨师说话 | 输入命令、执行 |

### 为什么需要终端

有些操作图形界面做不到：
- 🔧 安装开发工具（如 OpenClaw）
- 📁 批量处理文件
- 🤖 自动化脚本
- 📊 查看系统信息

---

## 😨 终端恐惧症

### 常见恐惧

| 恐惧 | 真相 |
|------|------|
| ❌ "会弄坏电脑" | ✅ 普通命令不会损坏系统 |
| ❌ "很难学" | ✅ 基础命令只有 10 个左右 |
| ❌ "要记很多命令" | ✅ 可以查速查表 |
| ❌ "输错了怎么办" | ✅ 大部分错误可以撤销 |

### 安全提醒

**终端不会弄坏电脑**，只要你：
- ✅ 按照教程操作
- ✅ 不运行不明来源的代码
- ✅ 不删除系统文件

---

## 🖥️ 打开终端

### macOS

```
方法 1：聚焦搜索
1. 按 Command + Space
2. 输入 "Terminal" 或 "终端"
3. 按 Enter

方法 2：启动台
1. 打开启动台
2. 找到"其他"文件夹
3. 点击"终端"
```

### Windows

```
方法 1：搜索
1. 按 Win + S
2. 输入 "PowerShell"
3. 按 Enter

方法 2：运行
1. 按 Win + R
2. 输入 "powershell"
3. 按 Enter
```

---

## 📝 你的第一个命令

### 试试这些命令

```bash
# macOS 和 Windows 都支持

# 1. 查看当前在哪里
pwd          # macOS
Get-Location # Windows

# 2. 列出文件
ls           # macOS
ls           # Windows (PowerShell)

# 3. 显示问候
echo "你好"   # macOS
Write-Output "你好" # Windows

# 4. 清屏
clear        # macOS
Clear-Host   # Windows
```

### 实际操作

打开终端，依次输入：

```bash
# 1. 看看自己在哪里
pwd

# 2. 看看这里有什么文件
ls

# 3. 打个招呼
echo "Hello, Terminal!"

# 4. 清屏，重新开始
clear
```

---

## 🎯 终端基本结构

### 命令格式

```
命令 [选项] [参数]
```

### 示例解析

```bash
ls -la /home/user

└─ ls     → 命令（列出文件）
   └─ -la → 选项（显示所有文件 + 详细信息）
      └─ /home/user → 参数（目标路径）
```

### 常见符号

| 符号 | 含义 | 例子 |
|------|------|------|
| `~` | 用户主目录 | `~/Documents` |
| `.` | 当前目录 | `./file.txt` |
| `..` | 上级目录 | `../Documents` |
| `/` | 路径分隔符（Mac） | `/home/user` |
| `\` | 路径分隔符（Win） | `C:\Users\user` |

---

## 🔄 常用操作

### 导航

```bash
# 切换目录
cd Documents      # 进入 Documents 文件夹
cd ..             # 返回上级目录
cd ~              # 回到主目录
cd /              # 到根目录（Mac）
cd C:\            # 到 C 盘根（Win）

# 查看当前位置
pwd               # macOS
Get-Location      # Windows
```

### 查看文件

```bash
# 列出文件
ls                # 简单列表
ls -l             # 详细信息
ls -la            # 包括隐藏文件

# 查看文件内容
cat file.txt      # macOS
Get-Content file.txt # Windows
```

### 创建和删除

```bash
# 创建目录
mkdir myfolder

# 创建文件
touch file.txt    # macOS
New-Item file.txt # Windows

# 删除文件
rm file.txt       # macOS
Remove-Item file.txt # Windows

# 删除目录
rm -r myfolder    # macOS
Remove-Item -r myfolder # Windows
```

---

## ⌨️ 快捷键

### 通用快捷键

| 快捷键 | 功能 |
|--------|------|
| `Tab` | 自动补全 |
| `↑` | 上一条命令 |
| `↓` | 下一条命令 |
| `Ctrl + C` | 取消当前命令 |
| `Ctrl + L` | 清屏 |

### Tab 补全

```bash
# 输入前几个字母，按 Tab 自动补全

# 例如：
cd Doc[TAB]  → 自动补全为 cd Documents/
```

---

## 📝 实践示例

### 示例 1：基础导航

```bash
# 1. 打开终端
# 2. 查看当前位置
pwd

# 3. 切换到桌面
cd Desktop       # macOS
cd Desktop       # Windows

# 4. 查看桌面上有什么
ls

# 5. 返回主目录
cd ~             # macOS
cd ~             # Windows
```

### 示例 2：创建和删除

```bash
# 1. 在主目录创建一个测试文件夹
mkdir test_folder

# 2. 进入文件夹
cd test_folder

# 3. 创建一个空文件
touch test.txt   # macOS
New-Item test.txt # Windows

# 4. 查看文件
ls

# 5. 返回主目录
cd ..

# 6. 删除测试文件夹
rm -r test_folder # macOS
Remove-Item -r test_folder # Windows
```

### 示例 3：使用 Tab 补全

```bash
# 1. 输入 cd，然后按空格
# 2. 输入 D，然后按 Tab
# 3. 观察自动补全
# 4. 重复练习，熟悉 Tab 补全
```

---

## ⚠️ 注意事项

### 安全操作

| ✅ 安全 | ❌ 危险 |
|--------|--------|
| `ls` 查看文件 | `rm -rf /` 删除所有文件 |
| `cd` 切换目录 | `sudo` 随意使用 |
| `mkdir` 创建目录 | 运行不明脚本 |
| `cat` 查看内容 | 修改系统文件 |

### 遇到问题怎么办

1. **命令找不到**
   - 检查拼写
   - 检查是否在当前目录

2. **权限不足**
   - 不要随意用 sudo
   - 检查文件权限

3. **卡住了**
   - 按 `Ctrl + C` 取消
   - 关闭终端重新打开

---

## 💡 实用技巧

### 提高效率

1. **用 ↑ ↓ 找历史命令**
   ```bash
   # 按 ↑ 找到之前输入的命令
   # 修改后直接执行
   ```

2. **用 Tab 补全**
   ```bash
   # 输入前几个字母
   # 按 Tab 自动补全
   ```

3. **复制粘贴**
   ```bash
   # macOS: Command + C / Command + V
   # Windows: Ctrl + C / Ctrl + V
   ```

### 记住这些就够了

初学者只需要记住 10 个命令：

```bash
pwd      # 我在哪
ls       # 有什么
cd       # 去哪里
mkdir    # 创建目录
touch    # 创建文件
rm       # 删除
cat      # 查看内容
clear    # 清屏
cp       # 复制
mv       # 移动
```

---

## 📚 延伸阅读

- [常用命令](05-common-commands.md) - 20 个常用命令详解
- [文件路径概念](06-file-paths.md) - 绝对路径 vs 相对路径

---

## ✅ 本节要点

**你学到了**：

- ✅ 什么是终端
- ✅ 如何打开终端
- ✅ 基础导航命令
- ✅ 创建和删除文件
- ✅ 常用快捷键
- ✅ 安全注意事项

**下一节**：[常用命令](05-common-commands.md)
