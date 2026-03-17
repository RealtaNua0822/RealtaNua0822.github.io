---
title: "Hugo 入门指南：如何运行 Hugo 生成静态网页"
date: 2026-03-17T01:45:00+08:00
draft: false
tags: ["Hugo", "入门", "教程", "静态网站", "AI生成"]
categories: ["教程"]
---

Hugo 是一个超快的静态网站生成器，但第一次使用时可能会有点困惑。本文将手把手教你如何安装和运行 Hugo，生成你的第一个静态网站。

## 什么是 Hugo？

Hugo 是一个用 Go 语言编写的静态网站生成器，它的特点是：

- **超快速度**：几秒钟内构建整个网站
- **简单易用**：配置简单，上手容易
- **零依赖**：无需数据库，无需后端
- **主题丰富**：有大量精美主题可选

## 安装 Hugo

### 方法 1：使用包管理器（推荐）

**Ubuntu/Debian：**

```bash
# 下载 Hugo
wget https://github.com/gohugoio/hugo/releases/download/v0.147.0/hugo_extended_0.147.0_linux-amd64.deb

# 安装
sudo dpkg -i hugo_extended_0.147.0_linux-amd64.deb

# 验证安装
hugo version
```

**macOS：**

```bash
# 使用 Homebrew
brew install hugo

# 验证安装
hugo version
```

**Windows：**

1. 访问 [Hugo Releases](https://github.com/gohugoio/hugo/releases)
2. 下载 Windows 版本（hugo_extended_0.147.0_windows-amd64.zip）
3. 解压到任意目录
4. 将 hugo.exe 添加到系统 PATH

### 方法 2：使用预编译二进制文件

1. 访问 [Hugo Releases](https://github.com/gohugoio/hugo/releases)
2. 下载对应系统的版本
3. 解压并添加到 PATH

### 验证安装

```bash
hugo version
```

应该看到类似输出：

```
hugo v0.147.0-xxxxxxxx linux/amd64 BuildDate=unknown
```

## 创建新网站

### 方法 1：使用 Hugo 命令创建

```bash
# 创建新网站
hugo new-site myblog

# 进入网站目录
cd myblog
```

这会创建以下目录结构：

```
myblog/
├── archetypes/       # 内容模板
├── assets/           # 资源文件
├── content/          # 博客内容
├── data/             # 数据文件
├── layouts/          # 自定义布局
├── static/           # 静态资源
└── hugo.yaml         # 配置文件
```

### 方法 2：克隆现有项目

如果你想基于现有博客创建：

```bash
# 克隆你的博客仓库
git clone https://github.com/yourname/yourname.github.io.git myblog

# 进入目录
cd myblog

# 安装主题子模块
git submodule update --init --recursive
```

## 安装主题

Hugo 需要主题才能生成美观的网站。

### 使用 Git 子模块安装主题（推荐）

```bash
# 添加 PaperMod 主题
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod

# 更新子模块
git submodule update --init --recursive
```

### 配置主题

编辑 `hugo.yaml`：

```yaml
baseURL: "https://yourname.github.io/"
languageCode: "zh-cn"
title: "我的博客"
theme: ["PaperMod"]
```

## 创建第一篇文章

### 使用 Hugo 命令创建

```bash
# 创建新文章
hugo new posts/my-first-post.md
```

这会创建 `content/posts/my-first-post.md` 文件：

```markdown
---
title: "My First Post"
date: 2026-03-17T01:45:00+08:00
draft: true
---
```

### 编辑文章

打开 `content/posts/my-first-post.md`，修改内容：

```markdown
---
title: "我的第一篇文章"
date: 2026-03-17T01:45:00+08:00
draft: false
tags: ["Hugo", "博客"]
categories: ["技术"]
---

欢迎来到我的博客！

这是我的第一篇文章。
```

**重要：** 将 `draft: true` 改为 `draft: false`，否则文章不会显示。

## 运行 Hugo

### 1. 启动本地服务器（开发模式）

```bash
hugo server
```

或者包含草稿：

```bash
hugo server -D
```

**参数说明：**
- `-D` 或 `--buildDrafts`：包含草稿文章
- `-F` 或 `--buildFuture`：包含未来日期的文章
- `--disableFastRender`：禁用快速渲染
- `--navigateToChanged`：自动导航到修改的页面

### 2. 访问网站

打开浏览器，访问：

```
http://localhost:1313
```

你应该能看到你的博客！

### 3. 热重载功能

Hugo 服务器支持热重载：

- **自动检测文件变化**：当你修改文件时，网站会自动更新
- **无需刷新浏览器**：浏览器会自动刷新
- **实时预览**：边修改边查看效果

## 构建静态网站

### 1. 开发构建（快速）

```bash
hugo
```

这会在 `public/` 目录生成静态网站。

### 2. 生产构建（优化）

```bash
hugo --gc --minify
```

**参数说明：**
- `--gc`：清理未使用的文件
- `--minify`：压缩 HTML、CSS、JS 文件
- `--quiet`：减少输出信息
- `--verbose`：显示详细信息

### 3. 指定 baseURL

```bash
hugo --baseURL "https://yourname.github.io/"
```

这确保网站中的链接是正确的。

## 查看生成的文件

构建完成后，查看 `public/` 目录：

```bash
ls -la public/
```

你应该看到：

```
public/
├── index.html           # 首页
├── posts/               # 文章页面
│   └── my-first-post/
│       └── index.html
├── categories/          # 分类页面
├── tags/                # 标签页面
├── assets/              # CSS、JS 文件
└── index.json           # 搜索索引
```

这些就是可以部署的静态文件！

## 常用命令速查

### 创建内容

```bash
# 创建新文章
hugo new posts/article-title.md

# 创建新页面
hugo new about.md
```

### 本地开发

```bash
# 启动服务器（不包含草稿）
hugo server

# 启动服务器（包含草稿）
hugo server -D

# 指定端口
hugo server --port 8080

# 绑定到所有网络接口
hugo server --bind 0.0.0.0
```

### 构建网站

```bash
# 标准构建
hugo

# 生产构建（优化）
hugo --gc --minify

# 构建到指定目录
hugo -d /path/to/output

# 清理缓存后构建
hugo --cleanDestinationDir
```

### 查看信息

```bash
# 查看版本
hugo version

# 查看配置
hugo config

# 列出所有页面
hugo list all

# 查看帮助
hugo help
```

## 高级功能

### 1. 创建自定义模板

在 `layouts/` 目录创建自定义模板：

```
layouts/
├── _default/
│   └── single.html      # 自定义文章页面
└── partials/
    └── custom.html      # 自定义组件
```

### 2. 使用数据文件

在 `data/` 目录创建数据文件：

```yaml
# data/menu.yaml
main:
  - name: "首页"
    url: "/"
  - name: "关于"
    url: "/about/"
```

在模板中使用：

```html
{{ range .Site.Data.menu.main }}
<a href="{{ .url }}">{{ .name }}</a>
{{ end }}
```

### 3. 创建短代码

在 `layouts/shortcodes/` 目录创建短代码：

```html
<!-- layouts/shortcodes/youtube.html -->
<div class="video-container">
  <iframe src="https://www.youtube.com/embed/{{ .Get 0 }}" frameborder="0"></iframe>
</div>
```

在文章中使用（注意：PaperMod 主题不内置视频短代码，如需嵌入视频需使用自定义短代码或 HTML）：

```markdown
<!-- 示例：使用 HTML 嵌入 YouTube 视频 -->
<iframe width="560" height="315" src="https://www.youtube.com/embed/VIDEO_ID" frameborder="0" allowfullscreen></iframe>
```

## 调试技巧

### 1. 查看详细日志

```bash
hugo server --verbose --logLevel debug
```

### 2. 检查模板错误

```bash
hugo --templateMetrics
```

### 3. 分析页面

```bash
hugo server --disableFastRender
```

### 4. 清除缓存

```bash
hugo --cleanDestinationDir
```

## 常见问题

### 1. Hugo 找不到主题

**问题：** 错误提示找不到主题

**解决：**

```bash
# 确保子模块已初始化
git submodule update --init --recursive

# 检查主题目录是否存在
ls themes/
```

### 2. 文章不显示

**问题：** 创建文章后看不到

**解决：**

```bash
# 检查 draft 设置
# 确保设置为 false
draft: false

# 使用 -D 参数包含草稿
hugo server -D
```

### 3. 样式不加载

**问题：** 网站没有样式

**解决：**

```bash
# 检查主题配置
# 确保 hugo.yaml 中 theme 设置正确
theme: ["PaperMod"]

# 清除缓存
hugo --cleanDestinationDir
```

### 4. 端口被占用

**问题：** 1313 端口被占用

**解决：**

```bash
# 使用其他端口
hugo server --port 8080

# 或者找到占用端口的进程
lsof -i :1313
kill -9 <PID>
```

## 最佳实践

### 1. 使用版本控制

```bash
# 初始化 Git 仓库
git init

# 添加 .gitignore
echo "public/" >> .gitignore

# 提交
git add .
git commit -m "Initial commit"
```

### 2. 使用草稿功能

在开发时使用草稿：

```markdown
---
draft: true
---
```

完成后再发布：

```markdown
---
draft: false
---
```

### 3. 本地预览

```bash
# 总是先本地预览
hugo server -D

# 确认无误后再构建
hugo --gc --minify
```

### 4. 定期更新 Hugo

```bash
# 检查新版本
hugo version

# 访问 GitHub Releases 下载新版本
# https://github.com/gohugoio/hugo/releases
```

## 下一步

现在你已经学会了：

- ✅ 安装 Hugo
- ✅ 创建新网站
- ✅ 安装主题
- ✅ 创建文章
- ✅ 运行本地服务器
- ✅ 构建静态网站

接下来你可以：

1. **学习 Markdown 语法**：撰写更好的文章
2. **自定义主题**：让博客更个性化
3. **部署到 GitHub Pages**：让全世界访问你的博客
4. **添加评论系统**：与读者互动
5. **集成分析工具**：了解访问情况

## 总结

Hugo 是一个强大而简单的静态网站生成器。通过本文，你已经掌握了：

- 基本的安装和配置
- 创建和管理内容
- 本地开发和预览
- 构建静态网站

现在你可以开始创作你的博客内容了！

记住：**先本地预览，再构建部署**。这样可以避免很多不必要的问题。

如果你遇到任何问题，查看 Hugo 官方文档：https://gohugo.io/documentation/

祝你使用 Hugo 愉快！