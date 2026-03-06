# 命令速查表

快速查阅的常用命令对照表，支持 macOS 和 Windows 双平台。

---

## 文件操作

| 功能 | macOS | Windows (PowerShell) | Windows (CMD) | 说明 |
|------|-------|---------------------|---------------|------|
| 列出目录内容 | `ls` | `ls` 或 `dir` | `dir` | 显示当前目录文件 |
| 详细列表 | `ls -la` | `ls -l` | `dir` | 显示详细信息 |
| 创建文件 | `touch filename` | `ni filename` | `type nul > filename` | 新建空文件 |
| 创建目录 | `mkdir dirname` | `mkdir dirname` | `mkdir dirname` | 新建文件夹 |
| 复制文件 | `cp src dst` | `cp src dst` | `copy src dst` | 复制文件 |
| 复制目录 | `cp -r src dst` | `cp -r src dst` | `xcopy /E src dst` | 递归复制文件夹 |
| 移动/重命名 | `mv src dst` | `mv src dst` | `move src dst` | 移动或重命名 |
| 删除文件 | `rm filename` | `rm filename` | `del filename` | 删除文件 |
| 删除目录 | `rm -rf dirname` | `rm -r dirname` | `rmdir /S dirname` | 递归删除文件夹 |
| 查找文件 | `find . -name "*.txt"` | `gci -Recurse -Filter "*.txt"` | `dir /S *.txt` | 搜索文件 |
| 文件权限 | `chmod 755 file` | `icacls file` | `icacls file` | 修改文件权限 |
| 文件所有者 | `chown user file` | — | — | 修改所有者 (Unix) |
| 查看文件大小 | `du -sh file` | `gci file | Measure-Object -Sum Length` | `dir file` | 显示文件大小 |
| 统计行数 | `wc -l file` | `gci file | Measure-Object -Line` | `find /c /v "" file` | 统计文件行数 |
| 比较文件 | `diff f1 f2` | `diff f1 f2` | `fc f1 f2` | 比较文件差异 |
| 创建软链接 | `ln -s src link` | `New-Item -Type SymbolicLink` | `mklink link src` | 创建符号链接 |
| 压缩文件 | `tar -czf a.tar.gz dir` | `Compress-Archive dir a.zip` | — | 创建压缩包 |
| 解压文件 | `tar -xzf a.tar.gz` | `Expand-Archive a.zip` | — | 解压文件 |
| 查看文件类型 | `file filename` | — | — | 识别文件类型 |

---

## 目录导航

| 功能 | macOS | Windows (PowerShell) | Windows (CMD) | 说明 |
|------|-------|---------------------|---------------|------|
| 显示当前路径 | `pwd` | `pwd` 或 `Get-Location` | `cd` | 显示工作目录 |
| 切换目录 | `cd /path` | `cd /path` | `cd /path` | 进入目录 |
| 返回上级 | `cd ..` | `cd ..` | `cd ..` | 返回上一级 |
| 返回根目录 | `cd /` | `cd \` | `cd \` | 回到根目录 |
| 返回家目录 | `cd ~` | `cd ~` | `cd %USERPROFILE%` | 回到用户目录 |
| 查看目录栈 | `dirs` | — | — | 显示目录历史 |
| 推入目录栈 | `pushd /path` | `pushd /path` | `pushd /path` | 保存当前目录 |
| 弹出目录栈 | `popd` | `popd` | `popd` | 恢复保存的目录 |
| 列出目录树 | `tree` | `tree` | `tree` | 显示目录结构 |

---

## 文件查看

| 功能 | macOS | Windows (PowerShell) | Windows (CMD) | 说明 |
|------|-------|---------------------|---------------|------|
| 查看内容 | `cat file` | `cat file` 或 `gc file` | `type file` | 显示全文 |
| 分页查看 | `less file` | `less file` | `more file` | 分页浏览 |
| 查看头部 | `head -n 20 file` | `gc file -Head 20` | `more +0 file` | 显示前 N 行 |
| 查看尾部 | `tail -n 20 file` | `gc file -Tail 20` | `more +N file` | 显示后 N 行 |
| 实时追踪 | `tail -f file` | `gc file -Wait` | — | 实时监控文件变化 |
| 搜索内容 | `grep "pattern" file` | `Select-String "pattern" file` | `findstr "pattern" file` | 文本搜索 |
| 正则搜索 | `grep -E "regex" file` | `Select-String -Pattern "regex" file` | `findstr /R "regex" file` | 正则表达式搜索 |
| 高亮显示 | `grep --color file` | `Select-String file` | — | 高亮匹配内容 |
| 统计词数 | `wc file` | `gc file | Measure-Object` | — | 统计行/词/字节 |
| 排序内容 | `sort file` | `sort file` | `sort file` | 按行排序 |
| 去重 | `sort -u file` | `gc file | Select-Object -Unique` | — | 去除重复行 |
| 查看编码 | `file -I filename` | — | — | 检测文件编码 |
| 进制转换 | `xxd file` | `Format-Hex file` | — | 十六进制查看 |
| 查看 PDF | `open file.pdf` | `Start-Process file.pdf` | `start file.pdf` | 打开 PDF |

---

## 系统信息

| 功能 | macOS | Windows (PowerShell) | Windows (CMD) | 说明 |
|------|-------|---------------------|---------------|------|
| 系统信息 | `uname -a` | `systeminfo` | `systeminfo` | 完整系统信息 |
| 操作系统 | `sw_vers` | `Get-ComputerInfo` | `ver` | 显示 OS 版本 |
| 主机名 | `hostname` | `hostname` | `hostname` | 显示主机名 |
| 用户信息 | `whoami` | `whoami` | `whoami` | 当前用户 |
| 当前时间 | `date` | `Get-Date` | `date /t` & `time /t` | 显示日期时间 |
| 运行时间 | `uptime` | `(Get-Date) - (gcim Win32_OperatingSystem).LastBootUpTime` | — | 系统运行时长 |
| CPU 信息 | `sysctl -n machdep.cpu` | `gcim Win32_Processor` | `wmic cpu get` | CPU 详细信息 |
| 内存信息 | `vm_stat` 或 `free -h` | `gcim Win32_PhysicalMemory` | `wmic memory` | 内存使用情况 |
| 磁盘空间 | `df -h` | `Get-PSDrive` 或 `diskutil list` | `wmic logicaldisk` | 磁盘使用率 |
| 进程列表 | `ps aux` | `Get-Process` | `tasklist` | 显示进程 |
| 进程详情 | `ps -p PID` | `Get-Process -Id PID` | `tasklist /FI "PID eq PID"` | 查看特定进程 |
| 杀死进程 | `kill PID` | `Stop-Process -Id PID` | `taskkill /PID PID` | 终止进程 |
| 网络接口 | `ifconfig` 或 `ip addr` | `Get-NetIPAddress` | `ipconfig` | 网络配置 |
| 网络连接 | `netstat -an` | `Get-NetTCPConnection` | `netstat -an` | 网络连接状态 |
| DNS 查询 | `nslookup domain` | `Resolve-DnsName domain` | `nslookup domain` | DNS 解析 |
| 网络测试 | `ping host` | `Test-Connection host` | `ping host` | 测试连通性 |
| 路由追踪 | `traceroute host` | `Test-NetConnection -TraceRoute` | `tracert host` | 路由跟踪 |
| 端口扫描 | `nc -zv host port` | `Test-NetConnection -Port port` | `telnet host port` | 测试端口 |
| 环境变量 | `env` 或 `printenv` | `Get-ChildItem Env:` | `set` | 显示环境变量 |
| 查看 PATH | `echo $PATH` | `echo $env:PATH` | `echo %PATH%` | 显示路径配置 |

---

## OpenClaw 命令

| 功能 | 命令 | 说明 |
|------|------|------|
| 查看帮助 | `openclaw help` | 显示所有可用命令 |
| 网关状态 | `openclaw gateway status` | 检查网关运行状态 |
| 启动网关 | `openclaw gateway start` | 启动网关服务 |
| 停止网关 | `openclaw gateway stop` | 停止网关服务 |
| 重启网关 | `openclaw gateway restart` | 重启网关服务 |
| 查看日志 | `openclaw logs` | 查看系统日志 |
| 版本信息 | `openclaw version` | 显示版本号 |
| 配置检查 | `openclaw config check` | 验证配置文件 |
| 技能列表 | `openclaw skills list` | 列出已安装技能 |
| 技能安装 | `openclaw skills install <name>` | 安装新技能 |
| 技能更新 | `openclaw skills update` | 更新所有技能 |
| 会话状态 | `openclaw session status` | 查看当前会话 |
| 清理缓存 | `openclaw cache clean` | 清理缓存文件 |
| 健康检查 | `openclaw healthcheck` | 系统健康诊断 |
| 备份配置 | `openclaw backup` | 备份配置文件 |
| 恢复配置 | `openclaw restore` | 恢复备份配置 |

---

## 快捷键

### 终端通用

| 快捷键 | 功能 | 说明 |
|--------|------|------|
| `Ctrl + C` | 中断 | 终止当前运行的命令 |
| `Ctrl + D` | 退出 | 退出当前 shell 或输入结束 |
| `Ctrl + Z` | 挂起 | 暂停进程并放入后台 |
| `Ctrl + L` | 清屏 | 清空终端屏幕 |
| `Ctrl + A` | 行首 | 光标移至行首 |
| `Ctrl + E` | 行尾 | 光标移至行尾 |
| `Ctrl + U` | 删除前行 | 删除光标前所有内容 |
| `Ctrl + K` | 删除后行 | 删除光标后所有内容 |
| `Ctrl + W` | 删除单词 | 删除前一个单词 |
| `Ctrl + R` | 搜索历史 | 反向搜索命令历史 |
| `Ctrl + G` | 取消搜索 | 退出历史搜索模式 |
| `Tab` | 自动补全 | 命令或路径补全 |
| `Tab + Tab` | 显示选项 | 显示所有补全选项 |
| `!!` | 上一条命令 | 执行上一条命令 |
| `!$` | 最后参数 | 引用上一条命令最后参数 |
| `!*` | 所有参数 | 引用上一条命令所有参数 |
| `Ctrl + _` | 撤销 | 撤销上一次编辑 |

### macOS 专属

| 快捷键 | 功能 | 说明 |
|--------|------|------|
| `Cmd + Space` | Spotlight | 打开系统搜索 |
| `Cmd + Tab` | 切换应用 | 在应用间切换 |
| `Cmd + ` ` | 同应用切换 | 同一应用窗口间切换 |
| `Cmd + Q` | 退出应用 | 完全退出当前应用 |
| `Cmd + W` | 关闭窗口 | 关闭当前窗口 |
| `Cmd + N` | 新建窗口 | 打开新窗口 |
| `Cmd + ,` | 偏好设置 | 打开应用设置 |
| `Cmd + Shift + 3` | 全屏截图 | 截取整个屏幕 |
| `Cmd + Shift + 4` | 区域截图 | 截取选定区域 |
| `Cmd + Shift + 5` | 截图工具 | 打开截图工具栏 |
| `Cmd + V` | 粘贴 | 粘贴剪贴板内容 |
| `Cmd + C` | 复制 | 复制选中内容 |
| `Cmd + X` | 剪切 | 剪切选中内容 |
| `Cmd + Z` | 撤销 | 撤销上一步操作 |
| `Cmd + Shift + Z` | 重做 | 重做上一步操作 |

### Windows 专属

| 快捷键 | 功能 | 说明 |
|--------|------|------|
| `Win` | 开始菜单 | 打开/关闭开始菜单 |
| `Win + E` | 文件资源管理器 | 打开文件浏览器 |
| `Win + D` | 显示桌面 | 最小化所有窗口 |
| `Win + L` | 锁屏 | 锁定计算机 |
| `Win + Tab` | 任务视图 | 打开任务视图 |
| `Win + V` | 剪贴板历史 | 查看剪贴板历史 |
| `Win + .` | 表情符号 | 打开表情符号面板 |
| `Win + Shift + S` | 截图工具 | 打开截图工具 |
| `Win + P` | 投影 | 选择显示模式 |
| `Win + I` | 设置 | 打开系统设置 |
| `Win + X` | 快捷菜单 | 打开电源菜单 |
| `Win + R` | 运行 | 打开运行对话框 |
| `Alt + Tab` | 切换窗口 | 在窗口间切换 |
| `Alt + F4` | 关闭窗口 | 关闭当前窗口或退出 |
| `Ctrl + Shift + Esc` | 任务管理器 | 直接打开任务管理器 |
| `Win + Ctrl + D` | 新建桌面 | 创建新虚拟桌面 |
| `Win + Ctrl + ←/→` | 切换桌面 | 在虚拟桌面间切换 |

### VS Code 常用

| 快捷键 | 功能 | 说明 |
|--------|------|------|
| `Ctrl + P` | 快速打开 | 搜索并打开文件 |
| `Ctrl + Shift + P` | 命令面板 | 打开命令面板 |
| `Ctrl + ` ` | 切换终端 | 显示/隐藏集成终端 |
| `Ctrl + B` | 侧边栏 | 显示/隐藏侧边栏 |
| `Ctrl + /` | 注释 | 切换行注释 |
| `Ctrl + D` | 选择下一个 | 选择下一个匹配项 |
| `Ctrl + F` | 查找 | 在当前文件查找 |
| `Ctrl + H` | 替换 | 查找并替换 |
| `Ctrl + Shift + F` | 全局查找 | 在所有文件中查找 |
| `F12` | 转到定义 | 跳转到符号定义 |
| `Shift + F12` | 查看引用 | 查看所有引用 |
| `Alt + F12` | 查看定义 | 内联查看定义 |
| `Ctrl + ` ` | 新建终端 | 创建新终端实例 |

---

## Git 常用命令

| 功能 | 命令 | 说明 |
|------|------|------|
| 初始化仓库 | `git init` | 创建新仓库 |
| 克隆仓库 | `git clone <url>` | 克隆远程仓库 |
| 查看状态 | `git status` | 显示工作区状态 |
| 添加文件 | `git add <file>` | 暂存文件 |
| 添加全部 | `git add .` | 暂存所有更改 |
| 提交更改 | `git commit -m "msg"` | 提交到本地 |
| 查看历史 | `git log` | 显示提交历史 |
| 查看简史 | `git log --oneline` | 单行显示历史 |
| 创建分支 | `git branch <name>` | 新建分支 |
| 切换分支 | `git checkout <name>` | 切换分支 |
| 新建并切换 | `git checkout -b <name>` | 创建并切换 |
| 合并分支 | `git merge <name>` | 合并指定分支 |
| 推送远程 | `git push origin <branch>` | 推送到远程 |
| 拉取远程 | `git pull` | 拉取并合并 |
| 获取远程 | `git fetch` | 获取远程更新 |
| 查看远程 | `git remote -v` | 显示远程仓库 |
| 暂存更改 | `git stash` | 暂存当前工作 |
| 恢复暂存 | `git stash pop` | 恢复暂存的更改 |
| 撤销提交 | `git reset HEAD~1` | 撤销最近提交 |
| 查看差异 | `git diff` | 显示未暂存差异 |
| 标签管理 | `git tag v1.0` | 创建版本标签 |

---

## 网络工具

| 功能 | macOS | Windows | 说明 |
|------|-------|---------|------|
| 查看 IP | `ipconfig getifaddr en0` | `ipconfig` | 显示 IP 地址 |
| 公网 IP | `curl ifconfig.me` | `curl ifconfig.me` | 查询公网 IP |
| 端口监听 | `nc -l port` | `Test-NetConnection -Port` | 监听端口 |
| 传输文件 | `nc host port < file` | — | 网络传输文件 |
| HTTP 请求 | `curl url` | `curl url` 或 `iwr url` | 发送 HTTP 请求 |
| 下载文件 | `curl -O url` | `iwr url -OutFile file` | 下载文件 |
| WebSocket | `websocat url` | — | WebSocket 客户端 |
| SSH 连接 | `ssh user@host` | `ssh user@host` | 远程连接 |
| SSH 密钥 | `ssh-keygen -t ed25519` | `ssh-keygen -t ed25519` | 生成密钥 |
| 复制密钥 | `ssh-copy-id user@host` | 手动复制 | 部署公钥 |
| SCP 传输 | `scp file host:path` | `scp file host:path` | 安全复制 |
| Rsync 同步 | `rsync -av src dst` | — | 增量同步 |
| 带宽测试 | `speedtest-cli` | `speedtest-cli` | 网络测速 |

---

## 包管理

### macOS (Homebrew)

| 功能 | 命令 | 说明 |
|------|------|------|
| 安装软件 | `brew install <pkg>` | 安装包 |
| 卸载软件 | `brew uninstall <pkg>` | 卸载包 |
| 搜索软件 | `brew search <query>` | 搜索包 |
| 更新 Homebrew | `brew update` | 更新包管理器 |
| 升级所有包 | `brew upgrade` | 升级已安装包 |
| 查看信息 | `brew info <pkg>` | 显示包信息 |
| 清理缓存 | `brew cleanup` | 清理旧版本 |
| 列出已安装 | `brew list` | 显示已安装包 |
| 检查问题 | `brew doctor` | 诊断问题 |

### Windows (Chocolatey/Scoop)

| 功能 | Chocolatey | Scoop | 说明 |
|------|------------|-------|------|
| 安装软件 | `choco install <pkg>` | `scoop install <pkg>` | 安装包 |
| 卸载软件 | `choco uninstall <pkg>` | `scoop uninstall <pkg>` | 卸载包 |
| 搜索软件 | `choco search <query>` | `scoop search <query>` | 搜索包 |
| 更新所有 | `choco upgrade all` | `scoop update *` | 升级所有包 |
| 查看信息 | `choco info <pkg>` | `scoop info <pkg>` | 显示包信息 |
| 列出已安装 | `choco list --local` | `scoop list` | 显示已安装包 |

### Node.js (npm/yarn)

| 功能 | npm | yarn | 说明 |
|------|-----|------|------|
| 安装包 | `npm install <pkg>` | `yarn add <pkg>` | 安装依赖 |
| 全局安装 | `npm install -g <pkg>` | `yarn global add <pkg>` | 全局安装 |
| 卸载包 | `npm uninstall <pkg>` | `yarn remove <pkg>` | 卸载依赖 |
| 搜索包 | `npm search <query>` | `yarn search <query>` | 搜索包 |
| 运行脚本 | `npm run <script>` | `yarn <script>` | 运行脚本 |
| 查看版本 | `npm -v` | `yarn -v` | 显示版本 |
| 清理缓存 | `npm cache clean` | `yarn cache clean` | 清理缓存 |

---

## 文本处理

| 功能 | 命令 | 说明 |
|------|------|------|
| 替换文本 | `sed 's/old/new/g' file` | 全局替换 |
| 删除空行 | `sed '/^$/d' file` | 删除空白行 |
| 提取列 | `cut -d: -f1 file` | 按分隔符提取 |
| 合并行 | `paste file1 file2` | 横向合并文件 |
| 合并文件 | `cat f1 f2 > out` | 纵向合并 |
| 反转行 | `tac file` | 反向显示行 |
| 反转列 | `rev file` | 反转每行字符 |
| 随机排序 | `shuf file` | 随机打乱行 |
| 生成序列 | `seq 1 10` | 生成数字序列 |
| 计算表达式 | `expr 5 + 3` | 简单数学计算 |
| JSON 格式化 | `jq '.' file.json` | 美化 JSON |
| JSON 查询 | `jq '.key' file.json` | 提取 JSON 字段 |
| XML 解析 | `xmllint --xpath file.xml` | 解析 XML |
| CSV 处理 | `csvkit` 工具集 | CSV 数据处理 |

---

## 开发工具

| 功能 | 命令 | 说明 |
|------|------|------|
| Python REPL | `python3` 或 `ipython` | Python 交互环境 |
| Node REPL | `node` | Node.js 交互环境 |
| 启动服务器 | `python -m http.server 8000` | 简易 HTTP 服务 |
| 端口占用 | `lsof -i :port` | 查看占用端口的进程 |
| 代码格式化 | `prettier --write file` | 格式化代码 |
| 代码检查 | `eslint file` | 检查代码问题 |
| 性能分析 | `time command` | 测量命令执行时间 |
| 压力测试 | `ab -n 1000 -c 10 url` | Apache 基准测试 |
| API 测试 | `httpie url` 或 `curl` | HTTP 客户端 |
| 数据库连接 | `psql`, `mysql`, `mongosh` | 数据库客户端 |
| Docker 容器 | `docker ps` | 查看运行容器 |
| Docker 镜像 | `docker images` | 查看本地镜像 |
| Docker 日志 | `docker logs <container>` | 查看容器日志 |
| Docker 执行 | `docker exec -it <c> sh` | 进入容器 |

---

## 实用技巧

### 命令组合

```bash
# 查找并删除 7 天前的日志文件
find . -name "*.log" -mtime +7 -delete

# 统计代码行数
find . -name "*.py" | xargs wc -l

# 监控日志文件并高亮错误
tail -f app.log | grep --color "ERROR"

# 批量重命名 (添加前缀)
for f in *.txt; do mv "$f" "bak_$f"; done

# 获取外网 IP 并显示地理位置
curl ipinfo.io

# 创建目录并进入
mkdir -p new/project && cd new/project

# 快速备份
cp file.txt{,.bak}

# 查看大文件
du -ah . | sort -rh | head -20
```

### 别名建议

```bash
# ~/.bashrc 或 ~/.zshrc
alias ll='ls -la'
alias gs='git status'
alias gc='git commit'
alias gp='git push'
alias gl='git pull'
alias ka='killall'
alias ..='cd ..'
alias ...='cd ../..'
alias h='history'
alias c='clear'
```

---

## 参考资料

- [PowerShell 文档](https://docs.microsoft.com/powershell/)
- [Bash 手册](https://www.gnu.org/software/bash/manual/)
- [Git 官方文档](https://git-scm.com/doc)
- [OpenClaw 文档](https://github.com/openclaw/openclaw)

---

*最后更新：2026-03-06 | 适用于 OpenClaw v1.x*
