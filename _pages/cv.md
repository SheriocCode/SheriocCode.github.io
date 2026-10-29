---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

教育经历
======
* **武汉理工大学**，武汉，中国
  * 专业与学位：待补充
  * 时间：待补充

研究方向
======
* 待补充：例如大语言模型应用、文档理解、机器翻译

项目
======
* **Arxiver**（2025–）
  * 本机离线翻译 + AI 助手的论文阅读桌面应用。
  * [项目主页](/arxiver/) · [源代码](https://github.com/SheriocCode/Arxiver)

技能
======
* 待补充：编程语言、工具、外语等

{% if site.publications.size > 0 %}
论文
======
  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
{% endif %}
