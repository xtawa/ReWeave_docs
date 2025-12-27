---
title: 项目结构
updatedDate: 2025-12-27
order: 1
---

# 项目结构

深入了解 ReWeave 的项目结构有助于你更好地管理内容、修改配置和进行二次开发。

```
reweave-project/
├── .github/             # GitHub Actions 工作流配置 (如自动部署)
├── dist/                # 构建输出目录 (生成后出现)
├── public/              # 静态资源目录 (图片, favicon, robots.txt 等)
├── scripts/             # 辅助脚本 (测试数据生成, 性能基准测试等)
├── src/
│   ├── config/          # 配置文件目录
│   │   ├── reweave.config.ts   # 主配置文件 (站点元数据, 主题选择)
│   │   ├── weave.config.ts     # Weave 主题配置
│   │   ├── gitbook.config.ts   # GitBook 主题配置
│   │   └── ...
│   ├── content/         # 博客文章内容 (扁平化 Markdown 文件)
│   ├── docs/            # 文档内容 (支持多级目录的 Markdown 文件)
│   ├── core/            # 框架核心逻辑 (构建器, Worker, Markdown 引擎)
│   ├── themes/          # 主题目录 (组件, 布局, 模板)
│   │   ├── weave/       
│   │   ├── gitbook/     
│   │   └── ...
│   └── style.css        # 全局样式 (Tailwind CSS 入口)
├── package.json         # 项目依赖、脚本命令
├── tailwind.config.js   # Tailwind CSS 配置
└── tsconfig.json        # TypeScript 配置
```

## 关键目录详解

### `src/content`
这是存放**博客文章**的地方。通常用于存放时间流的日志、技术文章等。
- 所有的 `.md` 文件都会被处理为独立的页面。
- URL 路径通常基于文件名（slug）或 Frontmatter 中的 `abbrlink` 生成。
- 不支持复杂的嵌套目录结构（目前设计为扁平化管理，便于分类和标签检索）。

### `src/docs`
这是存放**结构化文档**的地方。适合构建书籍、手册、教程等。
- 支持多级子目录。
- `gitbook` 主题会根据此目录的物理结构自动生成左侧导航栏。
- 每个目录下可以包含一个 `index.md` 作为该章节的入口页。

### `src/config`
配置中心。为了保持根目录整洁，我们将所有配置文件移入此目录。
- `reweave.config.ts`: 核心配置，控制全站行为。
- `*.config.ts`: 特定主题的配置，只有在使用对应主题时才会生效。

### `public`
静态资源目录。
- 放在这里的文件会被直接复制到构建输出目录 `dist` 的根目录下。
- 例如：`public/logo.png` -> `dist/logo.png`。
- 在 Markdown 中引用时，请使用绝对路径 `/logo.png`。

### `src/themes`
主题仓库。
- 每个子目录代表一个主题。
- 如果您想修改某个主题的布局或样式，直接修改对应目录下的 `Layout.tsx` 或组件即可。
- 支持热更新，修改后立即生效。