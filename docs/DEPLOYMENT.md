# 部署指南

本文档说明如何将站点部署到 GitHub Pages。

## 部署到 GitHub Pages

### 方式 1：部署到用户/组织站点（推荐）

部署到 `<username>.github.io` 仓库，站点 URL 为 `https://<username>.github.io`

#### 前置要求

1. **创建目标仓库**
   - 仓库名必须是：`<username>.github.io`
   - 例如：`hugopaper.github.io`

2. **创建 Personal Access Token**
   - 访问：GitHub Settings → Developer settings → Personal access tokens
   - 生成新 token，勾选 `repo` 权限
   - 复制 token（只显示一次）

3. **配置 Secret**
   - 在本仓库 Settings → Secrets and variables → Actions
   - 添加 Secret：
     - Name: `DEPLOY_TOKEN`
     - Value: 粘贴 token

#### 配置工作流

编辑 `.github/workflows/deploy.yml`：

```yaml
- name: Deploy to GitHub Pages
  uses: peaceiris/actions-gh-pages@v4
  with:
    personal_token: ${{ secrets.DEPLOY_TOKEN }}
    external_repository: <username>/<username>.github.io  # 修改为你的仓库
    publish_branch: main
    publish_dir: ./public
```

#### 配置 baseURL

编辑 `config/_default/hugo.toml`：

```toml
baseURL = "https://<username>.github.io/"
```

### 方式 2：部署到项目站点

部署到本仓库的 `gh-pages` 分支，站点 URL 为 `https://<username>.github.io/<repo-name>`

#### 配置工作流

编辑 `.github/workflows/deploy.yml`：

```yaml
- name: Deploy to GitHub Pages
  uses: peaceiris/actions-gh-pages@v4
  with:
    github_token: ${{ secrets.GITHUB_TOKEN }}  # 使用内置 token
    publish_branch: gh-pages
    publish_dir: ./public
```

#### 配置 baseURL

编辑 `config/_default/hugo.toml`：

```toml
baseURL = "https://<username>.github.io/<repo-name>/"
```

#### 启用 GitHub Pages

1. 进入仓库 Settings → Pages
2. Source: 选择 `gh-pages` 分支
3. 保存

## 自定义域名（可选）

### 1. 配置工作流

在 `.github/workflows/deploy.yml` 中添加：

```yaml
- name: Deploy to GitHub Pages
  uses: peaceiris/actions-gh-pages@v4
  with:
    # ...
    cname: yourdomain.com  # 你的域名
```

### 2. 配置 DNS

在域名提供商处添加 DNS 记录：

**A 记录**（根域名）：
```
@  A  185.199.108.153
@  A  185.199.109.153
@  A  185.199.110.153
@  A  185.199.111.153
```

**CNAME 记录**（www 子域名）：
```
www  CNAME  <username>.github.io.
```

### 3. 配置 baseURL

编辑 `config/_default/hugo.toml`：

```toml
baseURL = "https://yourdomain.com/"
```

### 4. 启用 HTTPS

在 GitHub 仓库 Settings → Pages：
- 勾选 "Enforce HTTPS"

## 部署流程

### 自动部署

推送到 `master` 或 `main` 分支会自动触发部署：

```bash
git add .
git commit -m "feat: 添加新文章"
git push origin master
```

### 手动部署

1. 进入 GitHub Actions 页面
2. 选择工作流
3. 点击 "Run workflow"

## 验证部署

### 检查工作流

1. 进入 Actions 标签页
2. 查看最新的工作流运行
3. 确保所有步骤成功

### 访问站点

- 用户站点：`https://<username>.github.io`
- 项目站点：`https://<username>.github.io/<repo-name>`
- 自定义域名：`https://yourdomain.com`

## 其他平台部署

### Vercel

1. 导入 GitHub 仓库
2. 构建命令：`hugo --minify --gc`
3. 输出目录：`public`
4. 自动部署

### Netlify

1. 连接 GitHub 仓库
2. 构建命令：`hugo --minify --gc`
3. 发布目录：`public`
4. Hugo 版本：在 `netlify.toml` 中指定

### Cloudflare Pages

1. 连接 GitHub 仓库
2. 构建命令：`hugo --minify --gc`
3. 构建输出目录：`public`
4. 环境变量：`HUGO_VERSION=0.120.0`

## 故障排除

### 部署失败 - 权限错误

**原因**：Token 权限不足或已过期

**解决**：
1. 检查 `DEPLOY_TOKEN` 配置
2. 确认 token 有 `repo` 权限
3. 重新生成 token

### 站点显示 404

**原因**：GitHub Pages 未启用或分支错误

**解决**：
1. 检查 Settings → Pages 配置
2. 确认部署到正确的分支
3. 等待几分钟让 GitHub Pages 生效

### 样式/资源加载失败

**原因**：baseURL 配置错误

**解决**：
1. 检查 `config/_default/hugo.toml` 中的 `baseURL`
2. 确保 URL 以 `/` 结尾
3. 重新构建和部署

### Hugo Modules 更新失败

**原因**：网络问题或模块不存在

**解决**：
1. 检查 `go.mod` 中的模块路径
2. 手动运行：`hugo mod get -u`
3. 清理缓存：`hugo mod clean`

## 本地测试

部署前本地测试：

```bash
# 更新模块
hugo mod get -u

# 构建
hugo --minify --gc

# 预览
hugo server --disableLiveReload
```

## 最佳实践

1. ✅ 在本地测试后再推送
2. ✅ 使用有意义的 commit message
3. ✅ 定期更新 Hugo Modules
4. ✅ 监控工作流状态
5. ✅ 备份重要内容

## 参考资源

- [GitHub Pages 文档](https://docs.github.com/en/pages)
- [Hugo 部署文档](https://gohugo.io/hosting-and-deployment/)
- [自定义域名配置](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
