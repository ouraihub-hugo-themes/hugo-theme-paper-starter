# 🚀 部署设置指南

## 当前错误

```
Error: Action failed with "not found deploy key or tokens"
```

**原因**：缺少 `DEPLOY_TOKEN` Secret

## 快速设置（5 分钟）

### 步骤 1：创建 Personal Access Token

1. 访问：https://github.com/settings/tokens/new
2. 填写信息：
   - **Note**: `Deploy to hugopaper.github.io`
   - **Expiration**: 选择 `90 days` 或 `No expiration`
   - **Select scopes**: 勾选 `repo` (完整权限)
3. 点击 **"Generate token"**
4. **立即复制 token**（只显示一次！）

### 步骤 2：添加 Secret 到仓库

1. 访问：https://github.com/ouraihub-hugo-themes/hugo-theme-paper-starter/settings/secrets/actions
2. 点击 **"New repository secret"**
3. 填写：
   - **Name**: `DEPLOY_TOKEN`
   - **Secret**: 粘贴刚才复制的 token
4. 点击 **"Add secret"**

### 步骤 3：重新运行工作流

1. 访问：https://github.com/ouraihub-hugo-themes/hugo-theme-paper-starter/actions
2. 选择失败的工作流
3. 点击 **"Re-run all jobs"**

### 步骤 4：验证部署

等待 1-2 分钟后访问：https://hugopaper.github.io

## 详细说明

### 为什么需要 Token？

因为要部署到**另一个仓库** (`hugopaper/hugopaper.github.io`)，需要：
- 跨仓库写入权限
- Personal Access Token 提供这个权限

### Token 权限说明

需要勾选的权限：
- ✅ `repo` - 完整的仓库访问权限
  - `repo:status` - 访问提交状态
  - `repo_deployment` - 访问部署状态
  - `public_repo` - 访问公共仓库
  - `repo:invite` - 访问仓库邀请

### 安全建议

1. ✅ 使用有过期时间的 token
2. ✅ 定期更新 token
3. ✅ 不要在代码中硬编码 token
4. ✅ 使用 GitHub Secrets 存储

## 故障排除

### 问题 1：Token 无效

**错误信息**：
```
Error: Invalid token
```

**解决方案**：
1. 检查 token 是否正确复制
2. 确认 token 有 `repo` 权限
3. 重新生成 token

### 问题 2：权限不足

**错误信息**：
```
Error: Permission denied
```

**解决方案**：
1. 确认你有 `hugopaper/hugopaper.github.io` 仓库的写入权限
2. 如果是组织仓库，确认 token 有组织访问权限

### 问题 3：目标仓库不存在

**错误信息**：
```
Error: Repository not found
```

**解决方案**：
1. 创建 `hugopaper/hugopaper.github.io` 仓库
2. 确认仓库名称拼写正确

## 验证清单

设置完成后，检查：

- [ ] Personal Access Token 已创建
- [ ] Token 有 `repo` 权限
- [ ] Secret `DEPLOY_TOKEN` 已添加到仓库
- [ ] 目标仓库 `hugopaper/hugopaper.github.io` 存在
- [ ] 工作流重新运行成功
- [ ] 站点可以访问：https://hugopaper.github.io

## 需要帮助？

查看完整文档：
- [部署指南](docs/DEPLOYMENT.md)
- [快速设置](docs/SETUP_DEPLOYMENT.md)
- [GitHub Actions 文档](https://docs.github.com/en/actions)
