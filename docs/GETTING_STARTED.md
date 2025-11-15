# Getting Started with Hugo Paper

This guide will help you set up and start using Hugo Paper theme for your blog.

## Prerequisites

Before you begin, make sure you have:

- **Hugo Extended** v0.120.0 or higher
  - Download: https://gohugo.io/installation/
  - Must be the Extended version (supports SCSS/SASS)
- **Git** 2.0 or higher
- **Go** 1.20 or higher (for Hugo Modules)
- **Node.js** v18.0 or higher (for Pagefind search)
- **pnpm** v8.0 or higher (recommended package manager)

Verify your installation:

```bash
hugo version  # Should show "extended"
git --version
go version
node --version
pnpm --version
```

## Installation

### Method 1: Use as Template (Recommended)

1. **Click "Use this template" button** on GitHub
   - Visit: https://github.com/ouraihub-hugo-themes/hugo-theme-paper-starter
   - Click the green "Use this template" button
   - Choose "Create a new repository"
   - Name your repository (e.g., `my-blog`)
   - Click "Create repository"

2. **Clone your new repository**

```bash
git clone https://github.com/yourusername/my-blog.git
cd my-blog
```

3. **Initialize Hugo Modules**

```bash
hugo mod get -u
```

4. **Install Node.js dependencies** (for Pagefind search)

```bash
pnpm install
```

5. **Start the development server**

```bash
pnpm dev
# or
hugo server
```

Visit http://localhost:1313 to see your blog!

**Note**: For search functionality to work, you need to build the site first with `pnpm build`.

### Method 2: Manual Clone

```bash
# Clone the starter repository
git clone https://github.com/ouraihub-hugo-themes/hugo-theme-paper-starter.git my-blog
cd my-blog

# Initialize Hugo Modules
hugo mod get -u

# Start development server
hugo server
```

## Project Structure

```
my-blog/
├── config/              # Configuration files
│   └── _default/
│       ├── hugo.toml    # Core Hugo settings
│       ├── languages.toml  # Language configuration
│       ├── menus.en.toml   # English menu
│       ├── menus.zh.toml   # Chinese menu
│       ├── params.toml     # Theme parameters
│       ├── markup.toml     # Markdown settings
│       └── module.toml     # Hugo Modules config
├── content/             # Your content
│   ├── en/             # English content
│   │   ├── post/       # Blog posts
│   │   │   └── _index.md  # Required for post list
│   │   ├── archives/   # Archives page
│   │   ├── search/     # Search page
│   │   └── about.md    # About page
│   └── zh/             # Chinese content
│       └── ...         # Same structure as en/
├── static/              # Static assets
├── layouts/             # Custom layouts (optional)
├── assets/              # Custom assets (optional)
├── go.mod               # Hugo Modules dependencies
└── go.sum               # Dependency lock file
```

## Understanding Hugo Modules

This starter uses **Hugo Modules** to manage the theme:

- **No Git submodules** - Easier to manage
- **Automatic updates** - Run `hugo mod get -u` to update
- **Pre-compiled theme** - Uses `hugo-theme-paper-dist` (no build tools needed)

The theme is configured in `config/_default/module.toml`:

```toml
[[imports]]
path = "github.com/ouraihub-hugo-themes/hugo-theme-paper-dist"
```

## Creating Your First Post

### 1. Create a new post

```bash
# English post
hugo new content/en/post/my-first-post.md

# Chinese post
hugo new content/zh/post/my-first-post.md
```

### 2. Edit the post

Open the generated file and edit the front matter:

```yaml
---
title: "My First Post"
description: "A brief description of your post"
date: 2024-01-15T10:00:00+08:00
draft: false              # Set to false to publish
featured: true            # Show in featured section
author: "Your Name"
categories:
  - Technology
tags:
  - Hugo
  - Blog
---

Your content starts here...

## This is a heading

Your post content in Markdown format.
```

### 3. View your post

Start the development server:

```bash
hugo server
```

Visit http://localhost:1313 to see your post.

## Creating Pages

### About Page

Edit `content/en/about.md`:

```yaml
---
title: "About"
date: 2024-01-15
layout: "page"
---

Information about you or your blog...
```

### Custom Pages

Create any page in the `content/` directory:

```bash
hugo new content/en/page/privacy.md
```

## Important Files

### _index.md Files

Each section (like `post/`) **must** have an `_index.md` file:

```yaml
# content/en/post/_index.md
---
title: "Posts"
description: "All the articles I've posted."
---
```

Without this file, the post list page will show a 404 error.

## Development Workflow

### Start Development Server

```bash
# Using pnpm (recommended)
pnpm dev

# Or directly with Hugo
hugo server

# With drafts
hugo server -D

# Custom port
hugo server --port 1313

# Accessible from LAN
hugo server --bind 0.0.0.0
```

### Build for Production

```bash
# Build with Pagefind search index (recommended)
pnpm build

# This runs:
# 1. hugo --minify --gc
# 2. pagefind --site public

# Or build without search
hugo --minify

# Output is in public/ directory
```

### Search Functionality (Pagefind)

This starter uses [Pagefind](https://pagefind.app/) for static search functionality.

**How it works:**
1. Pagefind scans your built site (`public/` directory)
2. Creates a search index
3. Provides instant client-side search

**Building with search:**
```bash
# Install dependencies first
pnpm install

# Build site with search index
pnpm build
```

**Note**: Search won't work in development mode (`hugo server`). You need to build the site first.

### Update Theme

**自动更新**：
- 每次部署时自动使用最新版本主题
- 无需手动操作

**手动更新本地**（可选）：
```bash
# 更新到最新版本
hugo mod get -u

# 测试
hugo server

# 提交更新
git add go.mod go.sum
git commit -m "chore: 更新主题"
git push
```

详见：[主题更新指南](THEME_UPDATE.md)

## Multilingual Setup

This starter supports English and Chinese out of the box.

### Language Configuration

Languages are configured in `config/_default/languages.toml`:

```toml
[en]
languageName = "English"
languageCode = "en"
weight = 1
title = "My Blog"
contentDir = "content/en"  # Important!

[zh]
languageName = "中文"
languageCode = "zh"
weight = 2
title = "我的博客"
contentDir = "content/zh"  # Important!
```

### Content Organization

- English content: `content/en/`
- Chinese content: `content/zh/`
- Default language (English) URLs: `/post/my-post/`
- Other language URLs: `/zh/post/my-post/`

### Linking Translations

To link English and Chinese versions of the same post, use `translationKey`:

```yaml
# content/en/post/my-post.md
---
title: "My Post"
translationKey: my-post
---

# content/zh/post/my-post.md
---
title: "我的文章"
translationKey: my-post
---
```

## Next Steps

- [Configuration Guide](CONFIGURATION.md) - Detailed configuration options
- [Deployment Guide](DEPLOYMENT.md) - Deploy to various platforms
- [Theme Documentation](https://github.com/ouraihub-hugo-themes/hugo-theme-paper) - Full theme docs

## Troubleshooting

### Theme not found

```bash
# Initialize Hugo Modules
hugo mod get -u
hugo mod tidy
```

### Post list page shows 404

Make sure `content/en/post/_index.md` exists:

```yaml
---
title: "Posts"
description: "All the articles I've posted."
---
```

### Styles not loading

```bash
# Clean cache and rebuild
hugo mod clean
rm -rf resources/_gen
hugo --gc
```

### Module errors

```bash
# Clean and reinitialize
hugo mod clean
hugo mod get -u
hugo mod tidy
```

## Getting Help

- **Documentation**: https://github.com/ouraihub-hugo-themes/hugo-theme-paper
- **Issues**: https://github.com/ouraihub-hugo-themes/hugo-theme-paper/issues
- **Discussions**: https://github.com/ouraihub-hugo-themes/hugo-theme-paper/discussions

## License

This project is licensed under the MIT License. See [LICENSE](../LICENSE) for details.
