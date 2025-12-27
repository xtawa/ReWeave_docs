---
title: 项目结构
updatedDate: 2025-12-27
order: 1
---

# 项目结构

了解 ReWeave 的项目结构有助于你更好地管理内容和进行开发。

```
├── public/              # 静态资源目录 (图片, favicon 等)
├── scripts/             # 辅助脚本 (测试数据生成等)
├── src/
│   ├── config/          # 配置文件目录
│   │   ├── reweave.config.ts   # 主配置文件
│   │   └── *.config.ts         # 各主题配置文件
│   ├── content/         # 博客文章内容 (Markdown)
│   ├── docs/            # 文档内容 (Markdown, 树状结构)
│   ├── core/            # 框架核心逻辑
│   │   ├── build.tsx    # 构建脚本
│   │   ├── dev.ts       # 开发服务器
│   │   ├── markdown.ts  # Markdown 处理逻辑
│   │   └── workers/     # 多线程 Worker
│   ├── themes/          # 主题目录
│   │   ├── weave/       # Weave 主题
│   │   ├── gitbook/     # GitBook 主题
│   │   └── ...
│   └── style.css        # 全局样式 (Tailwind CSS)
├── package.json         # 项目依赖和脚本
└── tsconfig.json        # TypeScript 配置
```

## 关键目录说明

### `src/content`
这是存放博客文章的地方。所有 `.md` 文件都会被处理为独立的页面。文件名将作为 URL 的 slug。

### `src/docs`
这是存放文档的地方。支持多级目录结构，适合构建像本书一样的文档网站。`gitbook` 主题主要读取此目录。

### `src/config`
所有的配置文件都集中在这里。你可以修改 `reweave.config.ts` 来切换主题或修改全局设置。

### `src/themes`
如果你想自定义外观，可以在这里找到对应的主题代码。每个主题通常包含 `layouts` (布局), `components` (组件) 和 `config.ts` (主题配置)。

### `src/core`
这是 ReWeave 的引擎室。除非你打算贡献代码或进行深度定制，否则通常不需要修改这里的内容。
