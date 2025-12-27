---
title: 部署指南
updatedDate: 2025-12-27
order: 2
---

# 部署指南

ReWeave 生成的是标准的静态 HTML/CSS/JS 文件，这意味着您可以将其部署在互联网上几乎任何位置。

## 标准构建流程

无论选择哪种托管方式，第一步都是生成构建产物。

```bash
# 安装依赖
npm install

# 执行构建
npm run build
```

构建完成后，项目根目录下会出现一个 `dist` 文件夹。这就是您需要发布的全部内容。

## 平台特定指南

### 1. Vercel (强烈推荐)

Vercel 拥有全球 CDN 和极佳的开发者体验，是部署 ReWeave 的首选。

1.  登录 Vercel Dashboard。
2.  点击 **"Add New..."** -> **"Project"**。
3.  导入包含 ReWeave 项目的 Git 仓库。
4.  Vercel 通常能自动识别项目配置。如果没有，请手动设置：
    -   **Framework Preset**: Other
    -   **Build Command**: `npm run build`
    -   **Output Directory**: `dist`
5.  点击 **Deploy**。

### 2. GitHub Pages

使用 GitHub Actions 可以实现自动化部署。

在项目根目录创建 `.github/workflows/deploy.yml`：

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

提交代码后，GitHub Actions 会自动运行并将 `dist` 目录推送到 `gh-pages` 分支。

### 3. Nginx

如果您拥有自己的 Linux 服务器，可以使用 Nginx 托管。

```nginx
server {
    listen 80;
    server_name example.com;
    
    # 指向 dist 目录的绝对路径
    root /var/www/my-reweave-site/dist;
    index index.html;

    location / {
        # 尝试查找对应的 HTML 文件
        try_files $uri $uri.html $uri/index.html /404.html;
    }

    # 缓存静态资源
    location ~* \.(css|js|png|jpg|jpeg|gif|ico|svg)$ {
        expires 30d;
        add_header Cache-Control "public, no-transform";
    }
}
```

## 常见问题

**Q: 部署后样式丢失？**
A: 请检查 `reweave.config.ts` 中的 `siteUrl` 或 `baseUrl` 配置是否正确，以及 Nginx 配置中是否正确设置了 `root` 路径。

**Q: 刷新页面出现 404？**
A: 对于静态站点，服务器需要配置为当 URL 对应文件不存在时，尝试查找 `.html` 后缀的文件或目录下的 `index.html`。