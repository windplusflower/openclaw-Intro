# 部署到 GitHub Pages

## 方法 1：使用 GitHub Actions（推荐）

### 步骤

1. 在仓库根目录创建 `.github/workflows/deploy.yml`
2. 配置自动部署
3. 推送代码后自动部署

### 创建 GitHub Actions 工作流

```bash
mkdir -p .github/workflows
cat > .github/workflows/deploy.yml << 'WORKFLOW'
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.x'
      
      - name: Install MkDocs
        run: |
          pip install mkdocs mkdocs-material
      
      - name: Build site
        run: mkdocs build
      
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./site
WORKFLOW
```

### 启用 GitHub Pages

1. 访问：https://github.com/windplusflower/AI-Intro/settings/pages
2. Source 选择：GitHub Actions
3. 等待部署完成
4. 访问生成的网页

---

## 方法 2：手动部署

### 本地安装 MkDocs

```bash
pip install mkdocs mkdocs-material
```

### 本地预览

```bash
mkdocs serve
# 访问 http://127.0.0.1:8000
```

### 构建并推送

```bash
mkdocs build
# 生成的网页在 ./site 目录
# 手动推送到 gh-pages 分支
```

---

## 预计效果

- ✅ 响应式设计（支持手机/平板/电脑）
- ✅ 搜索功能
- ✅ 侧边栏导航
- ✅ 深色/浅色模式切换
- ✅ 代码高亮和复制
- ✅ 目录导航

## 访问地址

部署完成后访问：
https://windplusflower.github.io/AI-Intro/
