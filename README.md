# SheriocCode.github.io

个人主页与 Arxiver 项目文档，发布在 GitHub Pages：

- 首页：<https://sherioccode.github.io/>
- Arxiver（概览 + 使用文档 + 参考 + 更新日志，单页）：<https://sherioccode.github.io/arxiver/>

站点基于 Jekyll 与 Academic Pages 主题，外观在 `assets/css/custom.css` 里覆盖：
Inter 字体、明暗主题、细窄滚动条、单页文档版式。

## 目录结构

```text
.
├─ _config.yml              # 站点配置（标题、作者、插件、构建）
├─ _config.local.yml        # 本地预览覆盖（清空 url，避免加载线上资源）
├─ _data/
│  ├─ navigation.yml        # 顶部导航
│  └─ ui-text.yml           # 主题文案（中英文）
├─ _pages/
│  ├─ about.md              # 首页
│  ├─ cv.md                 # 简历
│  ├─ publications.html     # 论文列表
│  ├─ blog.html             # 随笔列表
│  ├─ arxiver.md            # Arxiver 单页文档
│  └─ 404.md
├─ _posts/                  # 随笔文章
├─ _publications/           # 论文条目（每篇一个 md）
├─ _layouts/                # default / single / archive / splash / manual
├─ _includes/               # 页头、导航、页脚、seo 等
├─ _sass/                   # 主题样式源码（编译成 assets/css/main.css）
├─ assets/
│  ├─ css/main.scss         # 主题入口
│  ├─ css/custom.css        # 站点的颜色、明暗、文档版式、滚动条覆盖
│  └─ js/main.min.js        # 线上实际加载的脚本
├─ arxiver/assets/
│  ├─ index/                # 截图（home.jpg、library.jpg 等）
│  └─ videos/               # 演示视频（mp4）
└─ images/                  # 头像、favicon、manifest
```

## 本地环境

需要：

- Ruby 3.x（Windows 需要带 DevKit 的 RubyInstaller）
- Git
- 可选：Bundler、GitHub CLI（`gh`）
- 可选：Node.js —— 只有修改 `assets/js/_main.js` 后重新生成 `assets/js/main.min.js` 时才需要
  （`npm install` 后执行 `npm run build:js`）

## 本地预览

### 方式一：Bundler（推荐）

```powershell
bundle install
bundle exec jekyll serve --config _config.yml,_config.local.yml --livereload
```

打开 <http://127.0.0.1:4000/>；Arxiver 页在 <http://127.0.0.1:4000/arxiver/>。

`bundle install` 会安装 `github-pages` 依赖，第一次比较慢；`Gemfile.lock` 已在 `.gitignore` 中，不需要提交。

### 方式二：全局 Jekyll（Windows 上更快）

```powershell
gem install jekyll jekyll-feed jekyll-sitemap jekyll-redirect-from tzinfo tzinfo-data
$env:JEKYLL_NO_BUNDLER_REQUIRE = "true"
jekyll serve --config _config.yml,_config.local.yml
```

如果报错：

```text
Dependency Error: ... unable to find a version of 'jekyll' to activate
```

说明本机同时装了 `github-pages` 依赖的 Jekyll 3.x 和较新的 4.x。显式指定版本即可：

```powershell
$env:JEKYLL_NO_BUNDLER_REQUIRE = "true"
ruby -e 'gem "jekyll","4.4.1"; gem "jekyll-feed","0.18.0"; gem "jekyll-sitemap","1.4.0"; gem "jekyll-redirect-from","0.17.0"; load Gem.bin_path("jekyll","jekyll","4.4.1")' -- serve --config _config.yml,_config.local.yml
```

版本号按 `gem list jekyll` / `gem list jekyll-feed` 的实际输出调整。

### 为什么需要 `_config.local.yml`

`_config.yml` 里的 `url` 是 `https://sherioccode.github.io`，主题用它拼静态资源地址。
本地预览如果不覆盖，CSS / JS 会从线上加载。`_config.local.yml` 把 `url` 设为空，资源就走本地相对路径。

## 常见修改

| 想改什么 | 改哪里 |
| --- | --- |
| 首页介绍、研究兴趣、联系方式 | `_pages/about.md` |
| 简历 | `_pages/cv.md`（内容来自 `../resume-ng/main.tex`） |
| 顶部导航 | `_data/navigation.yml`（实际链接写死在 `_includes/masthead.html`） |
| 论文列表 | `_pages/publications.html` + `_publications/` |
| 随笔 | `_posts/`，列表页 `_pages/blog.html` |
| Arxiver 文档 | `_pages/arxiver.md` |
| 站点配色、明暗主题、滚动条 | `assets/css/custom.css` |
| 主题变量、布局 | `_sass/` |
| 页头 / 页脚 | `_includes/masthead.html` / `_includes/footer.html` |
| 首屏主题判断（防闪白） | `_includes/head.html` |
| 站点标题、作者、插件 | `_config.yml` |

### 新增论文

在 `_publications/` 新建一个 md：

```markdown
---
title: "论文标题"
collection: publications
category: manuscripts   # books / manuscripts / conferences
permalink: /publication/2026-example
excerpt: "一句话摘要。"
date: 2026-01-01
venue: "期刊或会议"
paperurl: "https://..."
citation: "作者. 标题. 期刊, 2026."
---
```

列表页会自动读取；分类标题在 `_config.yml` 的 `publication_category` 里。

### 新增随笔

在 `_posts/` 新建 `YYYY-MM-DD-slug.md`：

```markdown
---
title: "标题"
date: 2026-11-01
categories:
  - 随笔
tags:
  - 标签
permalink: /blog/slug/
---

正文……
```

### 更新 Arxiver 文档

`_pages/arxiver.md` 是**单页文档**，左侧目录由 front matter 的 `toc` 生成：

```yaml
toc:
  - title: 开始
    items:
      - { title: 下载与安装, id: download }
```

正文里用 `## 标题 {#download}` 定义锚点；新增章节时同时补 `toc`，否则左侧目录点不过去。
更新日志是页面最后一节「更新日志」，发版后直接改这里。

### 图片与视频

- 文件名用 ASCII（避免 URL 编码问题），例如 `library.jpg`、`tagging.mp4`
- 截图建议最长边 1400px，JPEG 质量 82
- 视频建议 H.264、1280 宽、无音轨、`faststart`，单个文件不要超过 100 MB

压缩视频（需要 ffmpeg）：

```powershell
ffmpeg -i input.mp4 -vf "scale=1280:764,setsar=1" `
  -c:v libx264 -preset slow -crf 26 -pix_fmt yuv420p `
  -an -movflags +faststart output.mp4
```

页面里用原生播放器，封面图和尺寸写清楚，避免加载时布局跳动：

```html
<video controls muted loop playsinline preload="metadata"
       width="1280" height="764"
       poster="/arxiver/assets/index/library.jpg">
  <source src="/arxiver/assets/videos/tagging.mp4" type="video/mp4">
</video>
```

## 提交与发布

```powershell
git status
git add -A
git commit -m "feat: ..."
git push origin master
```

GitHub Pages 使用 `master` 根目录构建，推送后 1–2 分钟自动更新。查看构建状态：

```powershell
gh api repos/SheriocCode/SheriocCode.github.io/pages/builds/latest --jq '.status'
```

`queued` / `building` / `built`；失败时加 `--jq '.error'` 看原因。

> 旧的 `/Arxiver/...` 地址由 Arxiver 仓库的 `docs/` 跳转页指向这里；要改跳转目标，去 Arxiver 仓库改 `docs/*.html`。

## 故障排查

- **`No source of timezone data could be found`**：Windows 上 Jekyll 需要时区数据；`Gemfile` 已包含 `tzinfo-data`，重新跑一次 `bundle install` 即可。
- **`unable to find a version of 'jekyll' to activate`**：本机有多个 Jekyll 版本；删掉 `Gemfile.lock` 用 `bundle exec`，或用上面的显式版本命令。
- **本地页面没样式 / 加载的是线上 CSS**：确认带了 `--config _config.yml,_config.local.yml`。
- **Sass deprecation warning**：主题依赖的老语法提示，不影响构建。
- **深色模式切页闪白**：`_includes/head.html` 顶部的内联背景色和主题脚本不要删。
- **`_site/`、`.jekyll-cache/`、`Gemfile.lock`**：已在 `.gitignore`，不要提交。

## 约定

- 正文用中文，专有名词保留英文
- 图片、视频用 ASCII 文件名
- 简历不要放手机号等隐私信息
- 提交信息用 `feat:` / `fix:` / `content:` / `chore:` 前缀
