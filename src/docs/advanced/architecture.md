---
title: 架构详解
updatedDate: 2025-12-27
order: 1
---

# 架构详解

ReWeave 的核心目标是在处理大规模内容时保持极速的构建性能。为了实现这一目标，我们设计了一套独特的多线程构建架构。

## 构建流水线 (Build Pipeline)

构建过程可以被视为一条流水线，主要包含以下四个阶段：

1.  **扫描 (Scan)**
    主线程遍历 `src/content` 和 `src/docs` 目录，收集所有 Markdown 文件路径。此阶段不读取文件内容，仅建立文件列表。

2.  **调度与解析 (Schedule & Parse)**
    这是最耗时的阶段。主线程将文件列表作为任务分发给 **Worker Pool**。
    -   **Supervisor**: 监控 Worker 状态，负责任务分配和负载均衡。
    -   **Workers**: 独立运行的 Node.js 线程。每个 Worker 加载 `unified` 生态链（Remark/Rehype），并行执行 Markdown 到 HTML 的转换、代码高亮和数学公式渲染。

3.  **渲染 (Render)**
    当 Worker 返回 HTML 字符串和元数据后，主线程接管控制权。
    -   使用 `preact-render-to-string` 将页面数据注入到主题的 `Layout` 组件中。
    -   生成最终的静态 HTML 字符串。

4.  **输出与优化 (Output & Optimize)**
    -   并发写入文件到 `dist` 目录。
    -   复制 `public` 资源。
    -   使用 Tailwind CLI 生成最小化的 CSS 文件。

## Worker Pool (Supervisor 模式)

为了解决单线程 Node.js 在 CPU 密集型任务（如大量的正则匹配和 AST 转换）下的性能瓶颈，ReWeave 实现了一个自定义的 Worker Pool。

-   **隔离性**: 每个 Markdown 文件的处理是相互隔离的，一个文件的解析错误不会导致整个构建进程崩溃。
-   **容错性**: 如果某个 Worker 因处理极端复杂的 LaTeX 公式而挂起或崩溃，Supervisor 会自动终止该 Worker，创建一个新 Worker，并将失败的任务标记或重试（取决于配置）。
-   **资源管理**: 根据 CPU 核心数自动调整 Worker 数量，最大化利用硬件资源。

## 缓存系统

ReWeave 采用了基于文件指纹和修改时间 (mtime) 的多级缓存策略。

-   **开发环境**: 监听文件变动 (`chokidar`)。只有发生变化的文件才会重新触发 Worker 任务，未修改的文件直接使用内存缓存。
-   **生产环境**: （计划中）支持持久化文件缓存，使得二次构建仅需处理新增文章。