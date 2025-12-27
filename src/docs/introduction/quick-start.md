---
title: 快速开始
updatedDate: 2025-12-27
order: 2
---

# 快速开始

本指南将带领您从零开始，快速搭建并运行一个 ReWeave 项目。

## 1. 环境准备

在开始之前，请确保您的开发环境满足以下要求：

- **Node.js**: v18.0.0 或更高版本 (推荐 v20+ 以获得最佳性能)
- **包管理器**: npm, yarn, 或 pnpm
- **Git**: 用于版本控制

## 2. 安装与初始化

目前 ReWeave 推荐通过克隆模板仓库的方式进行初始化。

```bash
# 克隆项目仓库
git clone <repository-url> my-reweave-site

# 进入项目目录
cd my-reweave-site

# 安装依赖
npm install
```

## 3. 启动开发服务器

在开发模式下，ReWeave 提供了一个带有热重载功能的本地服务器。

```bash
npm run dev
```

启动成功后，终端会显示访问地址，通常是 `http://localhost:3000`。您在编辑器中修改 Markdown 文件或配置文件后，浏览器会自动刷新显示最新内容。

## 4. 构建生产版本

当您准备好发布站点时，运行构建命令生成静态文件。

```bash
npm run build
```

构建完成后，所有的静态文件（HTML, CSS, JS, 图片等）都会被输出到 `dist` 目录。您可以将该目录下的内容部署到任何静态网站托管服务（如 Vercel, GitHub Pages, Netlify）。

## 5. 本地预览

在部署之前，建议先在本地预览构建产物，以确保一切符合预期。

```bash
npm run preview
```

此命令会启动一个静态文件服务器，托管 `dist` 目录的内容。

## 下一步

- **了解结构**: 阅读 [项目结构](/basics/project-structure) 了解各个目录的作用。
- **开始写作**: 学习如何 [编写内容](/basics/writing-content) 及使用 Frontmatter。
- **定制站点**: 探索 [配置选项](/basics/configuration) 修改站点标题、主题等。
