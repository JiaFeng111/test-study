# test-study 123456

一个包含 HTML、CSS 和 JavaScript 的单文件学习页面。

在线访问：[我的学习小站](https://jiafeng111.github.io/test-study/)

## GitHub Actions 自动部署

部署配置位于 [deploy-pages.yml](.github/workflows/deploy-pages.yml)。仓库的 **Settings → Pages → Build and deployment → Source** 使用 **GitHub Actions**。

每次推送到 `main` 分支后，GitHub 会自动执行以下流程：

1. 在 GitHub 提供的 Ubuntu 环境中获取仓库代码。
2. 将根目录的 `index.html` 复制到 `_site` 发布目录。
3. 上传 `_site` 中的静态文件。
4. 发布到 GitHub Pages，并在本次运行的部署环境中显示网站地址。

工作流使用 GitHub 自动生成的 `GITHUB_TOKEN`，无需手动添加 Secrets。

## 修改后如何更新网站

在本地修改 `index.html` 后，先用浏览器打开，确认效果，然后在仓库目录执行：

```bash
# 以下命令在 main 分支上执行。
git add index.html
git commit -m "更新学习页面"
git push origin main
```

打开仓库的 **Actions → Deploy to GitHub Pages**，查看最新一次运行。运行成功后，刷新在线页面即可看到更新。

如果通过 PR 修改页面，合并到 `main` 后也会自动部署。

## 手动重新部署

打开 **Actions → Deploy to GitHub Pages → Run workflow**，选择 `main` 分支，再点击 **Run workflow**。

## 使用说明

- `index.html` 是网站首页；本地双击即可预览。
- 这个流程适用于 HTML、CSS、JavaScript 静态页面，无需安装 Node.js 或 Maven。
- 当前仅发布 `index.html`。以后如果添加独立的图片、CSS 或 JavaScript 文件，需要在工作流的 `Prepare static site` 步骤中，将这些资源一并复制到 `_site`，并在网页中使用相对路径引用。
- 如果部署失败，点击 Actions 中标红的步骤查看日志，再根据错误修复配置。

参考：[GitHub Pages 自定义工作流官方文档](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages)。
