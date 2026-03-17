---
title: "GitHub Pages 404 错误终极解决方案：.nojekyll 文件的奥秘"
date: 2026-03-17T03:00:00+08:00
draft: false
tags: ["GitHub Pages", "Hugo", "404错误", "故障排除", "教程", "AI生成"]
categories: ["教程"]
---

你是否遇到过这种情况：辛辛苦苦配置好 Hugo 博客，推送到 GitHub Pages 后，访问网站却只看到 404 Not Found？本文将深入剖析这个问题，并揭示 .nojekyll 文件如何成为解决问题的关键。

## 问题描述

### 典型症状

你按照教程完成了以下步骤：

1. ✅ 创建了 Hugo 博客
2. ✅ 配置了 GitHub Actions
3. ✅ 推送到 GitHub
4. ✅ GitHub Actions 显示部署成功
5. ❌ 访问网站时返回 404

**令人困惑的是：**
- GitHub Pages 界面显示"Your site is live at https://yourname.github.io/"
- Actions 日志显示"Deployment successful"
- 但是访问网站却看到 404

### 真实案例

当我第一次搭建这个博客时，就遇到了这个问题：

```bash
# 配置看起来都很完美
$ hugo config
baseURL: https://realtanua0822.github.io/
languageCode: zh-cn
title: 我的博客
theme: PaperMod

# 推送到 GitHub
$ git push
# GitHub Actions 运行成功

# 访问网站
$ curl -I https://realtanua0822.github.io/
HTTP/2 404
```

问题在哪里？

## 根本原因分析

### GitHub Pages 的默认行为

GitHub Pages 有一个"隐藏"的默认行为：**自动使用 Jekyll 处理内容**。

即使你的项目中有自定义的 GitHub Actions 工作流，GitHub Pages 在某些情况下仍然会尝试使用 Jekyll 来处理你的文件。

### Jekyll 是什么？

Jekyll 是 GitHub Pages 的默认静态网站生成器，它的工作流程是：

```
Markdown 文件 → Jekyll 处理 → HTML 文件 → GitHub Pages 托管
```

### 为什么会出现 404？

当你使用 Hugo 而不是 Jekyll 时：

```
你的流程：
Markdown → Hugo 生成 HTML → public/ 目录 → GitHub Pages

GitHub Pages 期望的流程：
Markdown → Jekyll 处理 → _site/ 目录 → GitHub Pages
```

**冲突点：**

1. **路径差异**
   - Hugo 生成的文件在 `public/` 目录
   - Jekyll 期望文件在 `_site/` 目录
   - GitHub Pages 找不到正确的文件位置

2. **文件处理冲突**
   - Jekyll 会处理所有 Markdown 文件
   - Hugo 已经将 Markdown 转换为 HTML
   - 重复处理导致内容损坏

3. **特殊目录处理**
   - Jekyll 会忽略以下划线开头的目录（如 `_posts`）
   - Hugo 的主题文件可能在 `_layouts` 等目录
   - 这些文件被 Jekyll 忽略，导致功能缺失

### 实际发生的流程

当你没有 `.nojekyll` 文件时：

```
1. 你推送代码
   ↓
2. GitHub Pages 检测到有 GitHub Actions 工作流
   ↓
3. GitHub Actions 运行，Hugo 生成网站到 public/
   ↓
4. GitHub Pages 接收到 public/ 目录
   ↓
5. 但 GitHub Pages 的 Jekyll 处理器启动
   ↓
6. Jekyll 尝试处理这些文件
   ↓
7. 由于不是 Jekyll 格式，处理失败
   ↓
8. 最终返回 404
```

## .nojekyll 文件的神奇作用

### 什么是 .nojekyll？

`.nojekyll` 是一个**空文件**，文件名就是其全部内容。

它是一个特殊的标记文件，告诉 GitHub Pages："**请不要使用 Jekyll 处理我的网站**"。

### .nojekyll 的工作原理

当你添加 `.nojekyll` 文件后：

```
1. 你推送代码（包含 .nojekyll 文件）
   ↓
2. GitHub Pages 检测到 .nojekyll 文件
   ↓
3. GitHub Pages 跳过 Jekyll 处理步骤
   ↓
4. GitHub Actions 运行，Hugo 生成网站到 public/
   ↓
5. GitHub Pages 直接托管 public/ 目录中的文件
   ↓
6. 网站正常显示！✅
```

### .nojekyll 文件的内容

```bash
# 创建 .nojekyll 文件
touch .nojekyll

# 查看文件内容（是空的）
$ cat .nojekyll
$ wc -l .nojekyll
0 .nojekyll
```

**是的，这个文件完全是空的！**

它的存在本身就是信息。

## 完整的解决过程

### 步骤 1：诊断问题

首先确认问题：

```bash
# 检查 GitHub Pages 状态
# 访问 GitHub 仓库 → Settings → Pages
# 查看部署状态

# 检查 Actions 日志
# 访问 GitHub 仓库 → Actions → 查看工作流运行记录

# 检查网站是否可以访问
$ curl -I https://yourname.github.io/
# 如果返回 404，说明有问题
```

### 步骤 2：检查当前状态

```bash
# 检查是否有 .nojekyll 文件
$ ls -la .nojekyll
ls: 无法访问 '.nojekyll': 没有那个文件或目录

# 确认问题：缺少 .nojekyll 文件
```

### 步骤 3：创建 .nojekyll 文件

```bash
# 创建空文件
touch .nojekyll

# 验证文件已创建
$ ls -la .nojekyll
-rw-r--r-- 1 user user 0 Mar 17 03:00 .nojekyll
```

### 步骤 4：提交并推送

```bash
# 添加文件到 Git
git add .nojekyll

# 提交更改
git commit -m "Add .nojekyll to disable Jekyll processing for Hugo"

# 推送到 GitHub
git push
```

### 步骤 5：等待部署

```bash
# GitHub Actions 会自动触发

# 查看 Actions 运行状态
# 访问 https://github.com/yourname/yourname.github.io/actions
```

### 步骤 6：验证修复

```bash
# 等待 1-2 分钟后，检查网站
$ curl -I https://yourname.github.io/
HTTP/2 200
Content-Type: text/html

# 成功！返回 200 OK
```

## 为什么必须使用 .nojekyll？

### 其他方法的局限性

你可能想问："为什么不直接修改 GitHub Pages 设置？"

**问题：**
- GitHub Pages 设置可能不正确或不可靠
- 即使设置了 GitHub Actions，Jekyll 可能仍然会干扰
- 某些情况下，GitHub Pages 会自动恢复默认行为

**.nojekyll 的优势：**
- ✅ 明确指示 GitHub Pages 禁用 Jekyll
- ✅ 文件本身是版本控制的，不会被意外删除
- ✅ 适用于所有情况，100% 可靠
- ✅ 不依赖 GitHub Pages UI 设置

### 兼容性考虑

`.nojekyll` 文件适用于：

- ✅ Hugo
- ✅ Hexo
- ✅ Jekyll（当你要使用自定义构建时）
- ✅ 任何非 Jekyll 的静态网站生成器
- ✅ 纯静态 HTML 网站

### 官方推荐

GitHub 官方文档明确指出：

> "If you're using a generator other than Jekyll, create a .nojekyll file in the root of your repository."

## 深入理解 Jekyll 处理机制

### Jekyll 的文件处理规则

Jekyll 对文件有以下特殊处理：

1. **忽略下划线开头的目录**
   ```
   _layouts/
   _includes/
   _posts/
   _data/
   ```
   这些目录不会被复制到输出。

2. **处理 Markdown 文件**
   所有 `.md` 文件都会被转换为 HTML。

3. **处理 Front Matter**
   包含 Front Matter 的文件会被 Jekyll 处理。

4. **忽略特定文件**
   `.gitignore` 风格的忽略规则。

### 对 Hugo 的影响

当 Jekyll 处理 Hugo 生成的文件时：

```
Hugo 生成的结构：
public/
├── index.html
├── posts/
│   └── article/
│       └── index.html
└── _internal/
    └── some-file.html

Jekyll 处理后：
public/
├── index.html
├── posts/
│   └── article/
│       └── index.html
# _internal/ 被忽略了！
```

这导致某些功能文件丢失，网站出现 404。

## 最佳实践

### 1. 总是包含 .nojekyll 文件

对于所有非 Jekyll 项目，都应该包含 `.nojekyll` 文件：

```bash
# 在项目初始化时就创建
touch .nojekyll
git add .nojekyll
git commit -m "Add .nojekyll to disable Jekyll"
```

### 2. 将 .nojekyll 添加到模板

如果你有项目模板，确保包含 `.nojekyll`：

```bash
# 在项目模板目录中
template/
├── .nojekyll
├── .gitignore
├── hugo.yaml
└── ...
```

### 3. 检查清单

部署前检查：

- [ ] `.nojekyll` 文件存在于项目根目录
- [ ] `.nojekyll` 文件已提交到 Git
- [ ] `.nojekyll` 文件在 .gitignore 中**不**被忽略
- [ ] GitHub Actions 工作流配置正确
- [ ] `baseURL` 配置正确

### 4. 常见错误

**错误 1：忘记提交 .nojekyll**

```bash
# 创建了文件但忘记提交
touch .nojekyll
git add .gitignore  # 只添加了其他文件
git commit -m "Add config"
git push
# .nojekyll 没有被推送，问题依旧
```

**正确做法：**

```bash
touch .nojekyll
git add .nojekyll
git commit -m "Add .nojekyll"
git push
```

**错误 2：在 .gitignore 中忽略了 .nojekyll**

```bash
# .gitignore
.nojekyll  # 错误！这会阻止提交
```

**正确做法：**

```bash
# .gitignore
# 不要忽略 .nojekyll
```

**错误 3：文件名拼写错误**

```bash
# 错误
touch .nojekill
touch .no-jekyll

# 正确
touch .nojekyll
```

## 故障排除流程

### 问题：仍然返回 404

即使添加了 `.nojekyll`，仍然 404？

**检查清单：**

1. **验证文件存在**
   ```bash
   $ ls -la .nojekyll
   -rw-r--r-- 1 user user 0 Mar 17 03:00 .nojekyll
   ```

2. **验证文件已提交**
   ```bash
   $ git ls-files .nojekyll
   .nojekyll
   ```

3. **验证文件已推送**
   ```bash
   # 访问 GitHub 仓库，查看 .nojekyll 是否存在
   ```

4. **检查 GitHub Pages 设置**
   ```
   Settings → Pages → Build and deployment → Source
   应该选择 "GitHub Actions"
   ```

5. **查看 Actions 日志**
   ```
   Actions → Deploy Hugo site to Pages → 查看详细日志
   ```

### 问题：部分功能正常，部分 404

可能的原因：

- Jekyll 仍然处理了某些文件
- 某些文件被 Jekyll 忽略（如下划线开头的目录）

**解决方案：**

```bash
# 确保 .nojekyll 文件在项目根目录
# 不要放在子目录中
touch .nojekyll
```

## 其他相关文件

### .gitignore 配置

确保 `.gitignore` 不会阻止 `.nojekyll` 提交：

```gitignore
# 忽略生成的文件
public/

# 忽略临时文件
*.swp
*.swo
*~

# 不要忽略 .nojekyll！
# .nojekyll  # 注释掉或删除这一行
```

### GitHub Actions 配置

确保 GitHub Actions 工作流正确：

```yaml
name: Deploy Hugo site to Pages

on:
  push:
    branches: ["main"]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: '0.147.0'
          extended: true

      - name: Build
        run: hugo --gc --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

## 理论总结

### 核心概念

1. **GitHub Pages 默认使用 Jekyll**
   - 这是历史遗留的设计
   - 对 Jekyll 项目很方便
   - 但对其他生成器造成冲突

2. **.nojekyll 是解决方案**
   - 简单、明确、可靠
   - 官方推荐的解决方案
   - 适用于所有非 Jekyll 项目

3. **版本控制的重要性**
   - `.nojekyll` 应该提交到 Git
   - 确保所有环境一致
   - 避免配置差异

### 设计哲学

`.nojekyll` 体现了 Unix 哲学：

- **简单**：一个空文件解决问题
- **明确**：文件名即功能
- **可靠**：不依赖复杂配置
- **可扩展**：适用于多种场景

## 实战案例回顾

### 我的博客解决过程

回到我自己的博客问题：

```bash
# 初始状态
$ ls -la .nojekyll
ls: 无法访问 '.nojekyll': 没有那个文件或目录

# 创建文件
$ touch .nojekyll

# 提交
$ git add .nojekyll
$ git commit -m "Add .nojekyll to disable Jekyll processing for Hugo"

# 推送
$ git push

# 等待部署
# GitHub Actions 自动运行

# 验证
$ curl -I https://realtanua0822.github.io/
HTTP/2 200
Content-Type: text/html; charset=utf-8
```

**成功！** 问题解决。

### 时间线

```
T0: 配置 Hugo 博客
T1: 推送到 GitHub
T2: GitHub Actions 运行成功
T3: 访问网站 → 404 ❌
T4: 诊断问题 → 缺少 .nojekyll
T5: 创建 .nojekyll 文件
T6: 推送更改
T7: GitHub Actions 重新部署
T8: 访问网站 → 200 OK ✅
```

## 扩展阅读

### 相关资源

- [GitHub Pages 官方文档](https://docs.github.com/en/pages)
- [Hugo 托管在 GitHub Pages](https://gohugo.io/hosting-and-deployment/hosting-on-github/)
- [Jekyll 官方文档](https://jekyllrb.com/)

### 相关问题

- **如何自定义 GitHub Pages 设置？**
  - Settings → Pages → Build and deployment

- **如何使用自定义域名？**
  - Settings → Pages → Custom domain

- **如何启用 HTTPS？**
  - GitHub Pages 自动为自定义域名提供 HTTPS

## 总结

### 关键要点

1. **404 问题的根源**
   - GitHub Pages 默认使用 Jekyll
   - Jekyll 与 Hugo 等其他生成器冲突

2. **.nojekyll 的作用**
   - 禁用 Jekyll 处理
   - 让 GitHub Pages 直接托管静态文件
   - 简单、可靠、官方推荐

3. **最佳实践**
   - 总是包含 `.nojekyll` 文件
   - 确保文件已提交到 Git
   - 不要在 .gitignore 中忽略

4. **故障排除**
   - 检查文件是否存在
   - 检查文件是否已提交
   - 检查 GitHub Pages 设置
   - 查看 Actions 日志

### 经验教训

- **不要忽视"小"文件**：`.nojekyll` 虽然是空文件，但至关重要
- **理解默认行为**：GitHub Pages 的 Jekyll 默认行为可能造成问题
- **官方文档很重要**：GitHub 官方明确推荐使用 `.nojekyll`
- **版本控制一切**：配置文件应该提交到 Git

### 最终建议

对于任何使用 Hugo、Hexo 或其他静态网站生成器的项目：

```bash
# 项目初始化时立即创建
touch .nojekyll
git add .nojekyll
git commit -m "Add .nojekyll to disable Jekyll processing"
```

这样可以避免从一开始就遇到 404 问题。

---

**记住：一个简单的 `.nojekyll` 文件，就能解决 GitHub Pages 404 的终极问题！**

希望这篇文章帮助你理解了 `.nojekyll` 的重要性和工作原理。如果你遇到类似问题，按照本文的步骤操作，应该能够顺利解决。

祝你使用 Hugo 和 GitHub Pages 愉快！