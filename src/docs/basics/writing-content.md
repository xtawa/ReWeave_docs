---
title: 编写内容
updatedDate: 2025-12-27
order: 2
---

# 编写内容

ReWeave 使用 Markdown 作为主要的内容编写格式。

## 文件位置

- **博客文章**: 放在 `src/content` 目录下。通常是扁平结构。
- **文档页面**: 放在 `src/docs` 目录下。支持嵌套目录，适合层级化内容。

## Frontmatter

每个 Markdown 文件的开头必须包含 Frontmatter，用于定义页面的元数据。格式为 YAML。

### 博客文章示例 (`src/content`)

```yaml
---
title: 我的第一篇文章
date: 2025-12-27
category: 技术
tags: [ReWeave, 教程]
excerpt: 这是一篇关于如何使用 ReWeave 的文章摘要...
cover: /images/cover.jpg  # 可选，封面图路径
---
```

### 文档页面示例 (`src/docs`)

```yaml
---
title: 快速开始
updatedDate: 2025-12-27
order: 2  # 决定在侧边栏中的排序，数字越小越靠前
---
```

## Markdown 语法支持

ReWeave 基于 `unified` 生态，支持丰富的 Markdown 语法。

### 基础语法
支持标题、列表、粗体、斜体、链接、图片等标准语法。

### 代码块
支持语法高亮：

```typescript
function hello(name: string) {
  console.log(`Hello, ${name}!`);
}
```

### 数学公式 (LaTeX)
使用 `$` 或 `$$` 包裹 LaTeX 代码：

行内公式：$E = mc^2$

块级公式：
$$
\int_{-\infty}^\infty e^{-x^2} dx = \sqrt{\pi}
$$

### 表格
| 功能 | 状态 | 说明 |
| :--- | :---: | :--- |
| 构建 | ✅ | 极速 |
| 主题 | ✅ | 多样 |
| 搜索 | 🚧 | 规划中 |

### 图片
图片可以放在 `public` 目录下，然后使用绝对路径引用。
例如，`public/logo.png` 可以通过 `![Logo](/logo.png)` 引用。
