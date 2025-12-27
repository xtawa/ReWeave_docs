---
title: 主题开发
updatedDate: 2025-12-27
order: 2
---

# 主题开发指南

ReWeave 赋予了开发者完全的控制权。您可以轻松修改现有主题，或者从头创建一个全新的主题。

## 技术栈

- **Preact**: 轻量级的 React 替代方案，API 几乎完全兼容。
- **Tailwind CSS**: 实用优先的 CSS 框架，用于快速构建样式。
- **TypeScript**: 强类型支持。

## 主题结构

一个标准的主题位于 `src/themes/<theme-name>` 目录下：

```text
src/themes/my-theme/
├── config.ts        # 主题默认配置
├── components/      # UI 组件
│   ├── Header.tsx   # 顶部导航
│   ├── Footer.tsx   # 底部版权
│   └── Hero.tsx     # 首页 Hero 组件
├── layouts/         # 布局组件
│   ├── Layout.tsx   # 核心布局 (必须)
│   └── Home.tsx     # 首页专用布局 (可选)
└── templates/       # 页面模板 (可选)
    ├── Post.tsx     # 文章详情页
    └── Archive.tsx  # 归档页
```

## 核心接口：Layout

`Layout.tsx` 是主题的入口。构建器会将页面内容作为 `children` 传递给它。

```tsx
import { h, ComponentChildren } from 'preact';

interface LayoutProps {
  children: ComponentChildren;
  title?: string;
  siteTitle?: string;
  // 构建器会自动注入这些 Props
}

export function Layout({ children, title, siteTitle }: LayoutProps) {
  // 设置页面标题
  if (typeof document !== 'undefined') {
    document.title = title ? `${title} - ${siteTitle}` : siteTitle;
  }

  return (
    <div class="min-h-screen bg-gray-50 text-gray-900">
      <header>...</header>
      <main class="container mx-auto px-4">
        {children}
      </main>
      <footer>...</footer>
    </div>
  );
}
```

## 数据注入

在构建过程中，ReWeave 会将解析后的数据传递给组件。

- **Layout**: 接收 `title`, `description`, `frontmatter`, `toc` 等。
- **Post 模板**: 接收完整的 `post` 对象（包含 `content`, `date`, `tags`, `category` 等）以及 `prevPost` / `nextPost`。

## 样式开发

我们强烈建议使用 Tailwind CSS 类名编写样式，这能确保生成的 CSS 文件体积最小，并且与框架的其他部分风格统一。

如果需要自定义 CSS，可以在 `src/style.css` 中添加，或者在组件中使用 `<style>` 标签（注意：Preact 中通常直接使用全局 CSS 或 CSS Modules，但在 ReWeave 中直接写 Tailwind 类是最简单的）。