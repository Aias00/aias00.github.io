# Aias 的个人主页

网站：https://aias00.github.io/

源码仓库：https://github.com/Aias00/aias-homepage

发布仓库：https://github.com/Aias00/aias00.github.io

## 技术选型

网站使用 Astro，构建时生成静态 HTML、CSS 和浏览器脚本，发布到 GitHub Pages。首页、电子书架和自我介绍分别独立成页；禁用 JavaScript 仍能在三页之间导航，浏览所有书籍和阅读、下载链接。分类筛选、粒子动画和页脚时间采用原生 JavaScript。

## 本地开发

需要 Node.js 22.22.0 或更新版本；推荐按 `.nvmrc` 切换版本。

```sh
npm ci
npm run dev
```

访问 http://localhost:4321/ 。检查与生产预览：

```sh
npm run check
npm run build
npm run preview
```

浏览器回归检查（首次运行先安装测试浏览器）：

```sh
npx playwright install chromium
npm test
```

生产文件生成到 `dist/`，不提交构建产物。修改源码后需重新构建，不能直接用文件协议打开 Astro 源文件。

## 内容与样式

- `src/data/books.ts`：书目、分类、阅读和 EPUB 入口；书卡编号、总数与分类数量由数据生成。
- `src/pages/`：`index.astro` 为首页，`books.astro` 为电子书架，`about.astro` 为自我介绍与联系页。
- `src/components/`：首屏、关于、书架、书卡、阅读路线、联系和页脚。
- `src/layouts/SiteLayout.astro`：各页面独立的标题、描述与规范链接，全局样式与脚本入口。
- `src/styles/global.css`：深海军蓝背景、冰青主色、靛蓝辅助色，以及排版与移动端布局；粒子球从同一组 CSS 变量读取配色。
- `src/scripts/site.js`：全站时钟与旧首页锚点兼容；导航当前页状态在构建时生成。
- `src/scripts/bookshelf.js`、`src/scripts/orb.js`：分别仅在书架页加载筛选脚本、在首页加载粒子球脚本。
- `public/`：原样复制到构建输出的静态文件。

全站导航为“首页 / 书架 / 关于”。首页 `/` 保留个人首屏与书架入口；`/books/` 承载电子书架与阅读路线；`/about/` 展示自我介绍和联系方式。书架配置共 29 本书，支持“后端与基础设施 / AI 与智能体 / 开源实践”筛选，分别为 16、12、1 本。本轮新增 MySQL 备份恢复、CDC 数据同步、Kubernetes Operator 三本，各为 18 章正文、4 个附录，均已提供在线阅读和 EPUB。完整分类、阅读顺序与维护约定见 [内容规划](CONTENT_PLAN.md)，本轮交付和后续储备见 [写作路线](WRITING_ROADMAP.md)。

旧首页的 `#books`、`#book-*` 链接自动转到书架页，`#about`、`#contact` 转到关于页；书籍和联系锚点保留。此兼容跳转需要 JavaScript，禁用脚本时可通过全站导航访问对应页面。

移动端（820px 及以下）书名使用 20px、简介与阅读入口使用 16px 字号，简介独占整行，阅读和下载按钮提供至少 48px 点击高度。

首屏粒子球会在离开可视区域或切换标签页后暂停；系统开启“减少动态效果”时显示静态图形。页脚时间使用北京时间。字体、图标和图形均由本站提供。

## 发布

提交并推送到本仓库的 `main` 分支后，GitHub Actions 安装依赖、执行类型检查、构建及浏览器回归测试，再将 `dist/` 同步到发布仓库的 `master` 分支，由 GitHub Pages 发布。也可在 Actions → Publish homepage → Run workflow 手动发布。

请在源码仓库修改；发布仓库的手动修改会在下次同步时被覆盖。

`.github/workflows/deploy.yml` 使用 `PAGES_DEPLOY_KEY` Actions secret。它对应发布仓库中名为 `aias-homepage CI` 的可写 deploy key，只用于该发布仓库。更换密钥时需同时更新 secret 和 deploy key。

旧博客保留在发布仓库的历史提交 `e6a8efc07afbfbb53da7ce40b76334b0961661f8` 中。

## 阅读站统一样式

共用样式和主题控件位于 `reader-theme/`。默认浅色，支持低饱和深色；偏好在同域书站间共享。运行 `python3 scripts/sync_reader_theme.py --checkout-root /path/to/book/repos` 将其同步到各书的源码与发布文件，再执行对应站点的构建和检查。样式随站点发布，不依赖外部资源，也不修改 EPUB。详细映射见 [阅读器维护说明](reader-theme/README.md)。
