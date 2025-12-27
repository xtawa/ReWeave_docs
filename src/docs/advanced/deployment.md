---
title: 部署指南
updatedDate: 2025-12-27
order: 2
---

# 部署指南

ReWeave 生成的是纯静态文件，因此可以部署在任何支持静态网站托管的服务上。

## 构建

首先，确保你已经运行了构建命令：

```bash
npm run build
```

这将在项目根目录下生成 `dist` 文件夹。

## 部署选项

### 1. Vercel (推荐)

Vercel 是部署 Next.js 和其他静态站点的绝佳平台，对 ReWeave 支持良好。

1.  在 Vercel 控制台导入你的 GitHub 仓库。
2.  配置构建设置：
    -   **Build Command**: `npm run build`
    -   **Output Directory**: `dist`
    -   **Install Command**: `npm install`
3.  点击 Deploy。

### 2. GitHub Pages

你可以使用 GitHub Actions 自动部署。

创建一个 `.github/workflows/deploy.yml` 文件：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: 18
      - run: npm install
      - run: npm run build
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

### 3. Nginx / Apache

只需将 `dist` 目录下的所有文件上传到你的 Web 服务器根目录（例如 `/var/www/html`）即可。

确保服务器配置了正确的 MIME 类型，并且处理好 404 错误页（指向 `404.html`）。
