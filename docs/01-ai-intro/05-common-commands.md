# 常用命令

> 掌握 20 个常用终端命令

---

## 📋 命令速查

### 文件操作

| 命令 | macOS | Windows | 说明 |
|------|-------|---------|------|
| **查看文件** | `ls` | `ls` / `Get-ChildItem` | 列出目录内容 |
| **切换目录** | `cd 目录名` | `cd 目录名` | 进入指定目录 |
| **当前位置** | `pwd` | `Get-Location` | 显示当前路径 |
| **创建目录** | `mkdir 目录名` | `mkdir 目录名` | 新建文件夹 |
| **创建文件** | `touch 文件名` | `New-Item 文件名` | 新建空文件 |
| **复制文件** | `cp 源 目标` | `Copy-Item 源 目标` | 复制文件/文件夹 |
| **移动文件** | `mv 源 目标` | `Move-Item 源 目标` | 移动/重命名 |
| **删除文件** | `rm 文件名` | `Remove-Item 文件名` | 删除文件 |
| **删除目录** | `rm -r 目录名` | `Remove-Item -r 目录名` | 删除文件夹 |

### 查看内容

| 命令 | macOS | Windows | 说明 |
|------|-------|---------|------|
| **查看文件** | `cat 文件名` | `Get-Content 文件名` | 显示文件内容 |
| **分页查看** | `less 文件名` | `Get-Content 文件名` | 分页显示 |
| **查看前 N 行** | `head -n 10 文件名` | `Get-Content -Head 10 文件名` | 前 10 行 |
| **查看后 N 行** | `tail -n 10 文件名` | `Get-Content -Tail 10 文件名` | 后 10 行 |

### 系统信息

| 命令 | macOS | Windows | 说明 |
|------|-------|---------|------|
| **清屏** | `clear` | `Clear-Host` / `cls` | 清空屏幕 |
| **查看日期** | `date` | `Get-Date` | 显示当前日期时间 |
| **查看日历** | `cal` | 无 | 显示日历 |
| **查看主机名** | `hostname` | `hostname` | 显示计算机名 |
| **查看用户** | `whoami` | `whoami` | 显示当前用户 |

### 其他实用命令

| 命令 | macOS | Windows | 说明 |
|------|-------|---------|------|
| **查找文件** | `find . -name "文件名"` | `Get-ChildItem -Recurse -Filter "文件名"` | 搜索文件 |
| **查找内容** | `grep "关键词" 文件名` | `Select-String "关键词" 文件名` | 搜索内容 |
| **命令历史** | `history` | `Get-History` | 查看历史命令 |
| **命令说明** | `man 命令` | `Get-Help 命令` | 查看帮助 |
| **哪个命令** | `which 命令` | `Get-Command 命令` | 查看命令位置 |

---

## 📝 详细用法

### 1. ls - 列出文件

```bash
# 基础用法
ls              # 简单列表
ls -l           # 详细信息（权限、大小、时间）
ls -la          # 包括隐藏文件

# 示例输出
-rw-r--r--  1 user  staff  1024 Mar  5 10:00 file.txt
drwxr-xr-x  2 user  staff    64 Mar  5 10:00 folder/

# 含义
-         # 文件类型（-文件，d 目录）
rw-r--r-- # 权限（所有者/组/其他人）
1         # 链接数
user      # 所有者
staff     # 组
1024      # 大小（字节）
Mar  5 10:00 # 修改时间
file.txt  # 文件名
```

### 2. cd - 切换目录

```bash
# 基础用法
cd Documents      # 进入 Documents 文件夹
cd ..             # 返回上级目录
cd ~              # 回到主目录
cd /              # 到根目录（Mac）
cd C:\            # 到 C 盘根（Win）

# 实用技巧
cd -              # 回到上一个目录
cd ~/Documents    # 绝对路径
cd ../src         # 相对路径
```

### 3. mkdir - 创建目录

```bash
# 基础用法
mkdir myfolder              # 创建一个文件夹
mkdir folder1 folder2       # 创建多个文件夹
mkdir -p a/b/c              # 创建多级目录

# 示例
mkdir project
cd project
mkdir src docs tests
```

### 4. cp - 复制文件

```bash
# 基础用法
cp file.txt backup.txt          # 复制文件
cp -r folder/ backup/           # 复制文件夹
cp file1.txt file2.txt /dest/   # 复制到目标目录

# 实用选项
cp -i file.txt backup.txt       # 覆盖前询问
cp -v file.txt backup.txt       # 显示过程
```

### 5. mv - 移动/重命名文件

```bash
# 移动文件
mv file.txt /other/folder/      # 移动到其他目录
mv file1.txt file2.txt /dest/   # 移动多个文件

# 重命名文件
mv oldname.txt newname.txt      # 重命名文件
mv oldfolder newfolder          # 重命名文件夹

# 实用选项
mv -i file.txt dest/            # 覆盖前询问
mv -v file.txt dest/            # 显示过程
```

### 6. rm - 删除文件

```bash
# 基础用法
rm file.txt                     # 删除文件
rm -r folder/                   # 删除文件夹
rm -rf folder/                  # 强制删除（危险！）

# 实用选项
rm -i file.txt                  # 删除前询问
rm -v file.txt                  # 显示过程

# ⚠️ 警告
# 不要随意使用 rm -rf /
# 这会删除所有文件！
```

### 7. cat - 查看文件内容

```bash
# 基础用法
cat file.txt                    # 显示整个文件
cat file1.txt file2.txt         # 显示多个文件

# 实用选项
cat -n file.txt                 # 显示行号
cat -b file.txt                 # 非空行显示行号

# 查看大文件
less file.txt                   # 分页查看
head -n 20 file.txt             # 查看前 20 行
tail -n 20 file.txt             # 查看后 20 行
```

### 8. grep - 搜索内容

```bash
# 基础用法
grep "keyword" file.txt         # 搜索关键词
grep -r "keyword" folder/       # 递归搜索文件夹
grep -i "keyword" file.txt      # 忽略大小写

# 实用选项
grep -n "keyword" file.txt      # 显示行号
grep -v "keyword" file.txt      # 反向搜索（不包含）
grep -c "keyword" file.txt      # 统计匹配次数

# 示例
grep "error" log.txt            # 搜索错误日志
grep -r "TODO" src/             # 搜索所有 TODO 注释
```

---

## 🎯 实用组合

### 组合 1：查找并查看

```bash
# 查找包含"error"的文件，并查看内容
grep -r "error" logs/ | less

# 查找最近的日志文件，查看后 100 行
ls -lt logs/ | head -5 | tail -1 | xargs tail -n 100
```

### 组合 2：批量操作

```bash
# 批量重命名（添加前缀）
for file in *.txt; do mv "$file" "backup_$file"; done

# 批量删除空文件
find . -type f -empty -delete
```

### 组合 3：文件统计

```bash
# 统计文件数量
ls -1 | wc -l

# 统计代码行数
find src/ -name "*.py" | xargs wc -l

# 查找最大的文件
ls -lhS | head -10
```

---

## 📝 实践示例

### 示例 1：文件管理

```bash
# 1. 在主目录创建示例文件夹
mkdir ~/practice

# 2. 进入示例文件夹
cd ~/practice

# 3. 创建 3 个子文件夹
mkdir docs src tests

# 4. 在 src 中创建 2 个文件
cd src
touch file1.txt file2.txt

# 5. 返回主目录
cd ~/practice

# 6. 查看目录结构
ls -R

# 7. 清理
cd ~
rm -r practice
```

### 示例 2：文件操作

```bash
# 1. 创建测试文件
echo "Hello, World!" > test.txt

# 2. 查看文件内容
cat test.txt

# 3. 复制文件
cp test.txt backup.txt

# 4. 重命名文件
mv backup.txt copy.txt

# 5. 删除文件
rm test.txt copy.txt

# 6. 确认删除
ls
```

### 示例 3：搜索和过滤

```bash
# 1. 创建测试文件
echo "apple" > fruits.txt
echo "banana" >> fruits.txt
echo "cherry" >> fruits.txt

# 2. 搜索包含"a"的行
grep "a" fruits.txt

# 3. 统计行数
wc -l fruits.txt

# 4. 查看前 2 行
head -n 2 fruits.txt

# 5. 清理
rm fruits.txt
```

---

## 💡 实用技巧

### 提高效率

1. **用 Tab 补全**
   ```bash
   # 输入前几个字母，按 Tab
   cd Doc[TAB]  → cd Documents/
   ```

2. **用 ↑ ↓ 找历史命令**
   ```bash
   # 按 ↑ 找到之前的命令
   # 修改后直接执行
   ```

3. **用命令历史搜索**
   ```bash
   # macOS: Ctrl + R，然后输入关键词
   # Windows: 按 ↑ 然后输入关键词
   ```

### 常用别名

```bash
# macOS 可以添加别名（添加到 ~/.zshrc）
alias ll='ls -la'
alias ..='cd ..'
alias ...='cd ../..'

# Windows PowerShell 可以添加函数（添加到 profile）
function ll { ls -la }
function .. { cd .. }
```

---

## ⚠️ 注意事项

### 安全操作

| ✅ 安全 | ❌ 危险 |
|--------|--------|
| `ls` 查看文件 | `rm -rf /` 删除所有 |
| `cat` 查看内容 | `sudo` 随意使用 |
| `mkdir` 创建目录 | 修改系统文件 |
| `cd` 切换目录 | 运行不明脚本 |

### 常见错误

```bash
# 错误 1：命令拼写错误
sl file.txt      # ❌ 应该是 ls

# 错误 2：路径错误
cd Docuemnts     # ❌ 拼写错误
cd document      # ❌ 大小写错误（Mac）

# 错误 3：权限不足
rm system_file   # ❌ 需要 sudo

# 解决方法：
# 1. 检查拼写
# 2. 用 Tab 补全
# 3. 不要随意用 sudo
```

---

## 📚 延伸阅读

- [终端入门](./04-terminal-intro.md) - 终端基础操作
- [文件路径概念](./06-file-paths.md) - 绝对路径 vs 相对路径
- [命令速查表](../03-reference/command-cheatsheet.md) - 完整命令对照表

---

## ✅ 本节要点

**你学到了**：

- ✅ 20 个常用命令
- ✅ 双平台命令对照
- ✅ 实用组合技巧
- ✅ 常见错误和解决方法

**下一节**：[文件路径概念](./06-file-paths.md)
