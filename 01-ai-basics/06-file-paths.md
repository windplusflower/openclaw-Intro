# 文件路径概念

> 理解绝对路径和相对路径

---

## 📍 什么是文件路径

**文件路径** 是文件在电脑中的"地址"。

### 通俗理解

| 概念 | 比喻 | 例子 |
|------|------|------|
| **文件** | 房子 | `file.txt` |
| **文件夹** | 街道 | `Documents/` |
| **路径** | 完整地址 | `/home/user/Documents/file.txt` |

---

## 🗺️ 两种路径

### 1. 绝对路径

**绝对路径** = 从根目录开始的完整路径

```bash
# macOS 示例
/Users/zhangsan/Documents/file.txt
/Users/zhangsan/Projects/code.py
/Applications/Visual Studio Code.app

# Windows 示例
C:\Users\Zhangsan\Documents\file.txt
C:\Users\Zhangsan\Projects\code.py
C:\Program Files\Microsoft\

# 特点
✅ 始终指向同一个位置
✅ 从任何目录都能访问
❌ 路径较长
```

### 2. 相对路径

**相对路径** = 从当前目录开始的路径

```bash
# 假设当前在 /Users/zhangsan/

# 相对路径示例
Documents/file.txt      # 等同于 /Users/zhangsan/Documents/file.txt
Projects/code.py        # 等同于 /Users/zhangsan/Projects/code.py
../other/file.txt       # 上级目录的 other 文件夹

# 特点
✅ 路径较短
✅ 便于迁移项目
❌ 依赖当前目录位置
```

---

## 🔑 特殊符号

### 路径符号

| 符号 | 含义 | 例子 |
|------|------|------|
| `~` | 用户主目录 | `~/Documents` |
| `.` | 当前目录 | `./file.txt` |
| `..` | 上级目录 | `../Documents` |
| `/` | 路径分隔符（Mac） | `/home/user` |
| `\` | 路径分隔符（Win） | `C:\Users\user` |

### 实际用法

```bash
# ~ 用户主目录
cd ~              # 回到主目录
cd ~/Documents    # 进入 Documents 文件夹
ls ~/Projects     # 查看 Projects 文件夹

# . 当前目录
./script.sh       # 执行当前目录的脚本
cat ./file.txt    # 查看当前目录的文件

# .. 上级目录
cd ..             # 返回上级目录
cd ../..          # 返回上上级目录
ls ../src         # 查看上级目录的 src 文件夹
```

---

## 🌲 目录结构

### macOS 目录结构

```
/                    # 根目录
├── Applications/    # 应用程序
├── Users/           # 用户文件夹
│   └── zhangsan/   # 你的主目录（~）
│       ├── Desktop/     # 桌面
│       ├── Documents/   # 文档
│       ├── Downloads/   # 下载
│       ├── Music/       # 音乐
│       ├── Pictures/    # 图片
│       └── Projects/    # 项目
├── System/          # 系统文件
└── Library/         # 库文件
```

### Windows 目录结构

```
C:\                      # C 盘根目录
├── Users\              # 用户文件夹
│   └── Zhangsan\      # 你的主目录
│       ├── Desktop\       # 桌面
│       ├── Documents\     # 文档
│       ├── Downloads\     # 下载
│       ├── Music\         # 音乐
│       ├── Pictures\      # 图片
│       └── Projects\      # 项目
├── Program Files\     # 程序文件
└── Windows\           # 系统文件
```

---

## 🔄 路径转换

### 绝对路径 → 相对路径

```bash
# 假设当前在 /Users/zhangsan/

# 绝对路径
/Users/zhangsan/Documents/file.txt

# 相对路径（从当前位置）
Documents/file.txt
```

### 相对路径 → 绝对路径

```bash
# 假设当前在 /Users/zhangsan/Projects/

# 相对路径
src/main.py

# 绝对路径
/Users/zhangsan/Projects/src/main.py

# 如何查看绝对路径
pwd              # 查看当前绝对路径
pwd/src/main.py  # 组合出绝对路径
```

---

## 📝 实践练习

### 练习 1：理解路径

```bash
# 1. 查看当前绝对路径
pwd

# 2. 返回主目录
cd ~

# 3. 查看主目录的绝对路径
pwd

# 4. 进入 Documents 文件夹（相对路径）
cd Documents

# 5. 查看当前位置（绝对路径）
pwd

# 6. 用绝对路径返回
cd /Users/zhangsan    # Mac
cd C:\Users\Zhangsan  # Win
```

### 练习 2：路径导航

```bash
# 从任意位置回到主目录
cd ~              # 方法 1
cd $HOME          # 方法 2
cd                # 方法 3

# 在目录间切换
cd ~/Documents
cd ../Desktop
cd ../Downloads
cd ..

# 查看每步的绝对路径
pwd
```

### 练习 3：创建目录结构

```bash
# 1. 在主目录创建项目文件夹
mkdir -p ~/project/src
mkdir -p ~/project/docs
mkdir -p ~/project/tests

# 2. 用相对路径导航
cd ~/project
cd src
cd ../docs
cd ../tests

# 3. 查看完整结构
cd ~/project
ls -R

# 4. 清理
cd ~
rm -r project
```

---

## 💡 实用技巧

### 技巧 1：快速切换目录

```bash
# 记住常用路径
export PROJECTS=~/Projects
export DOCS=~/Documents

# 快速切换
cd $PROJECTS
cd $DOCS

# Windows PowerShell
$env:PROJECTS="$HOME\Projects"
cd $env:PROJECTS
```

### 技巧 2：查看路径信息

```bash
# 查看文件绝对路径
realpath file.txt       # macOS
Get-Item file.txt       # Windows

# 查看路径是否存在
ls /path/to/check
Test-Path /path/to/check  # Windows
```

### 技巧 3：路径补全

```bash
# 用 Tab 补全路径
cd ~/Doc[TAB]     # 自动补全为 ~/Documents/
cd ~/Pro[TAB]     # 自动补全为 ~/Projects/

# 提示：
# 多按几次 Tab 可以显示所有匹配项
```

---

## ⚠️ 常见错误

### 错误 1：路径拼写错误

```bash
# ❌ 错误
cd Docuemnts      # 拼写错误
cd document       # 大小写错误（Mac）
cd Document/      # 缺少 s

# ✅ 正确
cd Documents

# 解决方法：用 Tab 补全
cd Doc[TAB]
```

### 错误 2：混淆路径分隔符

```bash
# ❌ 错误（在 Mac 上）
cd C:\Users\Zhangsan

# ❌ 错误（在 Win 上）
cd /Users/Zhangsan

# ✅ 正确
# Mac 用 /
cd /Users/Zhangsan

# Win 用 \ 或 /
cd C:\Users\Zhangsan
cd C:/Users/Zhangsan  # PowerShell 支持
```

### 错误 3：相对路径 confusion

```bash
# 假设目录结构：
# /home/user/
# ├── project/
# │   └── src/
# └── docs/

# 在 /home/user/project/src/ 目录下

# ❌ 错误：以为 .. 是项目根目录
cd ..         # 实际到了 /home/user/project/

# ✅ 正确：到 docs 目录
cd ../../docs

# 提示：用 pwd 确认当前位置
```

---

## 📊 路径对比表

| 场景 | 绝对路径 | 相对路径 |
|------|---------|---------|
| **从任何地方访问** | ✅ 推荐 | ❌ 不可用 |
| **项目内部引用** | ❌ 不推荐 | ✅ 推荐 |
| **脚本中硬编码** | ❌ 不推荐 | ✅ 推荐 |
| **配置文件路径** | ⚠️ 看情况 | ⚠️ 看情况 |

---

## 📚 延伸阅读

- [常用命令](05-common-commands.md) - 20 个常用命令
- [代码是什么](07-code-basics.md) - 理解代码中的路径

---

## ✅ 本节小结

**你学到了**：

- ✅ 绝对路径和相对路径的区别
- ✅ 特殊符号（~, ., ..）的用法
- ✅ macOS 和 Windows 目录结构
- ✅ 路径转换技巧
- ✅ 常见错误和解决方法

**下一节**：[代码是什么](07-code-basics.md)
