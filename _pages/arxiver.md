---
layout: manual
title: "Arxiver"
permalink: /arxiver/
author_profile: false
redirect_from:
  - /arxiver/guide.html
  - /arxiver/reference.html
  - /arxiver/changelog.html
toc:
  - title: 开始
    items:
      - { title: 下载与安装, id: download }
      - { title: 安装与启动, id: install }
      - { title: 翻译引擎, id: model }
      - { title: 导入与阅读, id: read }
      - { title: 翻译, id: translate }
  - title: 功能
    items:
      - { title: Arxiver 助手, id: arxiver }
      - { title: 联网搜索, id: websearch }
      - { title: 设置, id: settings }
      - { title: 数据与存储, id: storage }
      - { title: 更新, id: update }
      - { title: 故障排查, id: troubleshoot }
  - title: 参考
    items:
      - { title: 工作原理, id: arch }
      - { title: 组成, id: layout }
      - { title: 数据格式, id: data }
      - { title: 助手实现, id: agent }
      - { title: 联网搜索与读正文, id: ref-websearch }
      - { title: 更新与发布, id: release }
      - { title: 构建, id: build }
      - { title: 第三方许可, id: license }
  - title: 更新日志
    items:
      - { title: 最新版本, id: changelog }
---

# Arxiver

把英文论文，读成中文。导入本地 PDF 或 arXiv 链接，本机翻译引擎离线完成：约 10 页/分钟、边翻边看，论文不出本机；另有能跨文献问答、联网检索的内置 AI 助手。

<div class="rtd-badges">
  <a href="https://github.com/SheriocCode/Arxiver/releases/latest"><img src="https://img.shields.io/github/v/release/SheriocCode/Arxiver?style=flat-square" alt="Release"></a>
  <a href="https://github.com/SheriocCode/Arxiver/releases/latest"><img src="https://img.shields.io/badge/platform-Windows%2010%20%7C%2011-0078D4?style=flat-square" alt="Platform"></a>
  <a href="/arxiver/#model"><img src="https://img.shields.io/badge/translation-100%25%20offline-10a37f?style=flat-square" alt="Offline"></a>
</div>

<figure class="rtd-doc-figure rtd-doc-figure--wide">
  <img src="/arxiver/assets/index/首页.jpg" alt="Arxiver 主界面">
  <figcaption>主界面：文献库、双语阅读与 AI 助手在同一个窗口。</figcaption>
</figure>

## 为什么值得一试

<div class="rtd-feature-grid">
  <div class="rtd-feature-card"><strong>真正离线</strong><p>内置 HY-MT 翻译模型与 llama.cpp 运行时，不需要 API Key，论文不出本机。</p></div>
  <div class="rtd-feature-card"><strong>三视图阅读</strong><p>保留原 PDF 版面，原文 / 对照 / 译文逐页切换，块框可溯源到原文段落。</p></div>
  <div class="rtd-feature-card"><strong>AI 助手</strong><p>跨文献问答、联网检索，引用精确到页码 + 段落，点击直接跳到原文。</p></div>
  <div class="rtd-feature-card"><strong>文献管理</strong><p>分类、标签、笔记、回收站、全文检索；粘贴 arXiv 编号 / DOI / 链接即可导入。</p></div>
  <div class="rtd-feature-card"><strong>Overleaf 工作区</strong><p>内嵌 Overleaf，AI 按需读取项目文件，修改建议确认后才写入。</p></div>
  <div class="rtd-feature-card"><strong>差量更新</strong><p>升级只下载变化的块；引擎与翻译模型没变就不会重下。</p></div>
</div>

## 和 Zotero 比一比

| 能力 | Arxiver | Zotero |
| --- | --- | --- |
| 论文翻译 | 内置本机翻译，离线、0 费用、边翻边看 | 无内置，需第三方插件，多为在线服务 |
| AI 助手 | 跨文献问答、联网检索、读写文献库 | 官方无内置 |
| 文献管理 | 分类、标签、笔记、回收站、全文检索 | 元数据与浏览器抓取更完整 |
| Overleaf | 内嵌工作区，可按需读取与修改 | 无 |

## 下载与安装 {#download}

1. **安装并启动** — 在 [Releases](https://github.com/SheriocCode/Arxiver/releases/latest) 下载 `Arxiver Setup vX.exe`，双击按向导安装。
2. **下载模型** — 首次翻译前到「设置 → 本地模型」下载版面识别模型（约 72 MB，必需）和本地翻译模型（约 1.1 GB，仅本地模式）。使用在线接口时只需版面识别模型。
3. **导入并翻译** — 导入本地 PDF 或 arXiv 链接，打开后点「翻译」，在阅读器里切换 原文 / 对照 / 译文。
4. **配置助手（可选）** — 需要对话式助手时，在「设置 → AI 服务」填入 OpenAI 兼容接口；默认 DeepSeek + `deepseek-flash`。

源码开发：克隆仓库后进入 `electron-app/`，`npm install` → `npm run dev`。

## 使用文档

### 安装与启动 {#install}

1. 在[下载页](https://github.com/SheriocCode/Arxiver/releases/latest)获取 `Arxiver Setup vX.exe`，双击按向导安装（可选择安装目录）。
2. 启动后即为桌面应用，无需浏览器扩展、无需单独启动任何服务。
3. **关闭窗口只是收进托盘**：应用继续在后台运行（翻译任务不中断），窗口会从任务栏消失。想再打开点**托盘图标**（单击即可），或再启动一次 Arxiver（会唤起已有窗口）；要**彻底退出**用托盘菜单里的「退出」。

### 翻译引擎 {#model}

本地翻译所需的运行时与模型**按需下载**：安装包只带 CPU 版推理运行时与依赖，其余在「设置 → 本地模型」下载：

- **版面识别模型**（DocLayout-YOLO，约 72 MB）：识别标题、正文、图表等版式；**本地翻译和在线接口翻译都需要**。
- **本地翻译模型**（HY-MT2 1.8B Q4_K_M，约 1.1 GB）：仅「本地模型」模式需要；如果使用在线接口，可以不下载。
- **GPU 加速包**（Vulkan 版 llama.cpp，约 35 MB）：可选。安装后本地翻译用显卡跑，速度是纯 CPU 的数倍；没有可用显卡或驱动时自动回退随包的 CPU 运行时。
- 每个项目都会列出可用的下载源（模型：HuggingFace / hf-mirror，版面模型还有 ModelScope；加速包：GitHub / gh-proxy / ghproxy.net），可以逐个测速或「全部测速」后选择；不选则按优先级自动回退。校验通过后才启用。
- 模型保存在**安装目录下的 `data\models`**（例如 `E:\develop\Arxiver\data\models`），不是 C 盘 AppData；设置页会显示实际路径并提供「打开目录」。版面识别模型还会复制一份到 `data\home\.cache\babeldoc\models` 供引擎读取，GPU 加速包解压到 `data\runtime\vulkan`。安装目录不可写时会回退到 `%APPDATA%\Arxiver`。删除文献不会删除模型。
untimeulkan`。安装目录不可写时会回退到 `%APPDATA%\Arxiver`。删除文献不会删除模型。

本地翻译在本机离线运行，无需 API Key；装了 GPU 加速包走显卡，否则用 CPU。

> 本地翻译与版面识别均在本机完成，数据不出本机；仅在线接口与 Arxiver 助手会访问你配置的服务。

### 导入与阅读 {#read}

- 「新建文献」可导入本地 PDF，或粘贴 arXiv 链接/编号自动下载。
- 文库支持分类、标签、星标、回收站、阅读历史与全文检索（标签页 / 年份 / 状态等）。
- 双击条目打开阅读器（**默认原文 + 单页**）：工具栏可切换 **原文 / 对照 / 译文** 与 单页 / 双页，并支持缩放、目录大纲、缩略图与页面主题（护眼 / 米黄 / 暗色）。
- 工具栏右端的**块框**按钮（层叠图标）可直接在阅读界面显示 / 隐藏段落块框，没有译文时不可用；点击块框会钉住它，查看对应的**译文**（**原文默认折叠**，点「原文」展开对照）。
  面板**按住标题栏可拖动**，拖过之后就不再跟随块框、停在原处；再次点击同一块框、点空白处或关闭按钮收起。
  译文里保留的公式 / 格式占位符（`{v0}`、`{{v0}}`）会单独渲染成**琥珀色小标签**：引擎能抽出公式内容时标签直接显示公式本身（如实线框），抽不出来（部分数学字体没有 Unicode 映射）才显示 `{vN}`（虚线框）。
  这份公式文本是翻译时随块框数据一起缓存的，**旧译文需要重新翻译一次**才会显示。
- **标注**：选中正文文字会浮出工具条——先点色块选颜色，再点高亮 / 下划线 / 删除线 / 笔记。
  点击页面上的标注打开一个紧凑面板：顶部直接改颜色，笔记框直接写、自动保存，点链接 / 图片图标可以添加；笔记里可以写文字、插入或粘贴图片、添加链接（点链接条目跳转），图片和链接都属于笔记内容，不会单独浮在页面上。
  没填内容的笔记关闭后不会留下标记。左侧面板的「标注」页会在每条下方直接显示笔记内容 / 原文摘要，方便快速查找；点击只定位（不弹面板），也可集中删除。标注保存在本机（不改原 PDF），缩放、双页与对照视图下位置不变。

### 翻译 {#translate}

- 在阅读器工具栏点「翻译」（有译文时为「已翻译」）→ 右侧下拉可设 源语言 / 目标语言 / 导出格式（双语对照 / 仅译文）/ 页数，也可「重新翻译」。
- 「已翻译」的下拉会列出该文献的多个译文版本，可切换；同一菜单里的「导出译文文件…」把当前译文另存为 PDF。
- 翻译过程中顶部显示进度（已完成页数 / 当前页块进度）；可取消。翻译在后台继续，切换标签页不会打断，关闭该文档的标签页才会取消。
- 相同 PDF 与参数再次翻译会命中本地缓存。

### Arxiver 助手 {#arxiver}

右侧「Arxiver」标签是基于文库（可选联网）的对话式助手：

- **自动路由**：默认针对当前文章；涉及其它文献或整库问题时自动检索，必要时会向你追问。
- **引用跳转**：引用文库内容时给出 `第 N 页` 胶囊，点击跳转到原文。
- **`@` 引用**：在输入框输入 `@` 选择其它已打开文献作为额外上下文（跨文献对比）。
- **选中文本提问**：在 PDF 里选中文字 → 点「问 Arxiver」。
- **截图 / 图片提问**：在 PDF 的**图 / 空白**处拖框选区（文字上仍是正常选词，按住 `Alt` 可在文字上强制框选）。松开后选区保留（不压暗页面），选框外侧出现小操作条：点 **Arxiver 图标**把选区加进对话，点 **×** 取消；也可以拖 8 个手柄改大小、拖框内移动，点菜单外或按 `Esc` 取消。**不会离开 PDF**（底部提示「已添加到对话」）。
  也可以在对话框里直接 **Ctrl+V 粘贴图片**，或点输入框左侧的图片按钮选文件。
  图片发送前会压缩到最长边 1600px 的 JPEG，随会话存在本机；**截图还会带上页码、页面纵向位置和选区内的文字**一起发给模型（图里的小字/公式认不准时，模型可以靠这些定位）。对话模型需要**支持视觉输入**（如 DeepSeek 的 `deepseek-flash`，`deepseek-chat` 不行）；选了不支持的模型时，输入框上方会立刻提示并给出「去设置」。
  一次框选只取鼠标所在的那一页，跨页区域请分两次截。
- **技能**：把重复使用的提示词 / 工作流程存成技能——点 AI 面板右上角的 ✦ 按钮，可新建、编辑、删除，或点「让 AI 帮我写」由助手先问清需求再保存。启用的技能会以标签显示在输入框上方（再点一次取消），可以单独发送，也可以和具体问题一起发；技能保存在本机，跨文档、跨会话可用。
- **写操作需确认**：改元数据 / 标签 / 星标 / 回收站 / 分类、导入论文、增删笔记、保存 / 删除技能等，都会先弹出确认卡片（批准 / 修改 / 拒绝）。
- **长任务有反馈**：搜索、读正文、导入下载会显示「正在执行 …」、当前阶段与已用时间；回答按到达顺序显示，中间的过程结果可折叠。
- 会话自动保存；右上角可查看历史（含关联论文，可搜索）。切换详情标签页不会丢会话。

### 联网搜索 {#websearch}

在「设置 → AI 助手 → 联网搜索」里开启（**默认关闭**），并填**当前服务商**的 API Key：

| 服务商 | 特点 | 申请地址 |
| --- | --- | --- |
| **Tavily** | 英文 / 学术结果更干净，支持学术域名加权；读正文（extract）优先用它，按 credits 计费 | [tavily.com](https://tavily.com) |
| **博查（Bocha）** | 国内网络友好、响应快，中文网页结果好；学术场景噪声略多，不显示 credits | [open.bochaai.com](https://open.bochaai.com) |
| **DeepSeek** | 自研搜索引擎，国内直连；返回 600~800 字长摘要与权威性排序，支持 `site:` / `after:` 等语法；按请求计费（¥5 / 1000 次，无结果不计费） | [platform.deepseek.com](https://platform.deepseek.com/) |

- **检索范围**：学术优先（对 arXiv / 会议 / 期刊等域名加权，不排他）或 全网。
- 各家的 Key 分开保存在本机，**切换服务商不用重填**；DeepSeek 的 Key 可以与「对话接口」用同一把。
- DeepSeek 搜索限 **账号级 5 QPS**、单条检索式 **128 字符**，应用内已做串行化与截断，正常使用不会触发限速。
- 开启后助手可以：
  - **搜索**：结果以卡片列出（标题 / 站点 / 年份 / 摘要片段 / 链接）。有 arXiv 编号或 DOI 的条目可点卡片上的「导入到文库」入库，其它只能「打开链接」；
  - **读正文**：在给结论之前把最相关的网页 / PDF 读进来（通常每轮挑 2~3 篇），用正文里的方法和数字作答，而不是凭搜索片段猜；
  - **引用**：回答里指代卡片时显示灰色的 `卡片 N` 胶囊，点击会滚动到那张卡片并高亮。
- 「已读正文」行显示读了哪个站点、多少字；悬停可看读取途径（Tavily extract / DeepSeek Fetch / 直接抓取）与完整链接，点 ↗ 用浏览器打开。
- **隐私**：只把检索式发给搜索服务商，不上传本地文献内容；读正文时只发送要读的网址。
- 检索与读取记录会写进运行日志（左侧栏「日志 → 系统运行日志」里搜 `websearch`，或看 `%APPDATA%\Arxiver\logs\app.log`）。
- 联网结果不在本地文库，所以助手给的是链接而不是页码引用。

### 设置 {#settings}

「设置」包含：翻译引擎（本地 / 在线）、通用、外观（主题 / 字号）、引用、AI 助手（对话接口 + 联网搜索）、同步与存储、快捷键、关于（版本与检查更新）。

### 数据与存储 {#storage}

本机数据位于**安装目录下的 `data\`**（例如 `E:\develop\Arxiver\data\`；`npm run dev` 为 `electron-app\data\`）。升级 / 卸载会保留 `data\`；安装目录不可写时会回退到 `%APPDATA%\Arxiver\`。

> 从旧版本升级：新版首次启动会自动把旧 `%APPDATA%\Arxiver\`（开发版 `%APPDATA%\Arxiver-dev\`）里的 `config.json`、`ui-settings.json`、`skills.json`、`background/`、`storage/`、`models/` 补到新版 `data\`（只补缺失；已有文库时不会合并）。Chromium 缓存不复制；确认新版 `data` 正常后，旧 `%APPDATA%` 里的 `config.json` / `skills.json` / `background/` / `storage/` 等可以删除（保留 Chromium 缓存目录即可）。旧的 `~/.cache/babeldoc` 也可以删除，新版使用 `data\home\.cacheabeldoc`。


~~~
data/
  config.json                # 设置（含 API Key，注意保管）
  ui-settings.json           # 外观 / 启动设置
  storage/
    index.json               # 文库元数据（条目 / 分类 / 标签 / 历史）
    <docId>/                 # 每个条目一个文件夹
      paper.pdf              # 原始 PDF
      <cacheKey>.dual.pdf    # 双语译文
      <cacheKey>.mono.pdf    # 仅译文
      <cacheKey>.blocks.jsonl# 块框数据
      text.json              # 全文检索用文本
    conversations/           # Arxiver 会话
  models/                    # 按需下载的翻译 / 版面模型
  runtime/vulkan/            # 按需下载的 GPU 加速包（Vulkan 版 llama.cpp）
  home/.cache/babeldoc/      # 引擎字体、版面模型、tiktoken 缓存
  skills.json                # AI 技能（可复用的提示词 / 工作流程）
  logs/app.log               # 运行日志（检索 / 读取 / 错误）
~~~

Chromium 的渲染缓存 / LocalStorage / Cookies 仍在 `%APPDATA%\Arxiver\`（开发版 `%APPDATA%\Arxiver-dev\`），不放进安装目录。

### 更新 {#update}

应用内置自动更新（`electron-updater`）：启动时自动检查，也可在「设置 → 关于 → 检查更新」。更新只下载变化的块，未变的大文件（如引擎）不会重复下载；下载完成后点「重启并安装」。

### 故障排查 {#troubleshoot}

- **翻译失败 / 提示缺少模型**：到「设置 → 本地模型」下载版面识别模型（任何翻译都需要，约 72 MB）和本地翻译模型（本地模式需要，约 1.1 GB）；阅读器报错里也带「去下载模型」入口。也可切换到在线接口（仍需版面识别模型）并填写地址 / 密钥 / 模型。
- **首次翻译较慢**：首次会加载本地模型并缓存字体 / 版面模型（约数秒）；如果模型还没下载，需要先完成一次下载。
- **翻译引擎**：本地模式下翻译时才会启动 Python 引擎（`python.exe`），任务结束就退出；**本地模型服务（`llama-server.exe`）首次翻译后常驻**，所以后续翻译主要是每页的版面分析 + 翻译 + PDF 写回，另有每次任务约 2 秒的引擎启动固定开销。每次翻译的分段耗时（引擎就绪 / 版面模型加载 / 版面分析 / 全流程）会自动记进「日志 → 系统运行日志」，也可在「设置 → 运行状态」看到引擎进程与任务。
- **源文件缺失**：条目对应的 `storage/<docId>/paper.pdf` 丢失时无法打开，需重新导入。
- **助手无响应**：确认「设置 → AI 助手」的接口地址 / 密钥 / 模型正确、网络可达，且已在「AI 助手」中启用。
- **联网搜索不生效**：确认已在「设置 → AI 助手 → 联网搜索」打开开关，并且填的是**当前服务商**的 Key（切到博查就填博查的 Key，切到 DeepSeek 就填 DeepSeek 的 Key）；各家的 Key 都留空时搜索不可用，「读正文」也只剩本机抓取。
- **搜索报错**：Key 无效 / 额度用尽 / 请求过于频繁会直接在回答里说明；可以换服务商或换检索式再试。
- **读正文失败**：需要登录或纯前端渲染的页面可能读不到，助手会说明；给它 PDF 直链（如 `arxiv.org/pdf/…`）通常可行。
- **任务管理器里的数字和「运行状态」面板不一样 / 那几个 “Arxiver” 分别是什么**：两件事一起说。① Windows 任务管理器只按 exe 的「描述」显示进程名，Chromium 的渲染 / GPU / 网络等子进程在它那里全都叫 `Arxiver`（只有 Chrome / Edge 这类被系统特殊识别的浏览器才显示「GPU 进程 / 工具进程」），用面板里的 **PID** 就能逐行对上。② **数字不一样是因为列的"口径"不同**：任务管理器「进程」页默认那列是「**活动的专用工作集**」，Chromium 不提供这个数；面板给的 **工作集 / 提交大小** 分别对应任务管理器「**详细信息**」里可添加的「**工作集(内存)**」「**提交大小**」两列（已逐进程核对一致）。所以要看数字，请在任务管理器切到「详细信息」→ 右键表头 → **选择列**，勾上这两列（顺便勾「命令行」还能看到 `--type=…`）。应用内 **「设置 → 运行状态」** 另有整体内存 / CPU 趋势、「暂停」采样和**「导出诊断报告」**（进程快照 + 环境信息 + 最近日志，方便发给开发者排查）。面板底部 **「翻译引擎与任务」** 单独列出主进程的子进程（Python 引擎 `python.exe`、本地模型服务 `llama-server.exe`：PID、内存、端口、正在翻的文件）与任务进度——这些不在 Electron 的进程表里，任务管理器里也是**另一个进程名**，所以不列在上面。另外注意：**多开文献标签或同时翻多篇不会新增进程**，所有文书都渲染在同一个界面进程里，翻译任务则是排队跑同一个 Python 引擎。

## 参考

### 工作原理 {#arch}

Electron 桌面应用：渲染进程（React）负责界面与 PDF.js 渲染，主进程负责文库/存储，并调用内嵌的本地翻译引擎（Python，内置离线翻译模型）与独立配置的在线接口（Arxiver 助手）。

~~~
导入 PDF ─▶ 文库 storage/<docId>/paper.pdf
打开 ─▶ 渲染进程用 PDF.js 渲染原文 / 译文（对照）
点翻译 ─▶ 主进程调用内嵌引擎（engine/）─▶ 内置本地翻译模型（离线；也可切换在线接口）
        └▶ 生成 dual/mono PDF + blocks.jsonl，落盘到 storage/<docId>/
Arxiver ─▶ 主进程检索 storage/*/text.json（BM25）；联网时再走搜索服务商（Tavily / 博查 / DeepSeek）+ 读正文
        └▶ 调用（独立配置的）在线接口流式作答（function calling；写操作先请用户批准）
~~~

### 组成 {#layout}

| 目录 | 说明 |
| --- | --- |
| `electron-app/src/main/` | 主进程：引擎调度、本地翻译服务（`localmodel`）、文库/存储、Agent（模型 + 工具 + 审批）、自动更新 |
| `electron-app/src/renderer/src/` | 渲染进程：React 组件、`styles.css`、PDF 阅读器引擎、Arxiver 面板 |
| `electron-app/src/preload/`、`src/shared/` | `window.api`（IPC）与共享类型 |
| `electron-app/engine/` | 本机翻译引擎（Python）：源码进 git；CPU 版 llama.cpp 与 python 运行时随安装包分发；GPU 加速包、HY-MT gguf 与版面识别 ONNX 按需下载 |
| `icons/`、`site/`→`docs/` | 品牌资源与文档站 |

### 数据格式 {#data}

数据都在**安装目录下的 `data\`**（例如 `E:\develop\Arxiver\data\`）：`storage/index.json`（文库元数据）、
`storage/<docId>/`（`paper.pdf`、`<cacheKey>.dual.pdf`、`<cacheKey>.mono.pdf`、`<cacheKey>.blocks.jsonl`、
`text.json`）、`storage/conversations/`（Arxiver 会话）、`config.json`（设置，含联网搜索的服务商与 API Key）、
`models/`（按需下载的模型）、`runtime/vulkan/`（GPU 加速包）、`home/.cache/babeldoc/`（引擎缓存）、`logs/app.log`（运行日志）。
Chromium 缓存 / LocalStorage / Cookies 仍在 `%APPDATA%\Arxiver\`（开发版 `Arxiver-dev`）；安装目录不可写时应用数据回退到该目录。详见[文档](../guide.html#storage)。

`<cacheKey>.blocks.jsonl` 每行是一个段落块（`page / index / bbox / src / dst`）。片段里出现公式占位符时还带
`vars`：页内编号 → 引擎从 PDF 字形抽出的公式文本（`{vN}` 与 `{{vN}}` 都认）；数学字体没有 Unicode 映射、抽不出内容时该键缺省，界面退回显示占位符。

### Arxiver 助手 {#agent}

- **模型**：OpenAI 兼容 `chat/completions`（流式、function calling、usage），读取 `config.json` 中的 `chat_*` 配置（与翻译接口分离）；一轮提问最多 8 次工具往返（`MAX_ROUNDS`）。
- **只读工具**：`list_library`（含分类 / 标签）、`list_collections`、`search_library`（整库 BM25）、`search_in_document`、`read_document`（按页读 `text.json`）。
- **写入工具**：`update_metadata`、`apply_tags`、`set_flags`、`move_to_trash`、`restore_from_trash`、`add_to_collection`、`remove_from_collection`、`rename_collection`、`delete_collection`、`import_paper`、`add_note`、`delete_note` —— 一律先弹确认卡片（批准 / 修改 / 拒绝）。分类名 / 标签名对不上时，工具返回相近候选让模型自己纠正，而不是让用户去核对拼写。
- **联网工具**：`search_web`、`fetch_url`（见下一节）。
- **图片输入**：`AgentChatRequest.images`（`dataUrl` + `page` + `anchor` + `text`）拼成 OpenAI 兼容内容块（`[{type:"text"},{type:"image_url"}]`），历史消息里的图片随 `history[].images` 一起回传（只有 user 消息允许带图）。阅读器里的区域截图是**自动进入**的：`root` 上的 `pointerdown` 先用 `elementsFromPoint` 找到所在页，再用 `textLines()` 按行判断落点是否在文字行内（仅 2px 容差）——在文字上就完全交给浏览器原生选区（不做任何锚点/终点干预），否则（图 / 空白，或按住 `Alt`）开始拖框；移动超过 4px 才创建遮罩（单纯点击不会闪），松开后选区保留、选框外侧出现小操作条（Arxiver 图标 = 添加到对话，× = 取消），可拖 8 个手柄缩放 / 拖框内移动 / 点空白或 `Esc` 取消，点图标才裁剪入队（页面不压暗）。裁剪时 `cropRegion()` 同时算 `anchor`（选区顶部在页面里的纵向比例）和 `regionText()`（与选区相交的文本层 span；几乎没字时补上相交段落的译文），一起写进提示词，供模型定位。粘贴/选文件走 `lib/images.ts` 统一压到最长边 1600px。`runChat()` 对 `api.deepseek.com` + `deepseek-chat/reasoner/coder` 直接拦截图片请求（这些模型会静默忽略图片），前端也会在输入框上方提前提示。
- **智能路由**：当前文章为默认上下文，跨文献 / 整库问题自动检索；信息不足时追问。
- **检索卡片**：`search_web` 的结果带会话全局编号（`cardBase` + 序号 = `idx`），推给界面渲染成卡片；历史消息里每张卡片压成一行摘要（`#N 标题（site · year）`），模型用 `[[card:N]]` 指代，界面渲染为可点击胶囊（滚动到对应卡片并高亮）；本地文献用 `[[cite:<docId>#<page>]]`。
- **进度事件**：长耗时工具（`import_paper` / `fetch_url`）通过 `progress` 回调上报阶段，界面显示转圈 + 阶段 + 已用秒数。

### 联网搜索与读正文 {#ref-websearch}

相关配置（`config.json`）：`search_enabled`（总开关，默认 `false`）、`search_provider`（`tavily` | `bocha` | `deepseek`）、
`search_key_tavily` / `search_key_bocha` / `search_key_deepseek`（各家 Key 分别保存）、`search_scope`（`academic` | `web`）。
开关关闭时联网工具不暴露给模型；`search_web` 需要**当前服务商**有 Key，`fetch_url` 只要有开关（没 Key 就用本机抓取）。
每次请求都会把联网状态（未开启 / 已开启但当前服务商缺 Key / 可用）写进上下文（`webSearchState()`），
避免模型把「缺 Key」说成「没开启」，或在不可用时编造外部资料。
不再调用 arXiv / OpenAlex 的检索接口（曾受 IP 限流）。

#### 聚合搜索（`search_web` → `searchWeb()`）

- **查询扇出**：模型给出 1~4 条**英文**受控检索式（可带会议名 / 年份 / `site:` 限定），并行请求（DeepSeek 并发限 2），去重后统一排序。
- **归一化**：各家结果都收敛成 `RawHit{title,url,content,date,site}`，之后共用清洗：
  - 标题剥掉 arXiv 的 `[2509.15459]` 前缀；博查另外剥站点后缀（`… – arxiv` / `… | researchgate`）；
  - 摘要优先从 `Abstract:` 之后截取——arXiv 摘要页常混入 arXivLabs / Announce Type / Subjects / Cite as 等样板，抽不到就留空，不显示噪声；
  - arXiv 编号先看 URL、取不到再从正文里找（`arXiv:…` 写法）；DOI **只从 URL 里识别**（防从摘要里误抓别人的 DOI）。两者决定条目能否一键导入；
  - 去重键：DOI → arXiv 编号 → 归一化 URL（去 `utm_*` / 锚点 / `www`）。
- **排序**：`tier = 学术域名(1) + 带标识符(1)`，同 tier 按年份降序。学术白名单含 arXiv / ar5iv / OpenReview / NeurIPS / CVF / ECVA / PMLR / ACL / AAAI / IJCAI / ACM / IEEE / Springer / ScienceDirect / Nature / Science / PubMed / bioRxiv 等。
- **Tavily**：`POST /search`，`search_depth=basic`、`include_usage`、`include_published_date`；学术时带 `include_domains` + `include_domains_mode`（`prefer` 加权 / `restrict` 限定），`time_range` 透传；用量取 `usage.credits`。
- **博查**：`POST /v1/web-search`，`summary=true`（长摘要比 `snippet` 完整）、`count`、`freshness`（`day/week/month/year` → `oneDay/oneWeek/oneMonth/oneYear`）；字段映射 `name→title`、`summary || snippet→content`、`datePublished || dateLastCrawled→date`。它**没有域名参数、没有 extract、也不返回 credits**，所以 `academic + restrict` 由本地白名单兜底（`prefer` 本来就只是排序加权）。
- **DeepSeek**：`POST https://api.deepseek.com/v1/tools/search`（Bearer 用 DeepSeek Key），`count`、`need_content=false`；字段映射 `summary || snippet→content`、`date→date`、`site_name→site`（本地认不出域名时用作 venue）。检索式按 **128 字符**预算截断（超长直接 400），时间范围转成 `after:YYYY-MM-DD`（比 day/week/month/year 更细）。它同样没有域名参数（`site:` 是 query 语法，26 个学术域名拼不进 128 字符），`academic + restrict` 也走本地白名单；**账号级 5 QPS**，所以四条查询限并发 2，408/429/5xx 等 800ms 重试一次；按请求计费（¥5 / 1000 次，无结果不计费），日志里记「N 次请求」而不是 credits。
- **失败处理**：401/403 → Key 无效、402 → 余额不足、432/433 → 额度用尽、429 → 频繁；所有查询都失败且无结果时抛出错误交给模型，让它如实说明，而不是编造论文。

#### 读正文（`fetch_url` → `readPage()`）

预算默认 8000 字（`max_chars` 限 2000~20000），三条路径：

1. **Tavily extract**（配了 Tavily Key 时优先）：`POST /extract`，带上 `query` 让服务端挑相关段落（`chunks_per_source=4`），1 credit / 5 个 URL，超时 25s；返回文本只做长度收敛。
2. **DeepSeek Fetch**（配了 DeepSeek Key 且上一步没取到）：`POST https://api.deepseek.com/v1/tools/fetch`，直接返回 Markdown 正文（`title` + `content`），超时 30s；先走一次内网地址校验（不把 `localhost` / 内网 URL 发给服务商），取回的正文同样用 `pickPassages()` 按 query 挑段。它有域名级 QPS 且对无正文的页面返回 404，所以只作兜底。
3. **本机抓取**（没配 Key 或上面都失败）：`fetchPageText()`
   - 只允许 `http` / `https`；拒绝 `localhost`、`*.local` / `*.internal`、IPv4 私网（`10.` / `127.` / `192.168.` / `172.16-31.` / `169.254.` / `0.` / CGNAT）与 IPv6 私网，**DNS 解析后再校验一次**（防内网域名与 DNS 重绑定）；
   - 手动跟随跳转、最多 4 跳、**每一跳重新校验**；单跳 20s 超时；响应体最大 3MB；
   - `application/pdf` → 落临时文件后调 `engine/extract_text.py`（PyMuPDF）逐页抽文本；HTML → 去 `script/style` / 标签、还原实体、取 `<title>`；其它按纯文本；
   - 再本地挑段落 `pickPassages()`：按空行切段（>40 字），用 `agent/text.ts` 的 `tokenize` 算与 query 的词重合度打分、轻微偏好靠前段落，拼到预算为止，段间用 `---`。

读到的内容一方面以 `read` 事件推给界面（「已读正文」行：站点 · 字数，悬停看途径与完整链接），另一方面作为工具结果回给模型。主进程日志（`websearch:` 前缀）记录每条检索式命中数、`<服务商> 合计 N 条，用量 X credits / N 次请求，耗时 Yms`、`读取 <域名>（<途径>，N 字，Yms）`。

> Key 以明文存于 `config.json`（仅本机、不进 git）；对外只发检索式与要读的 URL，本地文献内容不外发。

#### 导入

`import_paper` 与「新建文献」共用 `importPaper.ts`：接受 arXiv 编号 / DOI / arXiv abs 页 / PDF 直链，页面里会找 `citation_pdf_url`；下载后经 `engine/pdfmeta.py` 与 `enrich.ts` 补全标题 / 作者 / 年份 / 期刊 / DOI 再落库，全程通过 `progress` 回调报阶段（查询元信息 → 下载 PDF → 补全元数据）。

### 更新与发布 {#release}

- 本地打包：`powershell -File tools/build.ps1`（`electron-builder` NSIS，产出安装包、`.exe.blockmap`、`latest.yml` 于 `electron-app/dist/`）。
- 发布：`powershell -File tools/publish.ps1 -Version X.Y.Z`（提交版本、打 tag 并上传到 GitHub Release）。
- 更新：`electron-updater` 读取 `latest.yml`，差量下载（只下变化块）；引擎文件未变不会重下。
- 引擎版本记于 `electron-app/engine/VERSION`；引擎有实质更新时 bump 并在 changelog 注明。

### 构建 {#build}

~~~powershell
cd electron-app
npm install
npm run dev        # 开发运行
npm run typecheck  # tsc（node + web）
npm run build      # electron-vite 构建
npm run dist       # 打包安装包（electron-builder）
~~~

仓库根 `tools/`：`build.ps1`（本地打包）、`publish.ps1`（发布，先打包）、`build-docs.ps1`（文档站 `site/` → `docs/`）、`fetch-llm.ps1`（装配 CPU / Vulkan 运行时与 HY-MT 模型）。

### 第三方许可 {#license}

- **PDF.js**（Mozilla，Apache-2.0）：PDF 渲染与文本层。
- **HY-MT**（腾讯混元，Apache-2.0）：本地翻译模型，在应用内按需下载。
- **llama.cpp**（MIT）：本地翻译推理运行时。
- **ONNX Runtime**（MIT，含 DirectML 执行后端）：版面识别。
- **BabelDOC / PyMuPDF**（AGPL-3.0）：随引擎分发的翻译引擎与文本抽取。
- **KaTeX**（MIT）、**react-markdown / remark / rehype**（MIT）：Arxiver 回答渲染。
- 图标集移植自 **Lucide**（ISC）。

## 更新日志 {#changelog}

全部版本见 [GitHub Releases](https://github.com/SheriocCode/Arxiver/releases)。

### v0.16.0（2026-10-29）

- **Overleaf 工作区**：新增 Overleaf 侧栏，内嵌登录与项目页面，支持持久登录、地址栏、前进后退和项目导航；打开文本文件会自动加入上下文，也可一次提取项目里的 `.tex / .bib / .md / .txt`。
- **按需读取与修改**：AI 可以先列文件、再读取需要的文件；修改以 REPLACE / INSERT / CREATE_FILE 建议呈现，只有点「应用」才写入，并支持拒绝、定位和撤销。未配置或已删除的文件不会再被静默改写。
- **登录保护**：嵌入式窗口只支持邮箱密码登录；点击 Google / ORCID / IEEE / SSO 会直接提示原因，并引导到浏览器设置 Overleaf 密码，不再跳到第三方页面。
- **AI 服务设置重做**：连接与用途分离，模型归属连接、只需填一次；默认 DeepSeek + `deepseek-flash`，支持多连接、测试连接和按用途选择。翻译在线接口也使用同一套连接。
- **本地模型更可靠**：版面识别模型只保留 babeldoc 缓存中的一份；本地模型页自动刷新安装状态，每个模型可单独打开目录；翻译前会校验模型和 API 配置，缺失时立即报错，不再空转。
- **设置体验**：保存按钮固定在弹窗底部，实时显示「有未保存的修改」，关闭前会确认；移除开屏动画、AI 助手开关和检索范围，引用设置合并进通用。
- **其他修复**：右键菜单自动收进窗口内；Overleaf 空状态更简洁；未完成配置的翻译任务会被拦截并给出明确提示。

### v0.15.0（2026-10-26）

- **日志中心重做**：左侧「日志」改为整页视图（隐藏侧栏），翻译 / AI 对话 / 系统运行三类统一成「概览 + 时间线 + 详情」；
  系统运行日志改为读取 `data/logs/app.log` 的跨启动历史，按级别过滤后分页（默认 200 条/页，可继续加载更早的记录），
  概览与近 7 天趋势仍按全量统计。
- **分类与标签合并为「归类」**：右侧详情面板在同一个页签里管理分类和标签——点击 chip 加入 / 移出、已归入的高亮显示，
  也能直接新建分类并归入本文；文献右键新增「移出分类」「移出全部分类」。
- **新建文献更直接**：去掉已不再使用的手动录入表单，只保留按 arXiv / DOI 链接导入和本机 PDF 导入。
- **技能编辑更宽松**：新建 / 编辑技能改为独立大弹窗，提示词区可舒展查看和书写；同名技能在保存前用醒目提示说明，
  新建时按钮变为「覆盖保存」，编辑时改成已有名称会被拦下。
- **细节**：文献拖到分类时的拖影改为小标题卡片，不再拖出整行；侧栏搜索改用自绘清除按钮（按 Esc 清空）；
  修复「?」帮助浮层把弹窗撑出空白滚动区的问题。

### v0.14.0（2026-10-26）

- **详情面板可拖拽调宽**：拖动右侧面板左缘即可在 300–720px 之间调整宽度（信息 / 笔记 / 标签 / Arxiver 共用），
  双击恢复默认 372px；宽度会记入设置，重启后保留，窗口变窄时自动收窄给列表留出空间。
- **Arxiver 空状态精简**：去掉重复的品牌图标与整段说明，标题旁的信息图标悬浮显示工作方式；当前文档改为小字单独展示。
- **修复多页画笔清除错页**：连续滚动时按视口里露出面积最大的页判断「本页」，不会再出现笔迹在眼前却提示「本页没有画笔」。

### v0.13.0（2026-10-26）

- **安装包再瘦身：CUDA 运行库移出安装包**：安装包只带 CPU 版 llama.cpp（约 44 MB）；本地翻译的显卡加速改为按需下载
  「GPU 加速包」（Vulkan 版 llama.cpp，约 35 MB，解压到 `data\runtime\vulkan`）。同一台 RTX 3060 笔记本上实测
  Vulkan 141 tok/s、CUDA 124 tok/s、纯 CPU 24 tok/s，所以不再分发 1.1 GB 的 CUDA 运行库；没有可用显卡或驱动时
  自动回退随包的 CPU 运行时。
- **设置 → 本地模型**新增 GPU 加速包条目（下载源 GitHub / gh-proxy / ghproxy.net，支持测速与删除）；
  「翻译引擎」里的 GPU 层数说明会提示是否已安装加速包。

### v0.12.0（2026-10-26）

- **数据目录改到安装目录**：文库、翻译、设置、日志、模型放在 `<安装目录>\data\`，不再占用 C 盘；
  Chromium 缓存 / LocalStorage 仍留在 `%APPDATA%\Arxiver`（开发版 `Arxiver-dev`）。安装目录不可写时
  应用数据回退到用户目录；升级 / 卸载时保留 `data\`。旧版 `%APPDATA%` 里的配置、技能、背景、文库和模型会在首次启动时自动补到 `data`。

- **模型改为按需下载，安装包更小**：安装包不再内置本地翻译模型（HY-MT2 GGUF，约 1.1 GB）和版面识别模型
  （DocLayout-YOLO ONNX，约 72 MB），新增「设置 → 本地模型」：
  版面识别模型是任何翻译（本地 / 在线接口）都需要的，约 72 MB；本地翻译模型只在「本地模型」模式需要。
  下载优先 HuggingFace，失败自动尝试镜像站，校验通过后启用；翻译报错里也提供「去下载模型」入口。
  设置页会列出每个模型的下载源，支持逐个/全部测速并选择，也会保存选择。
- **引擎 0.3.4**：不再从引擎 assets 恢复版面模型，统一读取应用下载到 `data/models` 的模型。
- **缩略图 / 目录持久化**：缩略图按页缓存为 JPEG，目录缓存带页内位置的 JSON；第二次打开不再重新解析 PDF。
- **渲染体验修复**：缩略图只渲染可视区域、页面链接按需解析；撤销了会导致 Chromium tile memory 超限的整本预渲染，
  看过的页面保留到关闭标签，避免空白和跳页卡顿。

### v0.11.0（2026-10-19）

- **AI 引用精确到段落**：检索 / 阅读工具输出 `[[cite:文献id#页码|原文片段]]`；对话里的引用胶囊显示页码 + 段落预览，
  点击跳到对应页并在 PDF 文本层中高亮该段原文；高亮改为暖琥珀色，点击其它位置自动收起。
  修复 `react-markdown` 把 `|` 编码成 `%7C` 后引用落到系统协议、弹出「无法打开此 cite 链接」的问题。
- **导入进度**：按 arXiv / DOI、本地 PDF、拖拽、检索卡片和 Arxiver 助手导入时显示
  「查询元信息 → 下载 PDF → 写入文库 → 补全元数据」阶段；下载显示大小与百分比。
  PDF 下载改为 **60 秒无数据才超时**，不再限制总时长。
- **引擎 0.3.3**：修复多内容流 `Q` / `q` 被粘成 `Qq` 导致水印旋转矩阵泄漏、带 arXiv 竖排水印的页面整页漏翻。
  旧译文需要重新翻译一次才会补上该页。
- **设置清理**：移除没有实际功能的「同步与存储」页，以及自动保存笔记、PDF 默认缩放、默认引用格式、导出格式、
  AI 模型 / 附带引用来源 / 自动总结等占位项。
- **安装包**：跳过 NSIS 启动时的整包 CRC 校验，减少「verifying installer」等待；完整性由发布页 `SHA256SUMS` 保证。

### v0.10.0（2026-10-15）

- **运行状态（新）**：设置中新增「运行状态」页——已运行时长 / 进程数 / 合计内存 / 合计 CPU、内存与 CPU 趋势图
  （每 2 秒采样、保留约 3 分钟，离开本页仍在后台继续）、可分组与排序的进程列表（名称 / 类型 / PID / 内存 / CPU / 迷你趋势）、
  可切换「工作集 / 提交大小」两种口径；底部单列主进程的子进程（Python 引擎、本地模型服务 `llama-server`：PID / 内存 / 端口 / 正在翻的文件）
  与翻译任务进度；可暂停采样、打开日志文件，并 **一键导出诊断报告**（进程快照 + 环境信息 + 最近日志）。
- **进度与耗时**：阅读器进度条改为 **按页** 计算并显示百分比与转圈；每次翻译的分段耗时（引擎就绪 / 版面模型加载 / 版面分析 / 全流程）
  写进「日志 → 系统运行日志」；翻译预览改为 **每翻完一页** 就刷新，更跟手（保留 1 秒写入下限）。
- **日志视图**：翻译 / AI 对话 / 系统运行三类常驻，切换不再闪「暂无记录」；修复 **AI 对话日志点哪条都还停在第一条**。
- **AI 助手**：点 **停止不再清空内容**——保留已生成部分并标为「已暂停生成」，可 **「重新编辑问题」** 把问题回填输入框；消息去掉头像、收紧布局。
- **阅读与导航**：从阅读视图点导航或点侧栏分类 / 标签会回到文库视图，不再被阅读器盖住；Esc 只关弹层 / 整页视图，不误关文章；
  焦点描边只跟随键盘操作；详情面板「所有标签」改为对当前文献添加 / 移除。
- **修复**：同一篇论文导入两次时翻译日志出现两条重复记录；个别 PDF 在 **字体子集化** 一步导致整任务失败（现改为尽力而为，失败不中断翻译）；
  设置里的 API Key 与联网搜索项补上 DeepSeek / Tavily / 博查官网链接。
- 引擎更新至 **0.3.1**：字体子集化容错、预览刷新节奏、分段耗时埋点。

### v0.9.0（2026-10-14）

- **Arxiver 助手联网检索**：可搜索文库外的论文与资料，结果以卡片列出（标题 / 站点 / 年份 / 摘要片段 / 链接），
  带 arXiv 编号或 DOI 的条目可一键导入文库；回答里用 `卡片 N` 引用来源，点击滚动并高亮对应卡片。
  搜索服务商可选 **Tavily** 或 **博查（Bocha）**，两家 Key 各自保存、随时切换，检索范围可选 学术优先 / 全网。
- **读正文**：助手在给结论前会把最相关的网页 / PDF 正文读进来（优先服务端抽取，取不到就本机抓取），
  对话里显示「已读正文 · 站点 · 字数」并可打开原链接。
- **助手更多写作操作**：导入外部论文（arXiv 编号 / DOI / 链接）、增删笔记、重命名或删除分类、把文献移出分类等，
  全部先弹确认卡片；长任务（搜索 / 读正文 / 导入下载）显示当前阶段与已用时间；
  分类 / 标签名对不上时助手会自己查候选再确认，不再让你核对拼写。
- **日志视图重做**：左侧「日志」分 翻译日志 / AI 对话日志 / 系统运行日志 三类——每次翻译的状态与耗时、
  会话的完整工具调用步骤（参数 / 结果 / 计时 / Token）、分级运行记录（含联网检索与正文读取）。
- **文库分类与标签管理**：侧栏拖拽分类可调整顺序与层级（拖到分类上成为子分类），右键可新建 / 重命名 / 删除；
  标签右键可重命名 / 删除 / 调色（预设色 + 色轮）。删除分类只删分类本身，删除标签会从所有文献上移除，都不会删除文献。
- **导入更省事**：PDF 可直接拖到文献列表导入；「新建文献」支持粘贴 arXiv 链接 / 编号 / DOI 并自动取回元信息，
  入库后从 PDF 补全标题 / 作者 / 年份 / 来源；文献也能直接拖到侧栏分类里归类；列表上方新增搜索框。
- **阅读器**：打开默认「原文 + 单页」；工具栏新增块框按钮，可直接在阅读界面开关段落块框（无译文时不可用），
  块框改为点击钉住、面板贴着块框并跟随滚动；导出改到「翻译」下拉里的「导出译文文件…」，关闭文档用标签栏的 ×。
- **更新提示**：顶栏显示「有新的更新 / 正在下载更新 N% / 更新已就绪」，点击直达设置；
  启动时静默检查更新，「关于」里可下载 / 重启安装，并直接看到该版本的更新内容。
- **修复**：切换视图后块框消失；更换界面背景不生效；查看译文时块框默认值不对；设置项滑块样式异常；
  助手面板中间结果过长导致横向滚动、输入框首次打开点不进去；自定义安装目录时给出最终位置提示（并允许直接选驱动器根目录）。
- 列表与侧栏的**选中态**改为中性灰，不再用青绿色块填充。
- 引擎更新至 **0.3.0**：新增 `engine/pdfmeta.py`，探测 PDF 自带元信息与首页里的 arXiv 编号 / DOI，供导入时自动补全。
- ⚠️ **升级须知**：联网搜索**默认关闭**，需在「设置 → AI 助手 → 联网搜索」开启并填入**当前服务商**的 API Key；
  只发送检索式与要读取的网址，不上传本地文献内容（Key 以明文存于本机 `config.json`）。

### v0.8.0（2026-10-12）

- **多标签页阅读器**：每个文档独立渲染，切换标签不再重建 PDF、无闪烁；翻译在后台继续，任务按文档独立排队与取消。
- **文献列表重做**：标签改为可配色的**彩色圆点**（10 个预设 + 任意色轮取色，超出显示 `+N`）；标题单行省略，不再换行。
- **无书签 PDF 自动生成目录**：离线启发式按字号 / 加粗 / 编号 / 章节名识别标题，面板标注「自动生成」，结果缓存。
- **启动动画与自定义界面背景**：开屏动画可开关；界面背景支持图片 / 视频（视频静音循环），并提供不透明度滑块。
- **块框显示拆分**：分别控制「翻译时」与「查看译文时」是否标出文本块。
- **修复**：目录点击错跳 / 多条目同时高亮 / 点击无反应；启动瞬间「整屏灰色 + 左上角黑块」；界面设置偶发丢失（改存本地 `ui-settings.json`，同步落盘）。
- ⚠️ **升级须知**：界面设置不再读取旧的浏览器存储，升级后外观 / 启动选项会回到默认值，请重新设置一次；**文库、笔记、已有译文与标签不受影响**。

### v0.7.0（2026-10-11）

- **本地离线翻译**：翻译改由随包分发的 HY-MT 翻译模型（llama.cpp）在本机完成，安装即用、无需 API Key；
  有 NVIDIA 显卡走 GPU，无独显 / 驱动不匹配时自动回退 CPU。
- **翻译与会话分离**：AI 助手使用独立配置的在线接口，与翻译互不影响，也更省 API 费用。
- **版面识别提速**：改用 DirectML 显卡加速（约 6–10 倍），无 DX12 显卡自动回退 CPU。
- **预览更流畅**：修复翻译过程中预览 PDF 的重复重建，长文档整体更快。
- ⚠️ **升级须知**：配置项已重命名（`openai_*` → `translate_*` / `chat_*`），升级后请在「设置 → AI 助手」
  重新填写接口；文库、笔记与已有译文保留。

### 桌面版（Electron）

以 Electron 桌面应用取代原「浏览器扩展 + 本机服务 + 托盘启动器」组合。

- **桌面文献库**：导入、分类、标签、回收站、阅读历史与检索。
- **双语对照阅读器**：原文 / 对照 / 译文三视图，单页 / 双页、缩放、目录大纲、缩略图、页面主题。
- **内嵌引擎（本地离线翻译）**：随应用分发 HY-MT 翻译模型（llama.cpp），默认在本机离线翻译；有 N 卡走 GPU，无独显自动回退 CPU。AI 助手使用独立配置的在线接口。
- **段落块框与引用**：悬停显示「原文 → 译文」；引用预览目标页、点击跳转。
- **Arxiver 助手**：基于当前文章与整库的对话式检索、可点击引用、`@` 引用已打开文献、选中文本提问；
  标签 / 元数据等写操作经人机协作确认；会话持久化与历史。
- **自动更新**：`electron-builder`（NSIS）+ `electron-updater` 差量更新，未变的大文件不重复下载。
