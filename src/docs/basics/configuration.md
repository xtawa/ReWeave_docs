---
title: 配置指南
updatedDate: 2025-12-27
order: 3
---

# 配置指南

ReWeave 的配置系统位于 `src/config` 目录下。

## 全局配置 (`src/config/reweave.config.ts`)

这是项目的主配置文件，用于定义站点标题、描述、当前使用的主题等。

```typescript
import type { ReWeaveConfig } from '../core/types'; // 假设的类型导入

const config = {
  // 站点标题，显示在浏览器标签页和导航栏
  title: "ReWeave Docs",
  
  // 站点描述，用于 SEO
  description: "Documentation for ReWeave Framework",
  
  // 当前激活的主题
  // 可选值: 'weave' | 'gitbook' | 'landing' | 'butterfly'
  themeName: 'gitbook',
  
  // 站点的基础 URL (如果部署在子路径下)
  // baseUrl: '/docs/',
};

export default config;
```

## 主题配置

每个主题都有自己的独立配置文件，同样位于 `src/config` 目录下。

### Weave 主题 (`src/config/weave.config.ts`)

适用于博客的配置。

```typescript
export default {
  // 导航菜单链接
  navLinks: [
    { name: "Home", href: "/" },
    { name: "About", href: "/about" },
    { name: "Projects", href: "/projects" },
  ],
  // 社交媒体链接
  social: {
    github: "https://github.com/yourname",
    twitter: "https://twitter.com/yourname",
  },
  // 每页显示的文章数量
  postsPerPage: 10,
};
```

### GitBook 主题 (`src/config/gitbook.config.ts`)

适用于文档的配置。

```typescript
export default {
  // 侧边栏标题
  sidebarTitle: "文档目录",
  
  // 顶部导航链接
  navLinks: [
    { name: "首页", href: "/" },
    { name: "GitHub", href: "https://github.com/..." },
  ],
  
  // 是否启用搜索 (如果有实现)
  enableSearch: false,
};
```

## 环境变量

对于敏感信息或环境特定的配置，可以使用环境变量。虽然 ReWeave 是纯静态生成，但在构建时可以访问 Node.js 环境变量。

你可以在构建命令前设置环境变量，或者使用 `.env` 文件（需配合 `dotenv` 等库，ReWeave 默认构建脚本目前主要读取配置文件）。
