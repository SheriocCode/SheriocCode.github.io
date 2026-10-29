---
title: "站点合并：Arxiver 官网搬进个人主页"
date: 2026-10-29
permalink: /blog/site-merge/
categories:
  - 随笔
tags:
  - 站点
  - Arxiver
---

之前 Arxiver 有一个单独的官网仓库，每次更新文档都要在两个地方来回改。现在把文档并进了个人站，Arxiver 的内容统一放在 [/arxiver/](/arxiver/)。

这样做的几个好处：

- 只需要维护一个 Jekyll 站点，不用两个仓库同步；
- 文档和代码仍然各自独立，Arxiver 仓库只保留源码和发布产物；
- 顺手把个人主页、CV、项目和博客也搭起来，别人看项目时能顺便了解作者。

旧的 `sherioccode.github.io/Arxiver/` 地址会跳转到新的 `sherioccode.github.io/arxiver/`，之前的链接不会失效。
