---
title: 架构详解
updatedDate: 2025-12-27
order: 1
---

# 架构详解

深入了解 ReWeave 的内部工作原理。

## 核心流程

ReWeave 的构建过程主要包含以下几个阶段：

1.  **扫描 (Scan)**: `src/core/build.tsx` 扫描 `src/content` 和 `src/docs` 目录，获取所有 Markdown 文件列表。
2.  **解析 (Parse & Compile)**:
    -   利用 **Worker Pool** (位于 `src/core/markdown.ts`) 并行处理文件。
    -   每个 Worker 运行 `unified` 管道 (Remark -> Rehype -> HTMLString)。
    -   解析 Frontmatter，提取元数据。
    -   处理数学公式 (KaTeX) 和代码高亮。
3.  **渲染 (Render)**:
    -   使用 `preact-render-to-string` 将 React 组件渲染为静态 HTML 字符串。
    -   将解析好的 Markdown 内容注入到选定主题的 `Layout` 组件中。
4.  **输出 (Output)**:
    -   将生成的 HTML 写入 `dist` 目录。
    -   复制 `public` 目录下的静态资源到 `dist`。
    -   使用 `Tailwind CSS` CLI 生成最终的 CSS 文件。

## 多线程 Worker 机制

为了实现极致的构建速度，ReWeave 采用了 Supervisor 模式的 Worker Pool。

-   **主线程**: 负责任务调度、文件 I/O 和最终的 HTML 组装。
-   **Worker 线程**: 纯粹的计算单元，负责 Markdown 到 HTML 的 CPU 密集型转换。
-   **容错**: 如果某个 Worker 因处理极其复杂的内容而崩溃，Supervisor 会自动重启 Worker 并重试任务，确保构建过程的稳定性。

## 缓存系统

ReWeave 实现了基于文件修改时间 (mtime) 的缓存机制。在开发模式 (`npm run dev`) 下，只有被修改过的文件才会被重新编译，这使得热更新 (HMR) 响应非常迅速。
