---
title: 快速开始
updatedDate: 2025-12-27
order: 2
---

# 快速开始

本指南将帮助你快速搭建并运行一个 ReWeave 项目。

## 环境要求

- **Node.js**: v18.0.0 或更高版本
- **包管理器**: npm, yarn, 或 pnpm

## 安装与运行

1. **克隆项目**

   ```bash
   git clone <repository-url> my-reweave-site
   cd my-reweave-site
   ```

2. **安装依赖**

   ```bash
   npm install
   ```

3. **启动开发服务器**

   ```bash
   npm run dev
   ```

   服务器启动后，通常可以在 `http://localhost:3000` 访问你的站点。开发服务器支持热重载，修改内容后会自动刷新。

## 构建生产版本

当准备好部署时，运行构建命令：

```bash
npm run build
```

构建产物将输出到 `dist` 目录。

## 预览生产版本

要在本地预览构建后的站点：

```bash
npm run preview
```

## 下一步

- 了解 [项目结构](/docs/basics/project-structure)
- 学习如何 [编写内容](/docs/basics/writing-content)
- 探索 [配置选项](/docs/basics/configuration)