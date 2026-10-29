---
layout: single
title: "CV"
permalink: /cv/
author_profile: true
---

[邮箱](mailto:sherioc@whut.edu.cn) · [GitHub](https://github.com/SheriocCode) · [Arxiver 项目](https://sherioccode.github.io/arxiver/)

## 教育经历

**武汉理工大学** · 计算机技术 · 计算机与人工智能学院  
硕士研究生（保送） · 2026.09–2029.06  
研究方向：室内场景三维重建

**武汉理工大学** · 人工智能 · 计算机与人工智能学院  
工学学士 · 2022.09–2026.06

## 荣誉与成果

- 国家励志奖学金 1 项、校级奖学金 2 项；校优秀学生干部
- 国家发明专利《一种基于多模态嵌入的三维高斯点云网格构建方法及系统》（第二发明人）
- 软件著作权《智法通鉴——法律服务数智化平台》V1.0（第一作者）
- 省级创新创业训练计划项目《基于 3D Gaussian Splatting 的新型室内场景三维重建系统》（项目负责人）
- 2025 年第十六届中国大学生服务外包创新创业大赛 全国三等奖（主力成员）
- 2025 年第十八届中国大学生计算机设计大赛中南地区赛 省级一等奖（队长）

## 技术栈

- **语言**：TypeScript、Python、C++；熟悉 JavaScript / Node.js；了解 GDScript、VBA
- **大模型应用**：OpenAI 兼容接口、Function Calling / Agent 编排、RAG（文档解析、分块、BM25 检索排序）、Prompt 工程；llama.cpp 本地推理（GGUF 量化、GPU / CPU 回退）、ONNX Runtime
- **AI 工程**：opencode / Codex / Cursor 等 AI 编程工具；阅读 opencode 源码（Agent 循环、工具调用、上下文管理）
- **桌面客户端**：Electron（主 / 渲染进程、IPC、preload）、React 19 + Hooks、PDF.js、electron-builder / electron-updater 差量更新
- **工具链**：Linux、Shell、(Neo)Vim、Git、Docker

## 项目经历

### Arxiver｜科研文献翻译与阅读 Agent（桌面端）

[项目主页](https://sherioccode.github.io/arxiver/) · [源代码](https://github.com/SheriocCode/Arxiver) · 2026.10–至今

独立完成产品定位、UI 设计、架构与开发；已发布 Windows 安装包。

- **RAG 检索**：PyMuPDF 解析 PDF → 800 字 / 120 重叠分块 → 自研 BM25 检索排序 → 证据注入模型；回答绑定页码、可跳转原文。
- **Agent**：Function Calling 工具链覆盖整库检索、正文阅读、联网搜索与文库写操作；多轮 Tool Use + 会话记忆 + 自动路由，写操作先确认（human-in-the-loop）。
- **模型与部署**：OpenAI 兼容 API 接入在线模型；本地 llama.cpp + GGUF 部署 HY-MT 翻译模型，GPU / CPU 自适应，单机约 10 页/分钟、无 API 费用；版面识别（DocLayout-YOLO）DirectML 加速约 10 倍。
- **全栈与工程**：Electron + React 19 + TypeScript，Python 引擎子进程；任务队列、内容寻址缓存、流式增量渲染；工具调用 / Token / 分段耗时全链路日志。

### BusTub｜基于 C++ 的简易单机数据库

CMU 15-445 课程项目

- 基于可扩展哈希表和 LRU-K 的内存池管理；实现可并发 B+ 树，支持乐观锁读写。
- 采用火山模型实现查询、修改、连接、聚合等执行器，并对部分查询做改写与下推。
- 采用 2PL 并发控制，支持死锁处理、多种隔离级别、表锁与行锁。

### Multi-Raft｜分布式 KV 存储系统

MIT 6.824 课程项目

- 实现 Raft 的选举、日志复制、持久化、日志压缩等基本功能。
- 基于 Raft 实现满足线性一致性的 KV 数据库。
- Multi-Raft 架构，支持数据分片、分片迁移、垃圾回收，以及迁移期间的读写优化。

### 科研数据自动化处理流水线

Python 脚本与 VBA 宏开发 · 2025.10–2026.03

- 设计并实现「WPS 表单收集 → Excel 数据清洗 → Word / Visio 批量生成」的自动化流程。
- 基于 python-docx 动态填充实验数据并格式化表格，支持批量导出。
- 使用 VBA 宏实现 Visio 多源图片的自动检索、坐标定位与网格化排版。

## 个人总结

- **大模型应用落地**：从本地模型推理（llama.cpp / ONNX Runtime）、Agent 工具调用与 RAG 检索，到产品级桌面客户端与差量更新的端到端交付。
- **客户端与工程化**：熟悉 Electron + React + TypeScript 的桌面应用架构与安全 IPC，注重性能、可观测性与发布流程。
- **技术基础**：扎实的计算机科学基础（C++ / Linux / 分布式系统），六年 Linux 使用经验，习惯技术写作与持续学习。
