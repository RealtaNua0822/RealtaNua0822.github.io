---
title: "Hugo Shortcodes 完全指南：从入门到精通"
date: 2026-03-17T03:00:00+08:00
draft: false
tags: ["Hugo", "Shortcodes", "教程", "开发"]
categories: ["教程"]
---

Shortcodes 是 Hugo 最强大的功能之一，它允许你在 Markdown 文章中插入复杂的内容和功能。本文将详细介绍 PaperMod 主题的内置短代码，以及如何创建和使用自定义短代码。

## 什么是 Shortcode？

Shortcode 是 Hugo 提供的一种机制，让你能够在 Markdown 文章中插入预定义的 HTML 组件。它类似于 WordPress 的简码，但更加强大和灵活。

### 为什么使用 Shortcode？

- **简化复杂 HTML**：无需手写复杂的 HTML 代码
- **保持一致性**：确保相同类型的内容具有统一的样式
- **易于维护**：修改短代码模板即可更新所有使用该短代码的内容
- **扩展 Markdown**：弥补 Markdown 在功能上的不足

## PaperMod 主题内置的 Shortcodes

PaperMod 主题提供了多个实用的内置短代码，让我们一一了解。

### 1. Collapse（折叠内容）

折叠短代码可以创建可展开/折叠的内容块，非常适合放置大量细节信息或可选内容。

#### 基本用法

```markdown
{{</* collapse summary="点击查看详情" */>}}
这里是折叠的内容...
{{</* /collapse */>}}
```

#### 实际效果

{{< collapse summary="点击查看详情" >}}
这里是折叠的内容，只有点击标题后才会显示。
这样可以保持页面的整洁，避免一开始就展示太多信息。
{{< /collapse >}}

#### 默认展开

```markdown
{{</* collapse summary="默认展开的内容" openByDefault=true */>}}
这个内容默认就是展开的
{{</* /collapse */>}}
```

#### 实际效果

{{< collapse summary="默认展开的内容" openByDefault=true >}}
这个内容默认就是展开的
{{< /collapse >}}

#### 使用场景

- 技术文档中的详细信息
- 需要用户主动查看的内容
- 可能影响页面布局的大量内容
- 可选的补充信息

### 2. Figure（图片展示）

Figure 短代码提供了更强大的图片展示功能，支持标题、链接、对齐等多种选项。

#### 基本用法

```markdown
{{</* figure src="/images/example.jpg" title="图片标题" caption="图片描述" */>}}
```

#### 带链接的图片

```markdown
{{</* figure src="/images/example.jpg" link="https://example.com" target="_blank" title="点击查看大图" caption="点击图片跳转到外部链接" */>}}
```

#### 居中对齐

```markdown
{{</* figure src="/images/example.jpg" align="center" title="居中图片" */>}}
```

#### 完整参数

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `src` | 图片路径 | 必填 |
| `title` | 图片标题 | 无 |
| `caption` | 图片描述 | 无 |
| `alt` | 替代文本 | caption 的值 |
| `link` | 链接地址 | 无 |
| `target` | 链接目标 | `_self` |
| `rel` | 链接关系 | 无 |
| `align` | 对齐方式 | `left` |
| `class` | 自定义 CSS 类 | 无 |
| `width` | 图片宽度 | 原始宽度 |
| `height` | 图片高度 | 原始高度 |
| `attr` | 附加信息 | 无 |
| `attrlink` | 附加信息链接 | 无 |

#### 使用场景

- 展示带有说明的图片
- 创建可点击的图片链接
- 添加版权信息或图片来源
- 响应式图片展示

### 3. inTextImg（文中图片）

inTextImg 短代码用于在文本中插入小型图标或内联图片。

#### 基本用法

```markdown
这是一个 {{</* inTextImg url="/icons/info.png" height="15" alt="信息图标" */>}} 信息图标
```

#### 参数说明

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `url` | 图片路径 | 必填 |
| `height` | 图片高度（单位：px） | `15` |
| `alt` | 替代文本 | 无 |

#### 使用场景

- 在文本中插入图标
- 添加表情符号
- 标记重要信息

### 4. ltr/rtl（文本方向）

这两个短代码用于控制文本的显示方向。

#### ltr（从左到右）

```markdown
{{</* ltr */>}}
这是从左到右显示的文本
{{</* /ltr */>}}
```

#### rtl（从右到左）

```markdown
{{</* rtl */>}}
هذا نص يظهر من اليمين إلى اليسار
{{</* /rtl */>}}
```

#### 使用场景

- 多语言博客
- 需要显示不同方向文字的内容
- 特殊排版需求

### 5. rawhtml（原始 HTML）

允许在 Markdown 中插入原始 HTML 代码。

#### 基本用法

```markdown
{{</* rawhtml */>}}
<div class="custom-component">
  这是原始 HTML 内容
</div>
{{</* /rawhtml */>}}
```

#### 注意事项

- 只有当 `unsafe` 选项启用时才能使用
- 谨慎使用，确保 HTML 代码安全
- 优先考虑使用 shortcodes

## 自定义 Shortcodes

除了内置短代码，你还可以创建自己的短代码。以下是一些实用的自定义短代码示例。

### 1. Alert（警告框）

用于显示警告、提示信息。

#### Info（信息）

{{< info >}}
这是一条信息提示。用于提供额外的背景信息或说明。
{{< /info >}}

#### Warning（警告）

{{< alert >}}
这是一条警告信息。用于提醒用户注意潜在的问题或风险。
{{< /alert >}}

#### Success（成功）

{{< success >}}
操作成功完成！用于确认用户操作的结果。
{{< /success >}}

#### Note（笔记）

{{< note >}}
这是一条笔记。用于记录重要的提示或备忘信息。
{{< /note >}}

### 2. Button（按钮）

创建可点击的按钮链接。

#### 基本用法

```markdown
{{</* button url="https://example.com" text="访问网站" */>}}
```

#### 不同样式

主要按钮：
{{< button url="https://github.com" text="访问 GitHub" >}}

次要按钮：
{{< button url="https://example.com" text="了解更多" class="btn-secondary" >}}

成功按钮：
{{< button url="https://example.com" text="下载文件" class="btn-success" >}}

危险按钮：
{{< button url="https://example.com" text="删除内容" class="btn-danger" >}}

#### 参数说明

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `url` | 链接地址 | 必填 |
| `text` | 按钮文字 | `点击这里` |
| `class` | 按钮样式 | `btn-primary` |

## 创建自定义 Shortcode

创建自定义短代码非常简单，只需要在 `layouts/shortcodes/` 目录下创建 HTML 文件即可。

### 步骤 1：创建目录结构

```bash
mkdir -p layouts/shortcodes
```

### 步骤 2：创建短代码文件

例如创建一个 `greet.html` 文件：

```html
<!-- layouts/shortcodes/greet.html -->
<div class="greeting">
  <h2>{{ .Get "name" | default "朋友" }}，你好！</h2>
  {{ .Inner | markdownify }}
</div>
```

### 步骤 3：使用短代码

```markdown
{{</* greet name="小明" */>}}
欢迎来到我的博客！
{{</* /greet */>}}
```

### 短代码语法

#### 获取参数

```go
{{ .Get "paramName" }}
```

#### 获取带默认值的参数

```go
{{ .Get "paramName" | default "defaultValue" }}
```

#### 获取内部内容

```go
{{ .Inner }}
```

#### Markdown 渲染内部内容

```go
{{ .Inner | markdownify }}
```

#### 条件判断

```go
{{ if .Get "showTitle" }}
  <h1>标题</h1>
{{ end }}
```

#### 循环

```go
{{ range .Get "items" }}
  <li>{{ . }}</li>
{{ end }}
```

## 实用示例

### 示例 1：引用块

创建带有图标的引用块：

```html
<!-- layouts/shortcodes/quote.html -->
<blockquote class="custom-quote">
  <p>{{ .Inner | markdownify }}</p>
  {{ with .Get "author" }}
    <footer>— {{ . }}</footer>
  {{ end }}
</blockquote>
```

使用：

```markdown
{{</* quote author="Albert Einstein" */>}}
想象力比知识更重要。
{{</* /quote */>}}
```

### 示例 2：代码提示

创建带有语言标识的代码提示：

```html
<!-- layouts/shortcodes/codehint.html -->
<div class="code-hint">
  <span class="language-badge">{{ .Get "lang" }}</span>
  {{ .Inner }}
</div>
```

### 示例 3：步骤列表

创建分步骤的指导：

```html
<!-- layouts/shortcodes/steps.html -->
<ol class="steps">
  {{ .Inner }}
</ol>
```

```html
<!-- layouts/shortcodes/step.html -->
<li class="step-item">
  <h3>{{ .Get "title" }}</h3>
  {{ .Inner | markdownify }}
</li>
```

使用：

```markdown
{{</* steps */>}}
{{</* step title="准备工作" */>}}
确保你已安装 Hugo 和 Git。
{{</* /step */>}}
{{</* step title="创建站点" */>}}
运行 `hugo new-site myblog` 命令。
{{</* /step */>}}
{{</* step title="添加内容" */>}}
创建你的第一篇文章。
{{</* /step */>}}
{{</* /steps */>}}
```

## 最佳实践

### 1. 命名规范

- 使用小写字母和连字符：`my-shortcode`
- 避免使用特殊字符
- 选择描述性的名称

### 2. 参数设计

- 提供合理的默认值
- 使用清晰的参数名称
- 支持可选参数

### 3. 安全考虑

- 对用户输入进行适当转义
- 避免直接执行未验证的代码
- 使用 `markdownify` 而不是直接输出

### 4. 文档编写

- 为每个短代码编写使用说明
- 提供示例代码
- 说明参数含义和默认值

### 5. 性能优化

- 避免在短代码中进行复杂计算
- 使用缓存机制
- 最小化外部依赖

## 调试技巧

### 1. 查看可用短代码

运行以下命令查看所有可用的短代码：

```bash
hugo list all
```

### 2. 测试短代码

创建测试页面，逐步测试短代码功能：

```markdown
---
title: "Shortcode 测试"
draft: true
---

测试各种短代码...
```

### 3. 检查模板错误

如果短代码不工作，检查以下几点：

- 文件路径是否正确
- 文件名是否匹配
- 语法是否正确
- 参数是否缺失

### 4. 使用调试模式

```bash
hugo server --disableFastRender
```

## 常见问题

### Q1: Shortcode 不显示？

检查：
- 短代码名称是否正确
- 是否在代码块中（代码块中的短代码会被转义）
- 文件权限是否正确

### Q2: 如何禁用短代码解析？

使用注释语法：

```markdown
{{</* shortcode */>}}
```

### Q3: 可以嵌套短代码吗？

可以，但需要注意闭合顺序：

```markdown
{{</* outer */>}}
  {{</* inner */>}}
  {{</* /inner */>}}
{{</* /outer */>}}
```

### Q4: 如何传递复杂参数？

对于复杂参数，考虑使用 Front Matter 或 JSON 格式：

```markdown
{{</* myshortcode data='{"key": "value"}' */>}}
```

## 总结

通过本文，你学会了：

- ✅ PaperMod 主题内置短代码的使用
- ✅ 如何创建自定义短代码
- ✅ 短代码的语法和参数处理
- ✅ 实用的短代码示例
- ✅ 最佳实践和调试技巧

**记住：** 短代码是 Hugo 的强大功能，合理使用可以大大提升你的写作效率和博客质量。

## 参考资料

- [Hugo 官方文档 - Shortcodes](https://gohugo.io/content-management/shortcodes/)
- [PaperMod 主题文档](https://github.com/adityatelange/hugo-PaperMod)
- [Hugo 模板函数](https://gohugo.io/functions/)

---

**下一步：**
- 尝试创建你自己的短代码
- 为博客添加更多交互功能
- 探索 Hugo 主题的高级功能

祝你使用愉快！