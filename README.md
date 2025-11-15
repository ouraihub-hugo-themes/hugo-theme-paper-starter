# Hugo Paper Starter

English | [简体中文](README.zh.md)

A quick start template for [Hugo Paper](https://github.com/ouraihub-hugo-themes/hugo-theme-paper) theme - a minimal, responsive blog theme inspired by AstroPaper.

**Features:**
- ✅ Pre-configured with Hugo Modules
- ✅ Uses pre-compiled theme (no build tools needed)
- ✅ GitHub Actions deployment included
- ✅ Multilingual support (English/Chinese)
- ✅ Ready to use out of the box

## 📖 Documentation

- **[Getting Started](docs/GETTING_STARTED.md)** - Installation and first steps
- **[Configuration](docs/CONFIGURATION.md)** - Detailed configuration guide
- **[Deployment](docs/DEPLOYMENT.md)** - Deploy to GitHub Pages
- **[Quick Setup](docs/SETUP_DEPLOYMENT.md)** - One-minute deployment guide
- **[Changelog](CHANGELOG.md)** - Version history

**Theme Repositories:**
- [Development Repository](https://github.com/ouraihub-hugo-themes/hugo-theme-paper) - Source code
- [Distribution Repository](https://github.com/ouraihub-hugo-themes/hugo-theme-paper-dist) - Pre-compiled (used by this starter)

## 🚀 Quick Start

### Prerequisites

- Hugo Extended v0.120.0+
- Git 2.0+
- Go 1.20+
- Node.js v18.0+ (for Pagefind search)
- pnpm v8.0+

### Installation

1. **Use this template** (click the green button above)
2. **Clone your repository**
   ```bash
   git clone https://github.com/yourusername/your-repo.git
   cd your-repo
   ```
3. **Initialize Hugo Modules**
   ```bash
   hugo mod get -u
   ```
4. **Install dependencies** (for search)
   ```bash
   pnpm install
   ```
5. **Start development server**
   ```bash
   pnpm dev
   ```
6. **Visit** http://localhost:1313

See [Getting Started Guide](docs/GETTING_STARTED.md) for detailed instructions.

## ✨ Features

- 🎨 Minimal and responsive design
- 🌓 Dark/Light mode support
- 🔍 Built-in search functionality
- 🌐 Multilingual (English/Chinese)
- ⚡️ Fast performance
- ♿️ WCAG 2.1 AA accessibility
- 🎯 SEO optimized
- 💬 Giscus comments integration

## 📝 Creating Content

### Create a new post

```bash
# English post
hugo new content/en/post/my-first-post.md

# Chinese post
hugo new content/zh/post/my-first-post.md
```

### Edit the post

```yaml
---
title: "My First Post"
date: 2024-01-15T10:00:00+08:00
draft: false
description: "Post description"
categories: ["Technology"]
tags: ["Hugo", "Blog"]
---

Your content here...
```

See [Getting Started Guide](docs/GETTING_STARTED.md) for more details.

## 🚢 Deployment

This starter includes GitHub Actions for automatic deployment to GitHub Pages.

**Other platforms:**
- [Vercel](docs/DEPLOYMENT.md#vercel)
- [Netlify](docs/DEPLOYMENT.md#netlify)
- [Cloudflare Pages](docs/DEPLOYMENT.md#cloudflare-pages)

See [Deployment Guide](docs/DEPLOYMENT.md) for detailed instructions.

## 🔄 Updating Theme

```bash
hugo mod get -u
hugo mod tidy
```

## 🤝 Contributing

Issues and Pull Requests are welcome!

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

## 🔗 Links

- [Hugo Paper Theme](https://github.com/ouraihub-hugo-themes/hugo-theme-paper)
- [Hugo Documentation](https://gohugo.io/documentation/)

---

**Powered by [Hugo Paper](https://github.com/ouraihub-hugo-themes/hugo-theme-paper)** 🚀
