# Hugo Paper Starter

[English](README.md) | 简体中文

[Hugo Paper](https://github.com/ouraihub-hugo-themes/hugo-theme-paper) 主题的快速启动模板 - 一个受 AstroPaper 启发的最小化、响应式博客主题。

**特性：**
- ✅ 预配置 Hugo Modules
- ✅ 使用预编译主题（无需构建工具）
- ✅ 包含 GitHub Actions 部署
- ✅ 多语言支持（英文/中文）
- ✅ 开箱即用

## 📖 文档

- **[快速开始](docs/GETTING_STARTED.md)** - 安装和入门步骤
- **[配置指南](docs/CONFIGURATION.md)** - 详细配置说明
- **[部署指南](docs/DEPLOYMENT.md)** - 部署到各种平台
- **[更新日志](CHANGELOG.md)** - 版本历史

**主题仓库：**
- [开发仓库](https://github.com/ouraihub-hugo-themes/hugo-theme-paper) - 源代码
- [分发仓库](https://github.com/ouraihub-hugo-themes/hugo-theme-paper-dist) - 预编译版本（本 starter 使用）

## 🚀 快速开始

### 前置要求

- Hugo Extended v0.120.0+
- Git 2.0+
- Go 1.20+
- Node.js v18.0+（用于 Pagefind 搜索）
- pnpm v8.0+

### 安装

1. **使用此模板**（点击上方绿色按钮）
2. **克隆你的仓库**
   ```bash
   git clone https://github.com/你的用户名/你的仓库.git
   cd 你的仓库
   ```
3. **初始化 Hugo Modules**
   ```bash
   hugo mod get -u
   ```
4. **安装依赖**（用于搜索功能）
   ```bash
   pnpm install
   ```
5. **启动开发服务器**
   ```bash
   pnpm dev
   ```
6. **访问** http://localhost:1313

详细说明请查看[快速开始指南](docs/GETTING_STARTED.md)。

## ✨ 特性

- 🎨 最小化响应式设计
- 🌓 深色/浅色模式支持
- 🔍 内置搜索功能
- 🌐 多语言（英文/中文）
- ⚡️ 高性能
- ♿️ WCAG 2.1 AA 无障碍支持
- 🎯 SEO 优化
- 💬 Giscus 评论集成

## 📝 创建内容

### 创建新文章

```bash
# 英文文章
hugo new content/en/post/my-first-post.md

# 中文文章
hugo new content/zh/post/my-first-post.md
```

### 编辑文章

```yaml
---
title: "我的第一篇文章"
date: 2024-01-15T10:00:00+08:00
draft: false
description: "文章描述"
categories: ["技术"]
tags: ["Hugo", "博客"]
---

文章内容...
```

详细说明请查看[快速开始指南](docs/GETTING_STARTED.md)。

## 🚢 部署

本 starter 包含 GitHub Actions，可自动部署到 GitHub Pages。

**其他平台：**
- [Vercel](docs/DEPLOYMENT.md#vercel)
- [Netlify](docs/DEPLOYMENT.md#netlify)
- [Cloudflare Pages](docs/DEPLOYMENT.md#cloudflare-pages)

详细说明请查看[部署指南](docs/DEPLOYMENT.md)。

## 🔄 更新主题

```bash
hugo mod get -u
hugo mod tidy
```

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

MIT License - 详见 [LICENSE](LICENSE)。

## 🔗 链接

- [Hugo Paper 主题](https://github.com/ouraihub-hugo-themes/hugo-theme-paper)
- [Hugo 文档](https://gohugo.io/documentation/)

---

**由 [Hugo Paper](https://github.com/ouraihub-hugo-themes/hugo-theme-paper) 驱动** 🚀
