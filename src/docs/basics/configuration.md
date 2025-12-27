---
title: 配置指南
updatedDate: 2025-12-27
order: 3
---

# 配置指南

ReWeave 提供了灵活的配置系统，允许您通过简单的 TypeScript 文件控制站点的各个方面。

## 全局配置

全局配置文件位于 `src/config/reweave.config.ts`。

```typescript
const config = {
  // 站点标题，显示在浏览器标签页和导航栏
  title: "ReWeave Docs",
  
  // 站点描述，用于 SEO meta 标签
  description: "Documentation for ReWeave Framework",
  
  // 站点基础 URL，用于生成 RSS 和 Sitemap
  siteUrl: "https://reweave.vercel.app",
  
  // 默认语言
  language: "zh-CN",
  
  // 当前激活的主题
  // 修改此项可立即切换全站风格
  themeName: 'gitbook', // 可选: 'weave' | 'gitbook' | 'landing' | 'butterfly'
  
  // 目录生成 (Table of Contents) 配置
  toc: {
    enabled: true,      // 是否开启
    maxDepth: 3,        // 最大深度 (h1-h3)
    position: 'right',  // 位置: 'left' | 'right' | 'top'
    collapsible: true   // 是否可折叠
  },
  
  // 首页模式
  // 'hero': 使用 Hero 组件 (适用于 Landing 主题)
  // 'posts': 直接显示文章列表 (适用于 Weave/Butterfly 主题)
  homePage: 'posts',
};
```

## 主题专属配置

每个主题都有其独立的配置文件，位于 `src/config` 目录下。

### Weave 主题配置 (`weave.config.ts`)

```typescript
export default {
  // 导航栏链接
  navLinks: [
    { name: "首页", href: "/" },
    { name: "归档", href: "/archive" },
    { name: "关于", href: "/about" },
  ],
  
  // 社交链接图标
  social: {
    github: "https://github.com/xtawa/ReWeave",
    twitter: "https://twitter.com/xtawa",
  },
  
  // 分页设置
  postsPerPage: 10,
};
```

### GitBook 主题配置 (`gitbook.config.ts`)

```typescript
export default {
  // 侧边栏顶部标题
  sidebarTitle: "ReWeave 文档",
  
  // 是否启用搜索功能
  enableSearch: false,
  
  // 仓库链接 (用于显示 "在 GitHub 上编辑此页")
  repoUrl: "https://github.com/xtawa/ReWeave",
};
```

## 注意事项

- **类型安全**: 配置文件是 TypeScript 格式，这意味着编辑器会提供智能提示。如果输入了错误的配置项，构建时会报错，从而避免运行时错误。
- **热更新**: 修改配置文件通常会触发热更新，但修改 `themeName` 等涉及重大的架构变更可能需要重启开发服务器 (`npm run dev`)。