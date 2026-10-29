# SheriocCode.github.io

个人主页，发布在 GitHub Pages：<https://sherioccode.github.io/>。

站点不用 Jekyll 的默认主题，而是沿用 [Arxiver](https://github.com/SheriocCode/Arxiver) 官网的设计：
等宽字体、浅色纸面、`[+]` 列表标记，深色只出现在 TUI 展示块里。

## 目录

- `_pages/` — 独立页面
  - `about.md` — 首页（个人介绍、研究兴趣、项目、最近）
  - `cv.md` — 简历
  - `publications.html` — 论文列表
  - `blog.html` — 随笔列表
  - `404.md` — 404
- `_posts/` — 随笔文章
- `_publications/` — 论文条目（每篇一个 md）
- `arxiver/` — Arxiver 项目专区（`/arxiver/`，含概览、文档、参考、更新日志）
- `_layouts/arxiver/` — 全站布局：`default`（页头页脚）、`personal`（个人首页）、`page`（普通页）、`doc`（文档）、`post`（文章）
- `arxiver/assets/` — 设计样式、脚本、图片

## 本地预览

```bash
bundle install
bundle exec jekyll serve
```

打开 <http://127.0.0.1:4000/>；Arxiver 专区在 <http://127.0.0.1:4000/arxiver/>。

改完提交到 `master`，GitHub Pages 会自动构建。旧的 `/Arxiver/...` 地址由 Arxiver 仓库的 `docs/` 跳转页指向这里。
