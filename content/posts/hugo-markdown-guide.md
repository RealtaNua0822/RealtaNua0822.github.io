---
title: "Hugo Markdown 完全指南：从入门到精通"
date: 2026-03-17T02:00:00+08:00
draft: false
tags: ["Hugo", "Markdown", "教程", "写作"]
categories: ["教程"]
---

Markdown 是 Hugo 博客的核心，掌握 Markdown 语法是写好博客的基础。本文将详细介绍 Hugo 中使用的 Markdown 语法，从基础到高级，帮助你写出漂亮的文章。

## 什么是 Markdown？

Markdown 是一种轻量级标记语言，它的目标是：

- **易读易写**：纯文本格式，易于阅读和编辑
- **可转换为 HTML**：可以转换为 HTML 等格式
- **广泛支持**：大多数博客平台都支持

Hugo 使用 [Goldmark](https://github.com/yuin/goldmark) 作为 Markdown 解析器，支持标准 Markdown 和扩展语法。

## Front Matter（前置元数据）

每篇 Hugo 文章都必须以 Front Matter 开头，包含文章的元数据。

### YAML 格式（推荐）

```markdown
---
title: "文章标题"
date: 2026-03-17T02:00:00+08:00
draft: false
tags: ["标签1", "标签2"]
categories: ["分类"]
description: "文章描述"
---
```

### TOML 格式

```toml
+++
title = "文章标题"
date = 2026-03-17T02:00:00+08:00
draft = false
tags = ["标签1", "标签2"]
categories = ["分类"]
description = "文章描述"
+++
```

### 常用 Front Matter 字段

| 字段 | 类型 | 说明 | 示例 |
|------|------|------|------|
| `title` | string | 文章标题 | `"我的标题"` |
| `date` | string | 发布日期 | `"2026-03-17T02:00:00+08:00"` |
| `draft` | boolean | 是否为草稿 | `true` / `false` |
| `tags` | array | 文章标签 | `["Hugo", "教程"]` |
| `categories` | array | 文章分类 | `["技术"]` |
| `description` | string | 文章描述 | `"这篇文章是关于..."` |
| `featuredImage` | string | 特色图片 | `"/images/post.jpg"` |
| `slug` | string | URL 别名 | `"my-custom-slug"` |
| `url` | string | 自定义 URL | `"/custom/path/"` |
| `weight` | number | 排序权重 | `10` |

## 基础 Markdown 语法

### 1. 标题

```markdown
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

**效果：**

# 一级标题
## 二级标题
### 三级标题
...

**最佳实践：**
- 一篇文章只使用一个一级标题（文章标题）
- 使用二级标题作为主要章节
- 使用三级标题作为子章节

### 2. 段落

```markdown
这是第一个段落。

这是第二个段落。

空行会创建新段落。
```

**注意：** Markdown 中的段落之间需要空一行。

### 3. 强调文本

```markdown
*斜体* 或 _斜体_
**粗体** 或 __粗体__
***粗斜体*** 或 ___粗斜体___
```

**效果：**

*斜体* 或 _斜体_
**粗体** 或 __粗体__
***粗斜体*** 或 ___粗斜体___

### 4. 分隔线

```markdown
---

***

___
```

**效果：**

---

***

___

### 5. 列表

**无序列表：**

```markdown
- 项目 1
- 项目 2
  - 子项目 2.1
  - 子项目 2.2
- 项目 3
```

**效果：**

- 项目 1
- 项目 2
  - 子项目 2.1
  - 子项目 2.2
- 项目 3

**有序列表：**

```markdown
1. 第一步
2. 第二步
3. 第三步
```

**效果：**

1. 第一步
2. 第二步
3. 第三步

### 6. 链接

```markdown
[链接文本](https://example.com)

[带标题的链接](https://example.com "悬停显示的标题")

[相对链接](/about/)
```

**效果：**

[链接文本](https://example.com)

[带标题的链接](https://example.com "悬停显示的标题")

[相对链接](/about/)

### 7. 图片

```markdown
![图片描述](/images/image.jpg)

![带标题的图片](/images/image.jpg "图片标题")
```

**最佳实践：**
- 将图片放在 `static/` 目录下
- 使用相对路径
- 添加描述性文本

### 8. 代码

**行内代码：**

```markdown
使用 `code` 命令
```

**效果：**

使用 `code` 命令

**代码块：**

````markdown
```javascript
function hello() {
  console.log("Hello, World!");
}
```
````

**效果：**

```javascript
function hello() {
  console.log("Hello, World!");
}
```

**指定语言高亮：**

````markdown
```python
def hello():
    print("Hello, World!")
```
````

**效果：**

```python
def hello():
    print("Hello, World!")
```

### 9. 引用

```markdown
> 这是一段引用
>
> > 这是嵌套引用
```

**效果：**

> 这是一段引用
>
> > 这是嵌套引用

### 10. 表格

```markdown
| 列1 | 列2 | 列3 |
|-----|-----|-----|
| 数据1 | 数据2 | 数据3 |
| 数据4 | 数据5 | 数据6 |
```

**效果：**

| 列1 | 列2 | 列3 |
|-----|-----|-----|
| 数据1 | 数据2 | 数据3 |
| 数据4 | 数据5 | 数据6 |

**对齐方式：**

```markdown
| 左对齐 | 居中 | 右对齐 |
|:-------|:----:|-------:|
| 文本  | 文本  | 文本   |
```

**效果：**

| 左对齐 | 居中 | 右对齐 |
|:-------|:----:|-------:|
| 文本  | 文本  | 文本   |

## Hugo 扩展语法

### 1. 任务列表

```markdown
- [x] 已完成的任务
- [ ] 未完成的任务
- [ ] 另一个未完成的任务
```

**效果：**

- [x] 已完成的任务
- [ ] 未完成的任务
- [ ] 另一个未完成的任务

### 2. 自动链接

```markdown
https://github.com
```

**效果：**

https://github.com

### 3. 删除线

```markdown
~~删除的文本~~
```

**效果：**

~~删除的文本~~

### 4. 脚注

```markdown
这是一段文字[^1]。

[^1]: 这是脚注的内容
```

**效果：**

这是一段文字[^1]。

[^1]: 这是脚注的内容

### 5. 定义列表

```markdown
术语 1
:   定义 1

术语 2
:   定义 2
```

**效果：**

术语 1
:   定义 1

术语 2
:   定义 2

## Hugo 短代码

Hugo 提供了强大的短代码功能，可以插入复杂的内容。

### 1. 图片短代码

```markdown
{{< figure src="/images/image.jpg" title="图片标题" caption="图片描述" >}}
```

### 2. YouTube 视频

```markdown
{{< youtube dQw4w9WgXcQ >}}
```

### 3. Tweet

```markdown
{{< tweet user="twitterdev" id="1234567890" >}}
```

### 4. Spotify

```markdown
{{< spotify track="4uLU6hMCjMI75M1A2tKUQC" >}}
```

### 5. Instagram

```markdown
{{< instagram BWNjjyYFYPP >}}
```

### 6. 自定义短代码

创建 `layouts/shortcodes/notice.html`：

```html
<div class="notice">
  {{ .Inner }}
</div>
```

使用：

```markdown
{{< notice >}}
这是一个自定义通知
{{< /notice >}}
```

## 高级技巧

### 1. HTML 嵌入

Markdown 支持 HTML：

```markdown
<div class="custom-box">
  这是 HTML 内容
</div>
```

### 2. 内联样式

```markdown
<span style="color: red;">红色文字</span>
```

**效果：**

<span style="color: red;">红色文字</span>

### 3. 转义字符

如果要显示 Markdown 特殊字符，使用反斜杠：

```markdown
\*不是斜体\*
\**不是粗体\**
```

**效果：**

\*不是斜体\*
\**不是粗体\**

### 4. Emoji

Hugo 支持 Emoji：

```markdown
:smile: :heart: :rocket:
```

**效果：**

:smile: :heart: :rocket:

### 5. 数学公式

使用 KaTeX 或 MathJax：

```markdown
行内公式：$E = mc^2$

块级公式：
$$
\int_0^\infty e^{-x^2} dx = \frac{\sqrt{\pi}}{2}
$$
```

**效果：**

行内公式：$E = mc^2$

块级公式：
$$
\int_0^\infty e^{-x^2} dx = \frac{\sqrt{\pi}}{2}
$$

## 写作最佳实践

### 1. 结构清晰

```markdown
---
title: "文章标题"
---

## 引言

简短的介绍

## 主要内容

### 子主题 1

内容...

### 子主题 2

内容...

## 结论

总结...
```

### 2. 使用描述性标题

```markdown
❌ 不好的标题
# 第一章

✅ 好的标题
# Hugo 入门：从零开始搭建博客
```

### 3. 合理使用列表

```markdown
❌ 不好的写法
首先，然后，最后，最后。

✅ 好的写法
1. 第一步
2. 第二步
3. 第三步
```

### 4. 添加代码示例

```markdown
```bash
# 安装 Hugo
brew install hugo

# 创建新网站
hugo new-site myblog
```
```

### 5. 使用图片辅助说明

```markdown
![配置界面](/images/config.png)

如图所示，配置文件的路径是...
```

### 6. 保持段落简洁

```markdown
❌ 不好的段落
这是一个很长的段落，包含了很多内容，读者很难快速理解要点，应该拆分成多个段落。

✅ 好的段落
这是一个简洁的段落。

每个段落只表达一个观点。

这样更容易阅读。
```

## 常见问题

### 1. 如何换行？

```markdown
# 方法 1：空行（推荐）
第一段

第二段

# 方法 2：两个空格
第一段  
第二段
```

### 2. 如何创建空行？

```markdown
段落 1


段落 2
```

### 3. 如何显示特殊字符？

```markdown
使用反斜杠转义：
\* 不是斜体
\# 不是标题
```

### 4. 如何创建目录？

Hugo 会自动生成目录，配置：

```yaml
params:
  ShowToc: true
```

### 5. 如何添加代码复制按钮？

Hugo 主题通常会自动添加，配置：

```yaml
params:
  ShowCodeCopyButtons: true
```

## 实用工具

### 1. Markdown 编辑器

- **VS Code**：推荐，支持预览和语法高亮
- **Typora**：所见即所得
- **Mark Text**：开源免费

### 2. 在线编辑器

- [StackEdit](https://stackedit.io/)
- [Dillinger](https://dillinger.io/)

### 3. Markdown 转换工具

- [Pandoc](https://pandoc.org/)：格式转换
- [Markdown Here](https://markdown-here.com/)：邮件转换

## 示例文章模板

```markdown
---
title: "文章标题"
date: 2026-03-17T02:00:00+08:00
draft: false
tags: ["标签1", "标签2"]
categories: ["分类"]
description: "简短的文章描述"
---

## 引言

简短介绍文章主题和目的。

## 背景知识

相关的背景信息。

## 主要内容

### 要点 1

详细说明...

### 要点 2

详细说明...

## 代码示例

```bash
# 示例代码
command --option
```

## 实际应用

展示如何应用...

## 常见问题

Q: 问题？
A: 答案

## 总结

总结文章要点。

## 参考资料

- [链接 1](https://example.com)
- [链接 2](https://example.com)
```

## 总结

通过本文，你学会了：

- ✅ Front Matter 的使用
- ✅ 基础 Markdown 语法
- ✅ Hugo 扩展语法
- ✅ 短代码的使用
- ✅ 高级技巧
- ✅ 最佳实践

现在你可以开始创作高质量的文章了！

**记住：好的写作不仅需要掌握语法，更需要清晰的思路和结构。**

祝你写作愉快！