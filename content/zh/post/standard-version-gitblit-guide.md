---
title: "使用 standard-version 实现自动化版本管理和 CHANGELOG 生成"
description: "详细教程：如何在 Gitblit 等 Git 服务器上使用 standard-version 实现自动化版本管理、CHANGELOG 生成和语义化版本控制，适用于任何 Git 平台"
date: 2025-11-15T14:00:00+08:00
draft: false
tags: 
  - Git
  - 版本管理
  - 自动化
  - DevOps
  - Gitblit
  - standard-version
  - CHANGELOG
  - 语义化版本
categories:
  - 开发工具
  - 最佳实践
author: "OurAIHub"
featured: true
keywords:
  - standard-version
  - 自动化版本管理
  - CHANGELOG 生成
  - Gitblit
  - 语义化版本
  - Conventional Commits
  - Git 版本控制
  - 自动化发布
  - 版本号管理
  - Git 工作流
---

## 前言

在软件开发过程中，版本管理和变更日志（CHANGELOG）的维护是一项重要但繁琐的工作。手动更新版本号、编写 CHANGELOG、创建 Git tag 不仅耗时，还容易出错。

本文将介绍如何使用 `standard-version` 实现自动化版本管理，让你只需一条命令就能完成版本发布的所有工作。**重要的是，这个工具不依赖特定的 Git 平台，无论你使用 GitHub、GitLab、Gitblit 还是其他 Git 服务器，都可以使用。**

## 什么是 standard-version？

`standard-version` 是一个基于 [Conventional Commits](https://www.conventionalcommits.org/) 规范的自动化版本管理工具。它可以：

- ✅ 自动分析 Git commit 历史
- ✅ 根据 commit 类型自动升级版本号
- ✅ 自动生成和更新 CHANGELOG.md
- ✅ 自动创建 Git tag
- ✅ 支持所有 Git 平台（GitHub、GitLab、Gitblit 等）

## 核心优势

### 1. 平台无关

`standard-version` 只依赖 Git，不依赖任何特定的 Git 托管平台：

- ✅ **GitHub** - 完美支持
- ✅ **GitLab** - 完美支持
- ✅ **Gitblit** - 完美支持
- ✅ **Gitea** - 完美支持
- ✅ **本地 Git 仓库** - 完美支持
- ✅ **任何 Git 服务器** - 完美支持

### 2. 完全自动化

一条命令完成所有工作：

```bash
pnpm release
```

自动执行：
1. 分析 commit 历史
2. 确定版本号升级类型
3. 更新 package.json
4. 生成/更新 CHANGELOG.md
5. 创建 Git commit
6. 创建 Git tag
7. 推送到远程仓库

### 3. 语义化版本

遵循 [Semantic Versioning](https://semver.org/) 规范：

- `feat:` → 升级 **minor** 版本（1.0.0 → 1.1.0）
- `fix:` → 升级 **patch** 版本（1.0.0 → 1.0.1）
- `BREAKING CHANGE:` → 升级 **major** 版本（1.0.0 → 2.0.0）

## 安装和配置

### 前置要求

- Node.js 18.0+
- Git
- pnpm/npm/yarn（任选其一）

### 步骤 1：安装依赖

```bash
# 使用 pnpm（推荐）
pnpm add -D standard-version

# 或使用 npm
npm install --save-dev standard-version

# 或使用 yarn
yarn add -D standard-version
```

### 步骤 2：配置 package.json

在 `package.json` 中添加发布脚本：

```json
{
  "name": "your-project",
  "version": "1.0.0",
  "scripts": {
    "release": "standard-version && git push --follow-tags origin master",
    "release:minor": "standard-version --release-as minor && git push --follow-tags origin master",
    "release:major": "standard-version --release-as major && git push --follow-tags origin master",
    "release:patch": "standard-version --release-as patch && git push --follow-tags origin master",
    "release:first": "standard-version --first-release && git push --follow-tags origin master"
  },
  "repository": {
    "type": "git",
    "url": "https://your-git-server.com/your-repo.git"
  }
}
```

**注意**：
- 将 `origin master` 改为你的远程仓库名和分支名
- 如果使用 `main` 分支，改为 `origin main`
- `repository.url` 填写你的 Git 仓库地址（GitHub/GitLab/Gitblit 等）

### 步骤 3：创建配置文件（可选）

创建 `.versionrc.json` 文件来自定义配置：

```json
{
  "header": "# 更新日志\n\n本项目的所有重要更改都将记录在此文件中。\n",
  "types": [
    {"type": "feat", "section": "✨ 新功能"},
    {"type": "fix", "section": "🐛 Bug 修复"},
    {"type": "docs", "section": "📝 文档"},
    {"type": "style", "section": "💄 样式"},
    {"type": "refactor", "section": "♻️ 重构"},
    {"type": "perf", "section": "⚡️ 性能优化"},
    {"type": "test", "section": "✅ 测试"},
    {"type": "build", "section": "📦 构建"},
    {"type": "ci", "section": "👷 CI/CD"},
    {"type": "chore", "section": "🔧 其他"}
  ]
}
```

## Gitblit 特殊配置

如果你使用 Gitblit，可能需要自定义链接格式。

### 方案 1：配置 Gitblit 链接

在 `.versionrc.json` 中添加：

```json
{
  "types": [
    {"type": "feat", "section": "✨ 新功能"},
    {"type": "fix", "section": "🐛 Bug 修复"},
    {"type": "docs", "section": "📝 文档"},
    {"type": "chore", "section": "🔧 其他"}
  ],
  "commitUrlFormat": "https://your-gitblit.com/commit?r={{repository}}&h={{hash}}",
  "compareUrlFormat": "https://your-gitblit.com/compare?r={{repository}}&h={{previousTag}}..{{currentTag}}",
  "userUrlFormat": "https://your-gitblit.com/user/{{user}}"
}
```

**替换说明**：
- `your-gitblit.com` → 你的 Gitblit 服务器地址
- `{{repository}}` → 仓库名称（自动替换）
- `{{hash}}` → commit hash（自动替换）
- `{{previousTag}}` → 上一个版本 tag（自动替换）
- `{{currentTag}}` → 当前版本 tag（自动替换）

### 方案 2：不使用链接（推荐）

如果 Gitblit 的 Web UI 不支持这些链接，或者你不需要链接，可以简化配置：

```json
{
  "types": [
    {"type": "feat", "section": "✨ 新功能"},
    {"type": "fix", "section": "🐛 Bug 修复"},
    {"type": "docs", "section": "📝 文档"},
    {"type": "style", "section": "💄 样式"},
    {"type": "refactor", "section": "♻️ 重构"},
    {"type": "perf", "section": "⚡️ 性能优化"},
    {"type": "test", "section": "✅ 测试"},
    {"type": "chore", "section": "🔧 其他"}
  ]
}
```

这样生成的 CHANGELOG 只包含纯文本，不包含链接。

## Conventional Commits 规范

为了让 `standard-version` 正确工作，你的 commit message 需要遵循 Conventional Commits 规范。

### 基本格式

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Commit 类型

| 类型 | 说明 | 版本升级 | 示例 |
|------|------|----------|------|
| `feat` | 新功能 | minor | `feat(search): 添加全文搜索功能` |
| `fix` | Bug 修复 | patch | `fix(theme): 修复深色模式按钮颜色` |
| `docs` | 文档更新 | - | `docs(readme): 更新安装说明` |
| `style` | 代码格式 | - | `style: 格式化代码` |
| `refactor` | 重构 | - | `refactor(api): 重构用户认证逻辑` |
| `perf` | 性能优化 | patch | `perf(db): 优化数据库查询` |
| `test` | 测试 | - | `test(auth): 添加登录测试` |
| `build` | 构建系统 | - | `build: 升级 webpack 到 v5` |
| `ci` | CI/CD | - | `ci: 添加自动部署脚本` |
| `chore` | 其他 | - | `chore(deps): 升级依赖` |

### 示例

#### 新功能
```bash
git commit -m "feat(user): 添加用户头像上传功能"
```

#### Bug 修复
```bash
git commit -m "fix(login): 修复登录页面验证码不显示的问题"
```

#### 文档更新
```bash
git commit -m "docs(api): 更新 API 文档"
```

#### 破坏性更改（升级 major 版本）
```bash
git commit -m "feat(api): 重构 API 接口

BREAKING CHANGE: API 路径从 /api/v1 改为 /api/v2"
```

## 使用方法

### 日常开发流程

```bash
# 1. 开发功能
# 编辑代码...

# 2. 提交代码（遵循 Conventional Commits）
git add .
git commit -m "feat(dashboard): 添加数据统计图表"

# 3. 继续开发和提交
git commit -m "fix(chart): 修复图表数据显示错误"
git commit -m "docs(readme): 更新使用说明"

# 4. 准备发布新版本
pnpm release

# 完成！版本号已更新，CHANGELOG 已生成，tag 已创建并推送
```

### 发布命令

#### 自动升级版本（推荐）
```bash
pnpm release
```
根据 commit 类型自动决定升级 major/minor/patch。

#### 手动指定版本类型
```bash
# 升级 patch 版本（1.0.0 → 1.0.1）
pnpm release:patch

# 升级 minor 版本（1.0.0 → 1.1.0）
pnpm release:minor

# 升级 major 版本（1.0.0 → 2.0.0）
pnpm release:major
```

#### 首次发布
```bash
pnpm release:first
```
不升级版本号，只生成 CHANGELOG 和 tag。

#### 预发布版本
```bash
# 生成 1.0.0-alpha.0
pnpm standard-version --prerelease alpha

# 生成 1.0.0-beta.0
pnpm standard-version --prerelease beta
```

### 测试模式（不实际修改文件）

```bash
# 查看会生成什么，但不实际修改文件
pnpm standard-version --dry-run

# 查看详细输出
pnpm standard-version --dry-run --verbose
```

## 生成的 CHANGELOG 示例

运行 `pnpm release` 后，会自动生成/更新 `CHANGELOG.md`：

```markdown
# 更新日志

本项目的所有重要更改都将记录在此文件中。

### [1.2.0](https://your-git-server.com/compare/v1.1.0...v1.2.0) (2025-11-15)

### ✨ 新功能

* **dashboard:** 添加数据统计图表 ([a1b2c3d](https://your-git-server.com/commit/a1b2c3d))
* **user:** 添加用户头像上传功能 ([e4f5g6h](https://your-git-server.com/commit/e4f5g6h))

### 🐛 Bug 修复

* **chart:** 修复图表数据显示错误 ([i7j8k9l](https://your-git-server.com/commit/i7j8k9l))
* **login:** 修复登录页面验证码不显示的问题 ([m0n1o2p](https://your-git-server.com/commit/m0n1o2p))

### 📝 文档

* **readme:** 更新使用说明 ([q3r4s5t](https://your-git-server.com/commit/q3r4s5t))
* **api:** 更新 API 文档 ([u6v7w8x](https://your-git-server.com/commit/u6v7w8x))

### [1.1.0](https://your-git-server.com/compare/v1.0.0...v1.1.0) (2025-11-10)

...
```

## 高级配置

### 跳过某些步骤

在 `.versionrc.json` 中配置：

```json
{
  "skip": {
    "bump": false,      // 不跳过版本号升级
    "changelog": false, // 不跳过 CHANGELOG 生成
    "commit": false,    // 不跳过 Git commit
    "tag": false        // 不跳过 Git tag
  }
}
```

### 自定义 commit message

```json
{
  "releaseCommitMessageFormat": "chore(release): 发布 {{currentTag}}"
}
```

### 包含/排除文件

```json
{
  "bumpFiles": [
    {
      "filename": "package.json",
      "type": "json"
    },
    {
      "filename": "version.txt",
      "updater": "version.js"
    }
  ]
}
```

### 自定义版本号格式

```json
{
  "tagPrefix": "v",
  "releaseAs": "minor"
}
```

## Git 认证配置

### HTTP(S) 认证

```bash
# 方式 1：使用 credential helper
git config --global credential.helper store

# 第一次推送时输入用户名和密码，之后会自动保存
git push

# 方式 2：在 URL 中包含认证信息（不推荐）
git remote set-url origin https://username:password@your-gitblit.com/repo.git
```

### SSH 认证（推荐）

```bash
# 1. 生成 SSH 密钥
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

# 2. 将公钥添加到 Gitblit
cat ~/.ssh/id_rsa.pub

# 3. 修改远程仓库地址
git remote set-url origin git@your-gitblit.com:repo.git

# 4. 测试连接
ssh -T git@your-gitblit.com
```

## 团队协作

### 1. 统一 Commit 规范

在项目根目录创建 `.commitlintrc.json`：

```json
{
  "extends": ["@commitlint/config-conventional"],
  "rules": {
    "type-enum": [
      2,
      "always",
      [
        "feat",
        "fix",
        "docs",
        "style",
        "refactor",
        "perf",
        "test",
        "build",
        "ci",
        "chore"
      ]
    ]
  }
}
```

安装 commitlint：

```bash
pnpm add -D @commitlint/cli @commitlint/config-conventional
```

### 2. 使用 Git Hooks

安装 husky：

```bash
pnpm add -D husky
pnpm husky install
```

添加 commit-msg hook：

```bash
pnpm husky add .husky/commit-msg 'npx --no -- commitlint --edit ${1}'
```

现在，不符合规范的 commit 会被拒绝：

```bash
git commit -m "update code"
# ❌ 错误：commit message 不符合规范

git commit -m "feat: 添加新功能"
# ✅ 成功
```

### 3. 使用 Commitizen（可选）

安装 commitizen：

```bash
pnpm add -D commitizen cz-conventional-changelog
```

配置 `package.json`：

```json
{
  "scripts": {
    "commit": "cz"
  },
  "config": {
    "commitizen": {
      "path": "cz-conventional-changelog"
    }
  }
}
```

使用交互式提交：

```bash
git add .
pnpm commit

# 会出现交互式提示，引导你填写规范的 commit message
```

## 故障排除

### 问题 1：推送失败

**错误**：
```
fatal: unable to access 'https://...': Could not resolve host
```

**解决**：
1. 检查网络连接
2. 检查 Git 仓库地址是否正确
3. 检查认证信息是否正确

### 问题 2：版本号没有升级

**原因**：没有符合规范的 commit

**解决**：
```bash
# 查看自上次 tag 以来的 commits
git log $(git describe --tags --abbrev=0)..HEAD --oneline

# 确保至少有一个 feat: 或 fix: 类型的 commit
```

### 问题 3：CHANGELOG 没有生成

**原因**：`.versionrc.json` 配置错误

**解决**：
```bash
# 删除配置文件，使用默认配置
rm .versionrc.json

# 重新运行
pnpm release
```

### 问题 4：Tag 已存在

**错误**：
```
fatal: tag 'v1.0.0' already exists
```

**解决**：
```bash
# 删除本地 tag
git tag -d v1.0.0

# 删除远程 tag
git push origin :refs/tags/v1.0.0

# 重新发布
pnpm release
```

## 最佳实践

### 1. Commit Message 规范

✅ **好的示例**：
```bash
feat(auth): 添加 OAuth2 登录支持
fix(ui): 修复移动端菜单显示问题
docs(api): 更新 REST API 文档
perf(db): 优化用户查询性能
```

❌ **不好的示例**：
```bash
update code
fix bug
add feature
修改文件
```

### 2. 发布频率

- **小版本（patch）**：每周或每两周发布一次
- **中版本（minor）**：每月或每季度发布一次
- **大版本（major）**：有破坏性更改时发布

### 3. 版本号策略

遵循 [Semantic Versioning](https://semver.org/)：

- **MAJOR**（主版本号）：不兼容的 API 修改
- **MINOR**（次版本号）：向下兼容的功能性新增
- **PATCH**（修订号）：向下兼容的问题修正

### 4. CHANGELOG 维护

- ✅ 自动生成，不要手动编辑
- ✅ 每次发布都更新
- ✅ 包含在版本控制中
- ✅ 在 README 中链接到 CHANGELOG

### 5. Tag 管理

- ✅ 使用 `v` 前缀（v1.0.0）
- ✅ 每个版本都打 tag
- ✅ Tag 和版本号保持一致
- ✅ 不要删除已发布的 tag

## 与 CI/CD 集成

### GitHub Actions 示例

```yaml
name: Release

on:
  workflow_dispatch:

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      
      - uses: actions/setup-node@v4
        with:
          node-version: '18'
      
      - name: Install dependencies
        run: npm install
      
      - name: Release
        run: |
          git config user.name "GitHub Actions"
          git config user.email "actions@github.com"
          npm run release
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### GitLab CI 示例

```yaml
release:
  stage: release
  only:
    - master
  script:
    - npm install
    - git config user.name "GitLab CI"
    - git config user.email "ci@gitlab.com"
    - npm run release
  when: manual
```

## 总结

`standard-version` 是一个强大而灵活的版本管理工具，它：

- ✅ **平台无关** - 支持所有 Git 服务器（GitHub、GitLab、Gitblit 等）
- ✅ **完全自动化** - 一条命令完成所有工作
- ✅ **规范化** - 强制使用 Conventional Commits 和 Semantic Versioning
- ✅ **可定制** - 支持自定义配置
- ✅ **易于集成** - 可与 CI/CD 无缝集成

通过使用 `standard-version`，你可以：

1. 节省时间 - 不再手动维护 CHANGELOG
2. 减少错误 - 自动化流程避免人为失误
3. 提高质量 - 规范的 commit 和版本管理
4. 改善协作 - 团队成员遵循统一规范

## 参考资源

- [standard-version 官方文档](https://github.com/conventional-changelog/standard-version)
- [Conventional Commits 规范](https://www.conventionalcommits.org/)
- [Semantic Versioning 规范](https://semver.org/)
- [commitlint 文档](https://commitlint.js.org/)
- [Gitblit 官方网站](https://gitblit.com/)

## 相关文章

- [Git 工作流最佳实践](/post/git-workflow-best-practices/)
- [如何编写优秀的 Commit Message](/post/writing-good-commit-messages/)
- [语义化版本控制详解](/post/semantic-versioning-guide/)

---

**标签**：#Git #版本管理 #自动化 #DevOps #Gitblit #CHANGELOG

**关键词**：standard-version, 自动化版本管理, CHANGELOG 生成, Gitblit, 语义化版本, Conventional Commits, Git 版本控制
