---
title: 主题开发
updatedDate: 2025-12-27
order: 2
---

# 主题开发指南

ReWeave 的主题系统基于 TypeScript 和 React (Preact) 组件，非常易于扩展和定制。

## 主题目录结构

一个标准的主题位于 `src/themes/<theme-name>` 目录下，通常包含以下结构：

```
src/themes/my-theme/
├── components/      # 主题特有的 UI 组件 (Header, Footer, Sidebar 等)
│   ├── Header.tsx
│   └── Footer.tsx
├── layouts/         # 页面布局组件
│   ├── Layout.tsx   # 通用布局 (必须)
│   └── Home.tsx     # 首页布局 (可选，用于覆盖默认首页)
├── templates/       # 特殊页面的模板 (可选)
│   └── Post.tsx     # 单篇文章的显示模板
└── config.ts        # 主题默认配置 (建议)
```

## 核心组件说明

### `layouts/Layout.tsx`

这是主题的入口组件。所有的页面内容都会被包裹在这个组件中。

```tsx
import type { ComponentChildren } from 'preact';

interface LayoutProps {
  children: ComponentChildren;
  title?: string;
  // ...其他元数据
}

export default function Layout({ children, title }: LayoutProps) {
  return (
    <div className="min-h-screen bg-white dark:bg-gray-900">
      <Header />
      <main className="container mx-auto px-4 py-8">
        {children}
      </main>
      <Footer />
    </div>
  );
}
```

### `components/Header.tsx`

通常包含导航栏、Logo 和主题切换开关。

### 样式开发

我们推荐使用 Tailwind CSS 进行样式开发，这能保证主题的轻量级和易维护性。你可以直接在组件的 className 中编写样式。

## 注册新主题

虽然目前 ReWeave 通过动态导入加载主题，但为了获得最佳的 TypeScript 支持，建议遵循现有的命名规范。

1. 在 `src/themes` 下创建新文件夹。
2. 实现 `layouts/Layout.tsx`。
3. 在 `src/config/reweave.config.ts` 中将 `themeName` 设置为你的新主题目录名。

## 获取数据

在构建过程中，ReWeave 会将页面数据（Frontmatter, 内容 HTML, 导航信息等）作为 Props 传递给 `Layout` 组件。你可以在 Layout 中根据这些数据决定如何渲染页面。
