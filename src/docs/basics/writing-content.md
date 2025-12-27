---
title: 编写内容
updatedDate: 2025-12-27
order: 2
---

# 编写内容

ReWeave 旨在提供最佳的 Markdown 写作体验。本指南将介绍如何利用 ReWeave 的特性编写丰富多彩的内容。

## Frontmatter (元数据)

每个 Markdown 文件的顶部必须包含 Frontmatter，用于定义页面的元数据。格式为 YAML，由三根短横线包裹。

### 通用字段

```yaml
---
title: 文章标题              # 必填
date: 2025-12-27            # 发布日期
updatedDate: 2025-12-28     # 更新日期 (可选)
excerpt: 文章摘要...         # 摘要，用于列表页展示
cover: /images/cover.jpg    # 封面图路径 (可选)
draft: false                # 是否为草稿 (true 则不构建)
hide: false                 # 是否隐藏 (true 则不显示在列表)
order: 1                    # 排序权重 (数字越小越靠前，主要用于文档)
---
```

### 分类与标签 (仅博客)

```yaml
---
category: 技术教程           # 分类 (单选)
tags: [ReWeave, Markdown]   # 标签 (多选)
---
```

## Markdown 语法增强

除了标准的 Markdown 语法外，ReWeave 还内置了多种扩展支持。

### 1. 代码高亮

支持几乎所有主流编程语言的语法高亮。

```typescript
// TypeScript 示例
interface User {
  id: number;
  name: string;
}

const user: User = { id: 1, name: "ReWeave" };
```

### 2. 数学公式 (LaTeX)

使用 KaTeX 引擎渲染高质量的数学公式。

**行内公式**: 质能方程 $E = mc^2$ 改变了物理学。

**块级公式**:
$$
f(x) = \int_{-\infty}^\infty \hat f(\xi)\,e^{2\pi i \xi x} \,d\xi
$$

### 3. 表格

支持 GFM 风格的表格。

| 语法 | 效果 | 示例 |
| :--- | :---: | :--- |
| `**Bold**` | **粗体** | 强调 |
| `*Italic*` | *斜体* | 强调 |
| `` `Code` `` | `代码` | 行内 |

### 4. 引用块

> 这是一个引用块。
> 可以包含多行。

### 5. 图片

建议将图片放在 `public` 目录下，并使用绝对路径引用。

```markdown
![示例图片](/landing_hero_bg.png)
```

## 提示与技巧

- **文件名**: 建议使用英文连字符命名法（kebab-case），如 `my-first-post.md`，这将作为 URL 的一部分。
- **摘要**: 如果不手动指定 `excerpt`，系统会自动截取文章前 200 个字符作为摘要。
- **资源管理**: 对于大型站点，建议在 `public` 下建立子目录（如 `public/images/2025/`）来组织图片。