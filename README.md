# SheriocCode.github.io

个人主页，基于 [Academic Pages](https://github.com/academicpages/academicpages.github.io)（Jekyll），发布在 GitHub Pages：<https://sherioccode.github.io/>。

## 目录

- `_pages/` — 独立页面：About、CV、Publications、Projects、Blog 归档
- `_posts/` — 博客文章
- `_publications/` — 论文条目（每篇一个 md）
- `_portfolio/` — 项目条目，显示在 `/projects/`
- `arxiver/` — [Arxiver](https://github.com/SheriocCode/Arxiver) 项目专区，独立主题，访问路径 `/arxiver/`
- `_layouts/arxiver/`、`_includes/arxiver/` — Arxiver 专区使用的布局与图标
- `images/` — 站内图片

## 本地预览

```bash
bundle install
bundle exec jekyll serve
```

打开 <http://127.0.0.1:4000/>；Arxiver 专区在 <http://127.0.0.1:4000/arxiver/>。

改完直接提交到 `master`，GitHub Pages 会自动构建。
