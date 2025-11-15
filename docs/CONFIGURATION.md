# Configuration Guide

This guide covers all configuration options for Hugo Paper theme.

## Configuration Files

Hugo Paper uses a modular configuration structure in `config/_default/`:

```
config/_default/
├── hugo.toml        # Core Hugo settings
├── languages.toml   # Language configuration
├── menus.en.toml    # English menu
├── menus.zh.toml    # Chinese menu
├── params.toml      # Theme parameters
├── markup.toml      # Markdown rendering
└── module.toml      # Hugo Modules
```

## Core Configuration (hugo.toml)

### Basic Settings

```toml
baseURL = "https://yourdomain.com/"  # Your site URL
title = "My Blog"                     # Site title
defaultContentLanguage = "en"         # Default language: en or zh

# Content Settings
enableInlineShortcodes = true
enableEmoji = true
hasCJKLanguage = true                 # Enable for Chinese/Japanese/Korean
summaryLength = 200                   # Summary length in words
```

### Pagination

```toml
[pagination]
pagerSize = 10  # Number of posts per page
```

### Taxonomies

```toml
[taxonomies]
category = "categories"
tag = "tags"
```

### Output Formats

```toml
[outputs]
home = ["HTML", "RSS", "JSON"]  # JSON for search
page = ["HTML"]
section = ["HTML", "RSS"]

[outputFormats.JSON]
mediaType = "application/json"
baseName = "index"
```

## Language Configuration (languages.toml)

### English Configuration

```toml
[en]
languageName = "English"
languageCode = "en"
weight = 1
title = "My Blog"
contentDir = "content/en"  # Required!

[en.params]
description = "My blog description"
```

### Chinese Configuration

```toml
[zh]
languageName = "中文"
languageCode = "zh"
weight = 2
title = "我的博客"
contentDir = "content/zh"  # Required!

[zh.params]
description = "我的博客描述"
```

### Important Notes

- `contentDir` is **required** for each language
- Default language (weight = 1) URLs don't include language prefix
- Other language URLs include prefix (e.g., `/zh/post/`)

## Menu Configuration

### English Menu (menus.en.toml)

```toml
[[main]]
name = "Posts"
url = "/post/"      # No /en/ prefix for default language!
weight = 1

[[main]]
name = "Tags"
url = "/tags/"
weight = 2

[[main]]
name = "Archives"
url = "/archives/"
weight = 3

[[main]]
name = "About"
url = "/about/"
weight = 4

[[main]]
name = "Search"
url = "/search/"
weight = 5
```

### Chinese Menu (menus.zh.toml)

```toml
[[main]]
name = "文章"
url = "/zh/post/"   # Include /zh/ prefix for non-default language!
weight = 1

[[main]]
name = "标签"
url = "/zh/tags/"
weight = 2

[[main]]
name = "归档"
url = "/zh/archives/"
weight = 3

[[main]]
name = "关于"
url = "/zh/about/"
weight = 4

[[main]]
name = "搜索"
url = "/zh/search/"
weight = 5
```

### Menu URL Rules

- **Default language** (English): No language prefix (e.g., `/post/`)
- **Other languages** (Chinese): Include language prefix (e.g., `/zh/post/`)

## Theme Parameters (params.toml)

### Basic Information

```toml
description = "Your blog description"
readmeUrl = "https://github.com/yourusername/your-repo"
showArchives = true      # Show archives page
showBackButton = true    # Show back button on posts
postPerIndex = 4         # Number of posts on homepage
```

### Theme Settings

```toml
[theme]
defaultTheme = "light"   # Options: light, dark, auto
switchTheme = true       # Allow users to switch theme
```

### Header Configuration

```toml
[header]
logo = "/logo.svg"       # Optional logo path
logoText = "My Blog"     # Logo text (if no logo image)
```

### Edit Post Link

```toml
[editPost]
enabled = true
text = "Edit this page"
url = "https://github.com/yourusername/your-repo/edit/main/content/"
appendFilePath = true    # Append file path to URL
```

### Social Links

```toml
[[social]]
name = "GitHub"
href = "https://github.com/yourusername"
linkTitle = "Follow me on GitHub"

[[social]]
name = "X"
href = "https://x.com/yourusername"
linkTitle = "Follow me on X"

[[social]]
name = "Mail"
href = "mailto:your@email.com"
linkTitle = "Send me an email"

[[social]]
name = "RSS"
href = "/index.xml"
linkTitle = "Subscribe via RSS"
```

Available social icons:
- GitHub
- X (Twitter)
- Mail
- RSS
- LinkedIn
- Facebook
- Instagram
- YouTube
- Telegram
- Discord

### Comments (Giscus)

```toml
[comments]
enable = true
provider = "giscus"
repo = "yourusername/your-repo"
repoId = "R_..."
category = "Announcements"
categoryId = "DIC_..."
mapping = "pathname"
strict = "0"
reactionsEnabled = "1"
emitMetadata = "0"
inputPosition = "bottom"
theme = "preferred_color_scheme"
lang = "en"
```

Get your Giscus configuration at: https://giscus.app/

### Analytics

```toml
[analytics]
googleAnalytics = "G-XXXXXXXXXX"  # Google Analytics ID
```

### Search

```toml
[search]
enable = true
maxResults = 10
```

## Markdown Configuration (markup.toml)

### Goldmark (Markdown Parser)

```toml
[goldmark]
  [goldmark.renderer]
    unsafe = true  # Allow raw HTML in Markdown

  [goldmark.parser]
    [goldmark.parser.attribute]
      block = true
      title = true

[highlight]
  anchorLineNos = false
  codeFences = true
  guessSyntax = false
  hl_Lines = ""
  hl_inline = false
  lineAnchors = ""
  lineNoStart = 1
  lineNos = false
  lineNumbersInTable = true
  noClasses = false
  noHl = false
  style = "monokai"
  tabWidth = 4
```

### Table of Contents

```toml
[tableOfContents]
  endLevel = 3
  ordered = false
  startLevel = 2
```

## Module Configuration (module.toml)

```toml
[[imports]]
path = "github.com/ouraihub-hugo-themes/hugo-theme-paper-dist"
```

This imports the pre-compiled distribution version of the theme.

## Front Matter Configuration

### Post Front Matter

```yaml
---
title: "Post Title"
description: "Brief description"
date: 2024-01-15T10:00:00+08:00
draft: false
featured: true
author: "Author Name"
categories:
  - Technology
tags:
  - Hugo
  - Blog
cover:
  image: "/images/cover.jpg"
  alt: "Cover image description"
  caption: "Image caption"
  relative: false
---
```

### Page Front Matter

```yaml
---
title: "Page Title"
date: 2024-01-15
layout: "page"
---
```

## Custom Styles

### Override Theme Styles

Create `assets/css/custom.css`:

```css
/* Custom styles */
:root {
  --accent: #ff6b01;  /* Change accent color */
}

/* Custom classes */
.my-custom-class {
  /* Your styles */
}
```

### Include Custom CSS

Create `layouts/partials/head-custom.html`:

```html
<link rel="stylesheet" href="{{ "css/custom.css" | relURL }}" />
```

## Custom Layouts

### Override Theme Layouts

To customize a layout, copy it from the theme and modify:

```
layouts/
└── _default/
    └── single.html  # Override single post layout
```

### Custom Shortcodes

Create custom shortcodes in `layouts/shortcodes/`:

```
layouts/shortcodes/
└── myshortcode.html
```

## Environment Variables

### Development

```bash
HUGO_ENV=development hugo server
```

### Production

```bash
HUGO_ENV=production hugo --minify
```

## Advanced Configuration

### Custom Permalinks

```toml
[permalinks]
  post = "/:year/:month/:slug/"
```

### Related Content

```toml
[related]
  includeNewer = true
  threshold = 80
  toLower = false

  [[related.indices]]
    name = "tags"
    weight = 100

  [[related.indices]]
    name = "categories"
    weight = 50
```

### Image Processing

```toml
[imaging]
  resampleFilter = "Lanczos"
  quality = 85
  anchor = "Smart"
```

## Configuration Best Practices

1. **Keep sensitive data out of config**
   - Use environment variables for API keys
   - Don't commit secrets to Git

2. **Use modular configuration**
   - Separate concerns into different files
   - Easier to maintain and understand

3. **Document your changes**
   - Add comments to explain custom settings
   - Keep a changelog

4. **Test before deploying**
   - Always test locally first
   - Use `hugo --minify` to test production build

5. **Version control**
   - Commit `go.mod` and `go.sum`
   - Don't commit `public/` or `resources/`

## Troubleshooting

### Configuration not taking effect

```bash
# Clear cache and rebuild
hugo mod clean
rm -rf resources/_gen
hugo --gc
```

### Menu not showing

- Check `contentDir` in `languages.toml`
- Verify menu URLs match your content structure
- Ensure `_index.md` files exist for sections

### Theme not loading

```bash
# Reinitialize modules
hugo mod clean
hugo mod get -u
hugo mod tidy
```

## Next Steps

- [Getting Started Guide](GETTING_STARTED.md) - Setup and installation
- [Deployment Guide](DEPLOYMENT.md) - Deploy your site
- [Theme Documentation](https://github.com/ouraihub-hugo-themes/hugo-theme-paper) - Full theme docs

## Getting Help

- **Documentation**: https://github.com/ouraihub-hugo-themes/hugo-theme-paper
- **Issues**: https://github.com/ouraihub-hugo-themes/hugo-theme-paper/issues
- **Discussions**: https://github.com/ouraihub-hugo-themes/hugo-theme-paper/discussions
