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

## 本地预览与修改

直接用浏览器打开 `index.html`，或在仓库目录运行：

```sh
python3 -m http.server 4187 --bind 127.0.0.1
```

然后访问 http://127.0.0.1:4187/ 。

页面采用深色背景与青绿色点缀，按“个人首屏 → 电子书架与阅读路线 → 关于与联系”排列。颜色在 `:root` 中统一配置，书目在 `#book-grid` 中修改。所有图形和图标均在页面内绘制，不依赖外部字体、图片或脚本。

电子书架默认展示全部 9 本书，支持“后端与基础设施 / AI 与智能体 / 开源实践”筛选。每本书分别提供在线阅读和 EPUB 下载；禁用 JavaScript 时仍可浏览所有书目及链接。完整分类、阅读顺序与维护约定见源码仓库的 [内容规划](https://github.com/Aias00/aias-homepage/blob/main/CONTENT_PLAN.md)。

首屏粒子球会在离开可视区域或切换标签页后暂停；系统开启“减少动态效果”时显示静态图形。页脚时间使用北京时间。

## CI 配置

`.github/workflows/deploy.yml` 使用 `PAGES_DEPLOY_KEY` Actions secret。
它对应发布仓库中名为 `aias-homepage CI` 的可写 deploy key，只用于该发布仓库。
更换密钥时需同时更新 secret 和 deploy key。

旧博客保留在发布仓库的历史提交 `e6a8efc07afbfbb53da7ce40b76334b0961661f8` 中。
