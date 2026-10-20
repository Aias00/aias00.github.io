# Aias 的个人主页

网站：https://aias00.github.io/

源码仓库：https://github.com/Aias00/aias-homepage

发布仓库：https://github.com/Aias00/aias00.github.io

## 更新网站

修改 `index.html`，提交并推送到本仓库的 `main` 分支。
GitHub Actions 会自动将网站文件同步到发布仓库的 `master` 分支，然后由 GitHub Pages 发布。
也可在 Actions → Publish homepage → Run workflow 手动发布。

纯静态页面，无需安装依赖或构建。页面内容和样式都在 `index.html`。
请在源码仓库修改；发布仓库的手动修改会在下次同步时被覆盖。

## CI 配置

`.github/workflows/deploy.yml` 使用 `PAGES_DEPLOY_KEY` Actions secret。
它对应发布仓库中名为 `aias-homepage CI` 的可写 deploy key，只用于该发布仓库。
更换密钥时需同时更新 secret 和 deploy key。

旧博客保留在发布仓库的历史提交 `e6a8efc07afbfbb53da7ce40b76334b0961661f8` 中。
