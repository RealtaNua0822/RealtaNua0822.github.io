---
title: "Hugo + PaperMod 个人博客完整配置教程"
date: 2026-03-17T01:00:00+08:00
draft: false
tags: ["Hugo", "博客", "教程", "PaperMod"]
categories: ["教程"]
---

如果你也想搭建一个快速、简洁的个人博客，Hugo 是一个绝佳的选择。本文将从零开始，详细介绍如何使用 Hugo + PaperMod 主题搭建个人博客，并部署到 GitHub Pages。

## 什么是 Hugo？

Hugo 是一个快速、现代的静态网站生成器，它使用 Go 语言编写，具有以下特点：

- **超快速度**：几秒钟内构建整个网站
- **简单易用**：配置简单，上手容易
- **主题丰富**：有大量精美主题可选
- **零依赖**：无需数据库，无需后端
- **免费部署**：可免费部署到 GitHub Pages

## 项目结构概览

一个完整的 Hugo 博客项目结构如下：

```
mysite/
├── .github/          # GitHub Actions 工作流配置
├── archetypes/       # 内容模板
├── assets/           # 资源文件（CSS、JS）
├── content/          # 博客内容
├── data/             # 数据文件
├── i18n/             # 国际化文件
├── layouts/          # 自定义布局模板
├── public/           # 生成的静态网站（忽略）
├── static/           # 静态资源
├── themes/           # 主题文件
├── .gitignore        # Git 忽略文件
├── .gitmodules       # Git 子模块配置
├── .nojekyll         # 禁用 Jekyll
└── hugo.yaml         # Hugo 配置文件
```

## 核心配置文件

### 1. hugo.yaml - 主配置文件

这是 Hugo 的核心配置文件，控制网站的所有设置：

```yaml
# 基本信息
baseURL: "https://yourname.github.io/"  # 你的网站地址
languageCode: "zh-cn"                   # 语言代码
title: "我的博客"                       # 网站标题
theme: ["PaperMod"]                     # 使用主题

# 输出格式配置
outputs:
  home:
    - HTML    # 首页
    - RSS     # RSS 订阅
    - JSON    # 搜索索引（必需）

# 主题参数配置
params:
  env: "production"                     # 生产环境
  defaultTheme: "auto"                  # 自动切换深色/浅色模式
  ShowShareButtons: true                # 显示分享按钮
  ShowReadingTime: true                 # 显示阅读时间
  ShowPostNavLinks: true                # 显示文章导航
  ShowBreadCrumbs: true                 # 显示面包屑导航
  ShowCodeCopyButtons: true             # 显示代码复制按钮
  ShowToc: true                         # 显示目录
  comments: false                       # 禁用评论

  # 首页信息
  homeInfoParams:
    Title: "欢迎来到我的博客"
    Content: "这是一个使用 Hugo 和 PaperMod 主题搭建的个人博客"

  # 社交图标
  socialIcons:
    - name: "github"
      url: "https://github.com/"
    - name: "twitter"
      url: "https://twitter.com/"

# 导航菜单
menu:
  main:
    - identifier: "home"
      name: "首页"
      url: "/"
      weight: 1
    - identifier: "archives"
      name: "归档"
      url: "/archives/"
      weight: 2
    - identifier: "tags"
      name: "标签"
      url: "/tags/"
      weight: 3
    - identifier: "search"
      name: "搜索"
      url: "/search/"
      weight: 4
```

**关键配置说明：**

- `baseURL`：网站的基础 URL，必须与 GitHub Pages 地址一致
- `outputs`：定义输出格式，JSON 是搜索功能必需的
- `params`：主题自定义参数
- `menu`：网站导航菜单配置

## 内容文件管理

### 博客文章结构

所有博客内容都在 `content/` 目录下：

```
content/
├── posts/          # 博客文章
│   └── first-post.md
├── archives.md     # 归档页面
└── search.md       # 搜索页面
```

### 创建博客文章

每篇博客文章都是一个 Markdown 文件，文件头部包含 Front Matter（元数据）：

```markdown
---
title: "文章标题"
date: 2026-03-17T10:00:00+08:00
draft: false        # 是否为草稿
tags: ["标签1", "标签2"]
categories: ["分类"]
---

文章内容...
```

**Front Matter 字段说明：**

- `title`：文章标题
- `date`：发布日期
- `draft`：草稿状态（true 不会发布）
- `tags`：文章标签
- `categories`：文章分类

### 特殊页面

**归档页面** - `content/archives.md`

```markdown
---
title: "归档"
layout: "archives"     # 使用归档布局
url: "/archives/"
summary: archives
---
```

**搜索页面** - `content/search.md`

```markdown
---
title: "搜索"
layout: "search"       # 使用搜索布局
url: "/search/"
summary: search
---
```

## 主题配置

我们使用 PaperMod 主题，这是一个简洁、响应式的 Hugo 主题，通过 Git 子模块管理：

### 安装主题

```bash
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```

### 主题结构

```
themes/PaperMod/
├── assets/
│   ├── css/          # 样式文件
│   └── js/           # JavaScript 文件
│       ├── fastsearch.js    # 搜索功能
│       ├── fuse.basic.min.js  # 搜索引擎
│       └── license.js
├── layouts/
│   ├── _default/     # 默认布局
│   │   ├── index.json       # 搜索索引生成
│   │   ├── search.html      # 搜索页面
│   │   └── single.html      # 文章页面
│   └── partials/     # 组件模板
│       ├── head.html        # HTML 头部
│       ├── header.html      # 网站头部
│       ├── footer.html      # 网站底部
│       └── ...
└── i18n/             # 国际化文件
    ├── zh.yaml       # 中文
    └── en.yaml       # 英文
```

### 自定义样式

如果需要自定义样式，可以在项目根目录创建对应文件：

```
assets/
└── css/
    └── extended/
        └── custom.css    # 自定义样式
```

## 其他重要文件

### 1. archetypes/ - 内容模板

默认文章模板，创建新文章时会自动使用：

```markdown
+++
title = '{{ replace .File.ContentBaseName "-" " " | title }}'
date = {{ .Date }}
draft = true
+++
```

### 2. static/ - 静态资源

存放不需要处理的静态文件：

```
static/
├── images/         # 图片
├── favicon.ico     # 网站图标
└── robots.txt      # 搜索引擎爬虫配置
```

### 3. layouts/ - 自定义布局

覆盖主题的默认布局：

```
layouts/
├── _default/
│   └── single.html      # 自定义文章页面
└── partials/
    └── extend_head.html  # 自定义头部
```

### 4. .gitignore - Git 忽略文件

```gitignore
# 忽略生成的静态网站文件
public/

# 忽略临时文件
*.swp
*.swo
*~
.DS_Store

# 忽略依赖
node_modules/
```

### 5. .nojekyll - 禁用 Jekyll

**重要！** 空文件，告诉 GitHub Pages 不要使用 Jekyll 处理，这是 Hugo 部署到 GitHub Pages 的必需文件。

## 部署到 GitHub Pages

### 1. 创建 GitHub 仓库

1. 在 GitHub 创建新仓库，命名为 `yourname.github.io`
2. 初始化本地仓库并推送：

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin git@github.com:yourname/yourname.github.io.git
git push -u origin main
```

### 2. 配置 GitHub Actions

创建 `.github/workflows/hugo.yml`：

```yaml
name: Deploy Hugo site to Pages

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: '0.147.0'
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb

      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0

      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5

      - name: Build with Hugo
        env:
          HUGO_ENVIRONMENT: production
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### 3. 配置 GitHub Pages 设置

1. 进入仓库的 **Settings** → **Pages**
2. 在 **Build and deployment** → **Source** 下，选择 **GitHub Actions**
3. GitHub 会自动识别你的工作流

### 4. 创建 .nojekyll 文件

```bash
touch .nojekyll
git add .nojekyll
git commit -m "Add .nojekyll to disable Jekyll processing"
git push
```

## 常用命令

### 本地开发

```bash
# 创建新文章
hugo new posts/my-new-post.md

# 启动本地服务器（热重载）
hugo server -D

# 构建生产版本
hugo

# 构建并预览草稿
hugo server --buildDrafts
```

### Git 操作

```bash
# 添加所有更改
git add .

# 提交更改
git commit -m "描述信息"

# 推送到 GitHub
git push

# 拉取最新更改
git pull

# 更新子模块（主题）
git submodule update --remote --merge
```

## 完整工作流程

### 1. 创建新文章

```bash
# 创建新文章
hugo new posts/new-article.md

# 编辑文章
nano content/posts/new-article.md

# 本地预览
hugo server -D
```

### 2. 编辑文章

打开 `content/posts/new-article.md`，编辑 Front Matter 和内容：

```markdown
---
title: "新文章标题"
date: 2026-03-17T10:00:00+08:00
draft: false
tags: ["标签1", "标签2"]
categories: ["分类"]
---

文章内容...
```

### 3. 提交并部署

```bash
# 添加更改
git add content/posts/new-article.md

# 提交
git commit -m "Add: 新文章"

# 推送
git push

# GitHub Actions 自动部署
# 访问 https://yourname.github.io/
```

## 常见问题解决

### 1. 404 错误

**症状**：访问网站返回 404

**解决方法**：
- 确保存在 `.nojekyll` 文件
- 检查 GitHub Pages 设置是否选择了 GitHub Actions
- 检查 `hugo.yaml` 中的 `baseURL` 是否正确

### 2. 搜索功能不工作

**症状**：搜索页面可以显示搜索框，但不能搜索

**解决方法**：
- 确保 `hugo.yaml` 中 `outputs.home` 包含 `JSON`：
```yaml
outputs:
  home:
    - HTML
    - RSS
    - JSON
```

### 3. 样式不生效

**症状**：页面样式混乱或主题不显示

**解决方法**：
- 检查主题是否正确安装：`ls themes/PaperMod`
- 确保子模块已初始化：`git submodule update --init --recursive`
- 清除浏览器缓存

### 4. 部署失败

**症状**：GitHub Actions 工作流失败

**解决方法**：
- 查看 Actions 日志中的错误信息
- 检查 Hugo 版本是否兼容
- 确保所有子模块都已正确配置

## 总结

使用 Hugo 搭建个人博客的优势：

- **简单高效**：配置简单，几秒钟即可构建
- **免费托管**：GitHub Pages 免费托管
- **主题丰富**：PaperMod 等精美主题可选
- **响应式设计**：完美适配各种设备
- **搜索功能**：内置强大的搜索功能
- **深色模式**：自动切换深色/浅色主题

现在你已经掌握了完整的 Hugo 博客配置方法，可以开始创作你的博客内容了！

有任何问题欢迎在评论区讨论。