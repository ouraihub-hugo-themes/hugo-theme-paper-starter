# 主题更新指南

本文档说明如何更新 Hugo Paper 主题到最新版本。

## 自动更新机制

### 部署时自动使用最新版本

每次推送代码触发部署时，GitHub Actions 会自动：

1. ✅ 获取最新版本的主题 (`hugo mod get -u`)
2. ✅ 使用最新版本构建站点
3. ✅ 部署到 GitHub Pages

**优点**：
- 部署的站点始终使用最新主题
- 自动获取 bug 修复和新功能
- 无需手动操作

**注意**：
- 本地 `go.mod` 不会自动更新
- 本地测试可能使用旧版本主题

## 手动更新本地主题

### 何时需要手动更新？

- 想在本地测试新主题功能
- 本地开发时遇到问题（可能已在新版本修复）
- 想确保本地和线上版本一致

### 更新步骤

```bash
# 1. 更新主题到最新版本
hugo mod get -u

# 2. 清理缓存
hugo mod clean

# 3. 验证更新
hugo mod graph

# 4. 本地测试
hugo server

# 5. 如果测试通过，提交更新
git add go.mod go.sum
git commit -m "chore: 更新主题到最新版本"
git push
```

### 查看当前主题版本

```bash
# 查看 go.mod 中的版本
grep hugo-theme-paper-dist go.mod

# 输出示例：
# require github.com/ouraihub-hugo-themes/hugo-theme-paper-dist v0.7.4
```

## 更新到特定版本

### 更新到指定版本

```bash
# 更新到 v0.7.4
hugo mod get github.com/ouraihub-hugo-themes/hugo-theme-paper-dist@v0.7.4

# 提交
git add go.mod go.sum
git commit -m "chore: 更新主题到 v0.7.4"
git push
```

### 回退到旧版本

```bash
# 回退到 v0.7.3
hugo mod get github.com/ouraihub-hugo-themes/hugo-theme-paper-dist@v0.7.3

# 提交
git add go.mod go.sum
git commit -m "chore: 回退主题到 v0.7.3"
git push
```

## 查看主题更新日志

### 方式 1：GitHub Releases

访问：https://github.com/ouraihub-hugo-themes/hugo-theme-paper/releases

查看每个版本的更新内容。

### 方式 2：对比版本

```bash
# 查看两个版本之间的差异
# 访问：
https://github.com/ouraihub-hugo-themes/hugo-theme-paper/compare/v0.7.3...v0.7.4
```

## 故障排除

### 问题 1：更新后站点样式错误

**原因**：新版本可能有破坏性更改

**解决**：
1. 查看 Release Notes 中的 Breaking Changes
2. 更新配置文件（如果需要）
3. 或回退到旧版本

```bash
# 回退
hugo mod get github.com/ouraihub-hugo-themes/hugo-theme-paper-dist@v0.7.3
```

### 问题 2：模块缓存问题

**错误信息**：
```
go: module github.com/.../hugo-theme-paper-dist: not found
```

**解决**：
```bash
# 清理缓存
hugo mod clean

# 重新获取
hugo mod get -u

# 或手动清理 Go 缓存
go clean -modcache
```

### 问题 3：本地和线上版本不一致

**现象**：本地测试正常，部署后有问题

**原因**：本地使用旧版本，线上使用新版本

**解决**：
```bash
# 更新本地到最新版本
hugo mod get -u

# 测试
hugo server

# 如果有问题，锁定版本
hugo mod get github.com/ouraihub-hugo-themes/hugo-theme-paper-dist@v0.7.3
git add go.mod go.sum
git commit -m "chore: 锁定主题版本到 v0.7.3"
git push
```

## 版本管理策略

### 策略 1：始终使用最新版本（默认）

**适合**：
- 个人博客
- 不介意偶尔的小问题
- 想要最新功能

**操作**：
- 不需要手动更新
- 部署时自动使用最新版本

### 策略 2：锁定特定版本

**适合**：
- 生产环境
- 需要稳定性
- 团队协作

**操作**：
```bash
# 1. 锁定到特定版本
hugo mod get github.com/ouraihub-hugo-themes/hugo-theme-paper-dist@v0.7.4

# 2. 提交
git add go.mod go.sum
git commit -m "chore: 锁定主题版本到 v0.7.4"
git push

# 3. 修改工作流（可选）
# 将 deploy.yml 中的 "hugo mod get -u" 改为 "hugo mod get"
# 这样部署时不会自动更新
```

### 策略 3：定期手动更新

**适合**：
- 想要控制更新时机
- 需要测试后再部署

**操作**：
1. 每月或每季度手动更新
2. 本地测试
3. 确认无问题后推送

## 最佳实践

1. ✅ **定期查看 Release Notes**
   - 了解新功能和 bug 修复
   - 注意破坏性更改

2. ✅ **重要更新前先测试**
   - 本地更新并测试
   - 确认无问题再推送

3. ✅ **记录主题版本**
   - 在 CHANGELOG 中记录主题更新
   - 方便追溯问题

4. ✅ **遇到问题及时反馈**
   - 在主题仓库提 Issue
   - 帮助改进主题

## 相关资源

- [主题开发仓库](https://github.com/ouraihub-hugo-themes/hugo-theme-paper)
- [主题分发仓库](https://github.com/ouraihub-hugo-themes/hugo-theme-paper-dist)
- [Hugo Modules 文档](https://gohugo.io/hugo-modules/)
- [部署工作流](.github/workflows/deploy.yml)

## 常见问题

### Q: 为什么部署时自动更新，但不提交到仓库？

A: 为了避免推送冲突。如果 Actions 自动提交，你本地推送时会遇到冲突。现在的方案更简单：部署时临时更新，不影响仓库。

### Q: 如何知道线上使用的是哪个版本？

A: 查看最近一次部署的 Actions 日志，搜索 "hugo mod get" 步骤，会显示获取的版本。

### Q: 可以禁用自动更新吗？

A: 可以。修改 `.github/workflows/deploy.yml`，将 `hugo mod get -u` 改为 `hugo mod get`（去掉 `-u`）。这样会使用 go.mod 中锁定的版本。

### Q: 更新主题会影响我的内容吗？

A: 不会。主题更新只影响样式和功能，不会修改 `content/` 目录中的文章内容。
