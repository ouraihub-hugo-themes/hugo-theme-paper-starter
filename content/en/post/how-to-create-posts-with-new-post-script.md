---
title: "How to Create SEO-Optimized Blog Posts with Hugo Paper's New-Post Script"
slug: "create-seo-optimized-posts-hugo-paper-new-post-script"
description: "Learn how to quickly create SEO-optimized blog posts using Hugo Paper's interactive new-post script. Complete guide with examples and best practices for content creation."
date: 2024-11-15T10:00:00+08:00
lastmod: 2024-11-15T10:00:00+08:00
author: "Hugo Paper Team"
keywords:
  - hugo-paper
  - new-post-script
  - blog-creation
  - seo-optimization
  - content-management
  - hugo-tutorial
  - typescript-scripts
  - automated-blogging
categories:
  - Tutorial
  - Documentation
tags:
  - hugo
  - blogging
  - seo
  - automation
  - productivity
featured: true
draft: false
cover: "https://source.unsplash.com/1200x630/?writing,blog,computer"
---

Creating blog posts with proper SEO optimization can be time-consuming. Hugo Paper's `new-post` script automates this process, helping you create well-structured, SEO-friendly posts in seconds.

## Table of Contents

## Why Use the New-Post Script?

Traditional blog post creation requires manually setting up frontmatter with numerous SEO fields. The `new-post` script streamlines this by:

- ✅ **Interactive prompts** - Guides you through all SEO fields
- ✅ **Automatic slug generation** - Creates SEO-friendly URLs
- ✅ **Timestamp management** - Adds proper date/time formats
- ✅ **Multilingual support** - Creates posts in English or Chinese
- ✅ **SEO best practices** - Ensures all required fields are present
- ✅ **Consistent structure** - Maintains uniform post format

## Prerequisites

Before using the script, ensure you have:

```bash
# Check Node.js version (18.0+)
node --version

# Check pnpm version (8.0+)
pnpm --version

# Install dependencies if needed
pnpm install
```

## Two Ways to Create Posts

Hugo Paper provides two scripts for different workflows:

### 1. Interactive Mode (Recommended)

The `new-post` script provides an interactive experience with prompts for all fields:

```bash
# Basic usage
pnpm new-post

# With title
pnpm new-post "Getting Started with Hugo"

# With title and language
pnpm new-post "Hugo Getting Started Guide" en
```

### 2. Quick Mode

The `quick-post` script uses sensible defaults for rapid post creation:

```bash
# Quick English post
pnpm quick-post "My Article Title"

# Quick Chinese post
pnpm quick-post "My Article Title" en
```

## Step-by-Step: Using New-Post

### Step 1: Run the Command

```bash
pnpm new-post "How to Build a Hugo Blog"
```

### Step 2: Follow the Prompts

The script will ask for:

#### 1. **Slug** (URL-friendly identifier)
```
Enter slug (press Enter for auto-generated): 
→ how-to-build-hugo-blog
```

**Best practices:**
- Use lowercase letters
- Separate words with hyphens
- Keep it short (3-5 words)
- Include main keyword

#### 2. **Description** (150-160 characters)
```
Enter description (150-160 chars for SEO): 
→ Learn how to build a professional blog with Hugo static site generator. 
  Step-by-step guide with examples and best practices.
```

**Best practices:**
- 150-160 characters (optimal for search results)
- Include primary keyword
- Make it compelling and actionable
- Avoid keyword stuffing

#### 3. **Keywords** (comma-separated)
```
Enter keywords (comma-separated, 3-5 recommended): 
→ hugo, static-site-generator, blog-tutorial, web-development
```

**Best practices:**
- 3-5 keywords maximum
- Mix broad and specific terms
- Include long-tail keywords
- Research with Google Keyword Planner

#### 4. **Author**
```
Enter author name: 
→ John Doe
```

#### 5. **Categories** (comma-separated)
```
Enter categories (comma-separated): 
→ Tutorial, Web Development
```

**Best practices:**
- 1-2 categories per post
- Use consistent category names
- Keep categories broad

#### 6. **Tags** (comma-separated)
```
Enter tags (comma-separated, 5-10 recommended): 
→ hugo, jamstack, static-site, blogging, tutorial, beginner-friendly
```

**Best practices:**
- 5-10 tags per post
- Mix general and specific tags
- Use tags for detailed topics

#### 7. **Featured Post**
```
Is this a featured post? (y/n): 
→ y
```

Featured posts appear prominently on your homepage.

#### 8. **Draft Status**
```
Is this a draft? (y/n): 
→ n
```

Set to `y` for unpublished posts.

### Step 3: Edit Your Post

The script creates a file at:
```
content/en/post/how-to-build-hugo-blog.md
```

Open it and start writing:

```markdown
---
title: "How to Build a Hugo Blog"
slug: "how-to-build-hugo-blog"
description: "Learn how to build a professional blog with Hugo..."
date: 2024-11-15T10:00:00+08:00
lastmod: 2024-11-15T10:00:00+08:00
author: "John Doe"
keywords:
  - hugo
  - static-site-generator
  - blog-tutorial
categories:
  - Tutorial
tags:
  - hugo
  - jamstack
featured: true
draft: false
---

## Introduction

Your content starts here...
```

## Quick-Post for Rapid Creation

When you need to create posts quickly without interactive prompts:

```bash
# Creates post with default values
pnpm quick-post "Quick Article Title"
```

**Default values:**
- Slug: Auto-generated from title
- Description: "Article about [title]"
- Keywords: Extracted from title
- Author: From site config
- Categories: ["Blog"]
- Tags: Extracted from title
- Featured: false
- Draft: true

**When to use quick-post:**
- Drafting multiple posts quickly
- Creating placeholder posts
- Rapid prototyping
- When you'll edit frontmatter later

## Multilingual Post Creation

### Creating Chinese Posts

```bash
# Interactive Chinese post
pnpm new-post "Hugo Blog Setup Guide" zh

# Quick Chinese post
pnpm quick-post "My Article" zh
```

The script automatically:
- Creates file in `content/zh/post/`
- Uses Chinese prompts
- Sets proper language metadata
- Generates Chinese-friendly slugs

### Language-Specific Best Practices

**English posts:**
- Use hyphens in slugs: `my-blog-post`
- Keywords in English
- 150-160 character descriptions

**Chinese posts:**
- Use pinyin or English in slugs: `hugo-blog-guide`
- Keywords can be Chinese or English
- 70-80 Chinese character descriptions

## SEO Optimization Tips

### 1. Title Optimization

**Good titles:**
- ✅ "How to Build a Hugo Blog: Complete Guide for Beginners"
- ✅ "10 Hugo Tips to Boost Your Site Performance"
- ✅ "Hugo vs Jekyll: Which Static Site Generator is Better?"

**Poor titles:**
- ❌ "My Blog Post"
- ❌ "Untitled"
- ❌ "Test Post 123"

**Best practices:**
- 50-60 characters
- Include primary keyword
- Make it compelling
- Use numbers when relevant

### 2. Description Optimization

**Good descriptions:**
```
Learn how to build a professional blog with Hugo static site generator. 
This step-by-step guide covers installation, configuration, and deployment 
with practical examples.
```

**Poor descriptions:**
```
This is a post about Hugo.
```

**Best practices:**
- 150-160 characters
- Include primary and secondary keywords
- Write for humans, not just search engines
- Include a call-to-action

### 3. Keyword Strategy

**Keyword research:**
1. Use Google Keyword Planner
2. Check competitor keywords
3. Use Google autocomplete
4. Check "People also ask"

**Keyword placement:**
- Title (primary keyword)
- Description (primary + secondary)
- Keywords field (3-5 keywords)
- First paragraph of content
- Headings (H2, H3)
- Image alt text

### 4. URL Structure

**Good slugs:**
- ✅ `how-to-build-hugo-blog`
- ✅ `hugo-vs-jekyll-comparison`
- ✅ `10-hugo-performance-tips`

**Poor slugs:**
- ❌ `post-1`
- ❌ `untitled-post`
- ❌ `my_blog_post_about_hugo_and_stuff`

## Advanced Usage

### Custom Templates

Create custom post templates by modifying the script:

```typescript
// scripts/new-post.ts
function generatePostContent(metadata: PostMetadata): string {
  return `## Introduction

Write your introduction here...

## Main Content

### Section 1

Content...

### Section 2

Content...

## Conclusion

Wrap up your post...

## References

- [Link 1](https://example.com)
- [Link 2](https://example.com)
`;
}
```

### Batch Post Creation

Create multiple posts with a shell script:

```bash
#!/bin/bash
# create-posts.sh

posts=(
  "First Post Title"
  "Second Post Title"
  "Third Post Title"
)

for post in "${posts[@]}"; do
  pnpm quick-post "$post"
done
```

### Integration with CI/CD

Automate post creation in your workflow:

```yaml
# .github/workflows/create-post.yml
name: Create Post

on:
  workflow_dispatch:
    inputs:
      title:
        description: 'Post title'
        required: true

jobs:
  create:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: pnpm/action-setup@v2
      - run: pnpm install
      - run: pnpm quick-post "${{ github.event.inputs.title }}"
      - uses: stefanzweifel/git-auto-commit-action@v4
```

## Troubleshooting

### Script Not Found

```bash
Error: Cannot find module 'scripts/new-post.ts'
```

**Solution:**
```bash
# Ensure you're in the theme directory
cd hugo-theme-paper

# Install dependencies
pnpm install
```

### Permission Denied

```bash
Error: EACCES: permission denied
```

**Solution:**
```bash
# Make script executable (Unix/Mac)
chmod +x scripts/new-post.ts

# Or run with tsx directly
npx tsx scripts/new-post.ts
```

### Invalid Date Format

```bash
Error: Invalid date format
```

**Solution:**
The script uses ISO 8601 format automatically. If you see this error, check your system timezone settings.

## Best Practices Checklist

Before publishing, ensure:

- [ ] **Title** - 50-60 characters, includes primary keyword
- [ ] **Slug** - SEO-friendly, lowercase, hyphens
- [ ] **Description** - 150-160 characters, compelling
- [ ] **Keywords** - 3-5 relevant keywords
- [ ] **Categories** - 1-2 broad categories
- [ ] **Tags** - 5-10 specific tags
- [ ] **Author** - Proper attribution
- [ ] **Featured** - Set if important post
- [ ] **Draft** - Set to false when ready
- [ ] **Cover image** - High-quality, relevant image
- [ ] **Content** - Well-structured with headings
- [ ] **Links** - Internal and external links
- [ ] **Images** - Optimized with alt text

## Comparison: Manual vs Script

| Aspect | Manual Creation | New-Post Script |
|--------|----------------|-----------------|
| Time | 5-10 minutes | 30 seconds |
| SEO fields | Often forgotten | Always included |
| Consistency | Varies | Uniform |
| Errors | Common | Rare |
| Learning curve | Low | Very low |
| Flexibility | High | High |

## Next Steps

Now that you know how to create posts efficiently:

1. **Read the SEO guide** - Learn advanced SEO optimization
2. **Configure OG images** - Set up dynamic social media images
3. **Customize templates** - Modify the script for your needs
4. **Create content** - Start writing amazing posts!

## Related Resources

- [Hugo Paper Documentation](https://github.com/ouraihub-hugo-themes/hugo-theme-paper)
- [SEO Optimization Guide](/post/seo-optimization-guide-hugo-paper)
- [Dynamic OG Images Guide](/post/dynamic-og-images-hugo-paper)
- [Hugo Official Docs](https://gohugo.io/documentation/)

## Conclusion

The `new-post` script is a powerful tool that saves time and ensures SEO best practices. By automating frontmatter creation, you can focus on what matters most: creating great content.

Start using it today and experience the difference in your content creation workflow!

---

**Questions or feedback?** Open an issue on [GitHub](https://github.com/ouraihub-hugo-themes/hugo-theme-paper/issues) or join our [discussions](https://github.com/ouraihub-hugo-themes/hugo-theme-paper/discussions).
