# 快速设置 GitHub Pages 部署

## 一分钟设置指南

### 步骤 1：创建 Personal Access Token

1. 访问：https://github.com/settings/tokens/new
2. 设置：
   - Note: `Deploy to GitHub Pages`
   - Expiration: `90 days` 或更长
   - Scopes: 勾选 `repo`
3. 点击 "Generate token"
4. **复制 token**（只显示一次！）

### 步骤 2：添加 Secret

1. 进入本仓库 Settings → Secrets and variables → Actions
2. 点击 "New repository secret"
3. 添加：
   - Name: `DEPLOY_TOKEN`
   - Secret: 粘贴刚才的 token
4. 点击 "Add secret"

### 步骤 3：配置工作流

编辑 `.github/workflows/deploy.yml`，修改目标仓库：

```yaml
external_repository: <username>/<username>.github.io  # 改成你的
```

### 步骤 4：配置 baseURL

编辑 `config/_default/hugo.toml`：

```toml
baseURL = "https://<username>.github.io/"  # 改成你的
```

### 步骤 5：推送代码

```bash
git add .
git commit -m "feat: 配置部署"
git push origin master
```

### 步骤 6：等待部署

1. 进入 Actions 页面
2. 等待工作流完成（约 1-2 分钟）
3. 访问你的站点

## 完成！🎉

你的站点现在已经部署到 GitHub Pages。

每次推送到 `master` 分支都会自动重新部署。

## 下一步

- 📝 添加新文章
- ⚙️ [配置站点](./CONFIGURATION.md)
- 🌐 [设置自定义域名](./DEPLOYMENT.md#自定义域名可选)

## 需要帮助？

查看完整文档：[DEPLOYMENT.md](./DEPLOYMENT.md)
