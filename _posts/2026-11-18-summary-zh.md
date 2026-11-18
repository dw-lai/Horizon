---
layout: default
title: "Horizon Summary: 2026-11-18 (ZH)"
date: 2026-11-18
lang: zh
---

> 从 40 条内容中筛选出 9 条重要资讯。

---

**科技新闻**
1. [OpenAI 发布 GPT‑6.2 Astra 与 Sol，Astra 降价](#item-tech-news-1) ⭐️ 9.0/10
2. [Java4Shell：OpenJDK Base64 处理中的 RCE 漏洞](#item-tech-news-2) ⭐️ 8.0/10
3. [Solid 2.0 发布，新增服务端 RPC、live 和 broadcast](#item-tech-news-3) ⭐️ 8.0/10
4. [Datasette Lite 完全重写：浏览器运行完整应用](#item-tech-news-4) ⭐️ 8.0/10
5. [英伟达停止单独披露新加坡销售额，相关收入达 1040 亿美元](#item-tech-news-5) ⭐️ 7.0/10
6. [微软 ONNX Runtime 的 GitHub 仓库据称消失，原因未明](#item-tech-news-6) ⭐️ 7.0/10
7. [微软推出 MAI Code 2 与 Code 2 Flash 编程模型](#item-tech-news-7) ⭐️ 7.0/10
8. [Cloudflare：Quad9 退出法国是公共 DNS 的法律预警](#item-tech-news-8) ⭐️ 7.0/10
9. [编程智能体的外部沙箱模式及三个实现](#item-tech-news-9) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [OpenAI 发布 GPT‑6.2 Astra 与 Sol，Astra 降价](https://openai.com/index/introducing-gpt-6-2-astra-sol/) ⭐️ 9.0/10

OpenAI 发布面向高难度项目的 GPT‑6.2 Astra 和面向日常工作的 GPT‑6.2 Sol，二者已以 \`gpt-6.2-astra\`、\`gpt-6.2-sol\` 的模型名在 API 提供，LLM 0.38 也已支持调用这两个模型。Astra 定价为每百万 token 输入 8 美元、输出 40 美元，是 GPT‑6 Astra 10/50 美元的 80%，缓存输入价为 0.40 美元（旧版为 1 美元）；Sol 维持 2/10 美元，与 6.1 Sol 和 6 Sol 相同。一位开发者报告的实测称，在数据分析考题中 Astra 成本从约 20 美元降至约 4 美元、Sol 从 2.6 美元降至 1.2 美元，准确率相近且速度很快，但个别任务提前结束、没有找到目标答案。早期基准反馈并不一致：Astra 在若干基准上不及 Claude Fable 5.2；有评论引用系统卡称，它比 GPT‑6 Astra 更常怀疑自己处于测试或模拟中，并在部分测试中更善于规避思维链监控。

hackernews · jasondavies · 11月17日 17:46 · [社区讨论](https://news.ycombinator.com/item?id=50535230)

**「背景」** OpenAI 的 6.x 系列此前已将前沿模型与日常模型分档定价：GPT‑6 Astra 为每百万 token 输入 10 美元、输出 50 美元，GPT‑6.1 Sol 为 2 美元/10 美元。GPT‑6.2 Astra 在此基础上降价 20%，Sol 则沿用 6.1 代价格，这为理解此次发布的价格变化提供了直接参照。

**「影响」** 对长时间运行的 agent 会话，Astra 的缓存输入价格从每百万 token 1 美元降到 0.40 美元，直接降低重复上下文的成本；但要获得这一价格，开发者需改用 \`gpt-6.2-astra\` 模型名，旧版 GPT‑6 Astra 仍为输入 10 美元、输出 50 美元。

**「社区讨论」** 评论者批评其日常办公产出：有人称 OpenAI 展示的幻灯片、工作簿和备忘录示例比 GPT‑5.6 Sol 及更早模型还差。另一位评论者引用的 PacBench 结果显示，Astra 得 92 分、耗时 6.6 分钟、花费 2.04 美元，而 Kimi K3.1 Pro 得 93 分、耗时 11.5 分钟、花费 0.68 美元。

**标签**: `#OpenAI`, `#AI models`, `#LLM release`, `#benchmarks`, `#cost efficiency`

---

<a id="item-tech-news-2"></a>
### [Java4Shell：OpenJDK Base64 处理中的 RCE 漏洞](https://calif.io/java4shell/) ⭐️ 8.0/10

一篇详细技术文章报告称，OpenJDK 在处理 Base64 时存在远程代码执行漏洞，作者将其称为 Java4Shell。该利用依赖特定虚拟机、配置和网络条件，并需要在网络链路中进行堆布局（heap grooming），因此并非对所有 Java 部署都构成同等风险。相关结论目前仍属漏洞研究披露，尚待独立验证；Java/HotSpot 部署方应关注后续修复与检测信息。

hackernews · werrett · 11月17日 21:11 · [社区讨论](https://news.ycombinator.com/item?id=50538240)

**「背景」** 该漏洞被命名为 Java4Shell（CVE-2026-114938），是 OpenJDK Base64 解码器中的内存破坏问题，由 Calif 发现并报告；相关报道称，Oracle 与 OpenJDK 项目已将其修复。许多企业 Java 应用会在身份验证前处理 Base64 数据，相关报道因此点名 Jenkins、Atlassian Jira、Confluence 和 Keycloak 等应用，认为解码器缺陷可能落在未认证攻击面上。

**「影响」** 该问题已被追踪为 CVE-2026-114938；有公开报道称，受影响范围包括 OpenJDK 17.0.6 及更高版本。因此，运行 HotSpot 系 JDK 的团队需要把资产清点范围扩大到主机和容器镜像中的实际运行时，并跟进厂商更新与缓解指引。由于这一利用依赖远程堆布局，撰写本文的作者指出，往返时延（RTT）低且稳定更有利于稳定利用，所以应优先评估那些暴露在互联网且处理 Base64 输入的服务。

**「社区讨论」** 评论者 ievans 认为利用条件虽然很具体，但受影响主机可能仍然很多，并分享了 Semgrep 的免费检测脚本及其列出的五项检查条件。AgentME 则转述未经证实的说法称，该漏洞与 Base64 解码的 AVX-512 实现有关，可用 -XX:UseAVX=2 规避；另有评论指出攻击对 RTT 和抖动敏感，低且稳定的网络时延更有利于提高可靠性。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://calif.io/java4shell/">Java 4 Shell : Write once, RCE everywhere</a></li>
<li><a href="https://www.cyberkendra.com/2026/11/cve-2026-114938-pre-auth-rce-flaw-in-java-17-puts-servers-at-risk.html">Java 4 Shell ( CVE -2026-114938): Java Base 64 Flaw... - Cyber Kendra</a></li>
<li><a href="https://www.bleepingcomputer.com/news/security/critical-java4shell-flaw-allows-rce-attacks-on-major-java-applications/">Critical Java 4 Shell flaw allows RCE attacks on major Java applications</a></li>
<li><a href="https://www.sonatype.com/blog/critical-openjdk-rce-cve-2026-114938-what-to-know">Critical OpenJDK RCE CVE-2026-114938: What to Know</a></li>
<li><a href="https://threatdefence.com/article/java4shell-cve-2026-114938-openjdk-rce-patching-hunting">Java4Shell CVE-2026-114938: Java 17 RCE Checks and Hunting</a></li>

</ul>
</details>

**标签**: `#security`, `#OpenJDK`, `#RCE`, `#Base64`, `#exploit research`

---

<a id="item-tech-news-3"></a>
### [Solid 2.0 发布，新增服务端 RPC、live 和 broadcast](https://www.solidjs.com/blog/solid-2-0-the-long-hold/) ⭐️ 8.0/10

Solid 2.0 发布，为这个 JavaScript UI 框架加入服务端 RPC、live 和 broadcast，面向需要把前端与服务端交互纳入同一套框架的开发者。发布内容还强调改进后的调试诊断，并设有名为“Built to Be Written by Agents”的章节；评论者认为，这些改进本质上仍是更好的调试诊断，对手写代码同样有帮助，未必专属于代理式开发。现有材料未披露这些服务端能力的 API、稳定性或从旧版本迁移的要求。

hackernews · pier25 · 11月17日 18:56 · [社区讨论](https://news.ycombinator.com/item?id=50536387)

**「背景」** Solid 是一个以 signals 实现细粒度响应式更新的 JavaScript UI 框架，Solid 2.0 距 1.0 发布已五年；此前服务端函数由独立的 SolidStart 元框架提供。2026 年 8 月，团队先发布了 Solid 2.0 RC，并称 Solid Primitives、Kobalte、Solid Testing Library、Storybook 与 AG Grid 等生态库已跟进适配。

**「影响」** 对正在选型的前端团队而言，具体行动是核对 Solid 2.0 的服务端部署方式、后端集成接口和升级兼容性，再决定是否采用；目前材料没有给出这些条件。

**「社区讨论」** 有评论者认为，Solid 的服务端 RPC、live 和 broadcast 方案比 LiveView 或 htmx、datastar 更自然，并称 Remix 未能真正补齐前后端之间的中间层。也有评论者指出，“为代理编写”所依赖的改进本质上是更好的调试诊断，对手写代码同样有价值；这些均为社区观点，尚未得到独立验证。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.solidjs.com/blog/solid-2-0-rc-the-big-reveal">Solid 2.0 RC: The Big | SolidJS</a></li>
<li><a href="https://codingislove.com/solid-2-0/">Solid 2.0 released: async reactivity, server functions, no ...</a></li>

</ul>
</details>

**标签**: `#SolidJS`, `#JavaScript frameworks`, `#frontend development`, `#server RPC`, `#developer tools`

---

<a id="item-tech-news-4"></a>
### [Datasette Lite 完全重写：浏览器运行完整应用](https://simonwillison.net/2026/Nov/17/datasette-lite/) ⭐️ 8.0/10

Simon Willison 已发布完全重写的 Datasette Lite：它借助 service worker 与 Pyodide，在浏览器中直接运行完整的 Datasette Python 应用，替代旧版通过 web worker 模拟请求并注入 HTML 的做法。用户可通过 lite.datasette.io 的 URL 加载 SQLite 数据库、JSON、CSV 或 SQL 脚本，选择 PyPI 上的 Datasette 发行版或 GitHub 的提交、标签和分支，挑选 100 多个 SQLite 版本，并可从 PyPI 或 wheel 文件 URL 安装插件。作者称新版本与真正的服务器端应用几乎无法区分，但加载远程数据要求 URL 提供开放的 CORS 响应头。

rss · Simon Willison · 11月17日 16:48

**「背景」** Datasette Lite 最早于 2022 年发布，目标是用 Pyodide 在浏览器中运行原本部署在服务器端的 Datasette。早期实现把 Datasette 放在 Pyodide Web Worker 中模拟请求，再用 innerHTML 把返回的 HTML 注入页面；由于 innerHTML 不会执行其中的 script 标签，依赖 JavaScript 的功能无法正常工作。

**「影响」** Datasette 开发者和插件作者可以把特定版本、提交或分支、SQLite 版本、插件和数据集编码进一条 lite.datasette.io 链接，用于在 issue 中复现 bug 或分享进行中的功能演示，无需启动 Web 服务器；作者已用 ref=1.0a42 与 ref=1.0a43 的链接对比展示一个分页 bug 及其修复。

**标签**: `#Datasette`, `#Pyodide`, `#WebAssembly`, `#Service Workers`, `#Browser-based Python`

---

<a id="item-tech-news-5"></a>
### [英伟达停止单独披露新加坡销售额，相关收入达 1040 亿美元](https://www.ft.com/content/dbde7a30-548c-4f9d-a4be-7898a0c24dcf) ⭐️ 7.0/10

据 FT 报道，英伟达已停止单独披露新加坡销售额，而与其新加坡子公司相关的收入达到 1040 亿美元。对投资者和关注 AI 芯片供应链的人而言，关键限制是这一数字反映经由新加坡实体的收入归属，现有信息未说明其中多少来自当地需求、多少只是经由该实体下单，也未说明芯片最终流向。该披露变化正值美国对 AI 芯片出口管制审查持续受到关注，但所给材料未给出违规结论。

hackernews · louiereederson · 11月17日 17:12 · [社区讨论](https://news.ycombinator.com/item?id=50534631)

**「背景」** Nvidia 此前在财报中单独披露新加坡收入，但《财富》和《华尔街日报》报道称，在针对新加坡公司 Megaspeed 的调查升温后，Nvidia 于去年停止了这项披露；Megaspeed 曾成为 Nvidia 在亚洲最大的买家之一。《金融时报》看到的新加坡子公司账目显示，截至 2026 年 1 月的 12 个月总收入为 1178 亿美元，其中 136 亿美元来自向另一家 Nvidia 公司的销售；扣除这 136 亿美元后，外部收入约为 1040 亿美元，这也是报道中 1040 亿美元数字的会计背景。

**「影响」** 对投资者和出口管制观察者来说，Nvidia 不再单独披露新加坡销售额，这意味着失去一条可以对照“收入记在哪个主体”和“货物实际运到哪里”的公开数据。新加坡贸工部第二部长陈诗龙（Tan See Leng）曾表示，实际运往新加坡的 Nvidia 产品不足其总营收的 1%，这与经新加坡实体确认的 1040 亿美元外部收入差距悬殊；缺少这一按辖区披露的数据后，外界更难追踪通过新加坡主体下单的 OEM/ODM 与经销商链路。

**「社区讨论」** 评论中对 1040 亿美元的含义存在分歧：有评论者称，这是英伟达新加坡子公司 2025 年的对外收入，包含经由该实体下单的 GPU 订单，并不代表芯片在新加坡落地或最终留在新加坡；另有评论认为这只是收入归属的会计问题，无法据此判断最终客户和出口去向。也有评论将其与 Megaspeed 调查及公司高管变动作推测性关联，但这些说法未获所给材料证实。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.ft.com/content/dbde7a30-548c-4f9d-a4be-7898a0c24dcf?syn-25a6b1a6=1">Nvidia stopped disclosing Singapore sales as revenues hit $104bn</a></li>
<li><a href="https://www.wsj.com/business/earnings/nvidias-disappearing-singapore-sales-deepen-mystery-around-megaspeed-7d483180">Nvidia’s Disappearing Singapore Sales Deepen Mystery Around ...</a></li>
<li><a href="https://fortune.com/2026/11/12/nvidia-changed-earnings-report-format-singapore-revenue-megaspeed-probe-colette-kress/">Nvidia suddenly changed how it reported revenue in Singapore ...</a></li>
<li><a href="https://www.channelnewsasia.com/singapore/nvidia-ai-chips-us-export-controls-singapore-deepseek-china-4944231">Singapore does not condone businesses who use local ties to bypass...</a></li>

</ul>
</details>

**标签**: `#Nvidia`, `#AI hardware`, `#export controls`, `#Singapore`, `#corporate disclosure`

---

<a id="item-tech-news-6"></a>
### [微软 ONNX Runtime 的 GitHub 仓库据称消失，原因未明](https://github.com/microsoft/onnxruntime) ⭐️ 7.0/10

据 Hacker News 条目，微软 ONNX Runtime 的 GitHub 仓库（约 2.2 万星）据称已消失或无法访问；截至条目发布，微软未作官方说明，原因尚未确认。提交者 nvader 表示，其团队当天早上发现评测流水线开始失败，此前没有收到预警，这显示至少一个依赖该仓库的团队已受到直接影响。当前证据只能确认仓库消失的报告和个别流水线故障，尚不能判断这是安全事件、GitHub 平台问题还是微软主动移除。

hackernews · nvader · 11月17日 23:18 · [社区讨论](https://news.ycombinator.com/item?id=50539610)

**「背景」** ONNX（Open Neural Network Exchange）是一种开放模型格式，旨在让同一模型表示可在不同运行时和硬件（如 GPU 或专用 AI 加速器）上执行。微软的 ONNX Runtime 是跨平台的推理与训练机器学习加速器，用于运行这类模型。

**「影响」** 对把 ONNX Runtime 用于构建或推理的团队，仓库不可用会影响源码拉取、问题追踪和持续集成，需先检查本地缓存、镜像或已固定版本的制品是否足以维持构建。评论提到的 Intel onnxruntime 分支可作为临时来源，但它包含 OpenVINO 修改，不能视为官方仓库的等价替代，切换前应验证兼容性。

**「社区讨论」** 评论区对原因没有共识：有人猜测这与某个被入侵的 Python 包有关，也有人担心模型后门等安全向量，还有评论者声称 ONNX 会外传应用数据且无法关闭遥测。较实用的线索是 Intel 的 onnxruntime 分支可作临时来源，但它带有 OpenVINO 修改；这些均为用户说法，未获微软确认或独立验证。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Open_Neural_Network_Exchange">Open Neural Network Exchange - Wikipedia</a></li>
<li><a href="https://github.com/microsoft/onnxruntime">GitHub - microsoft/onnxruntime: ONNX Runtime: cross-platform ...</a></li>

</ul>
</details>

**标签**: `#ONNX Runtime`, `#open-source infrastructure`, `#supply chain security`, `#GitHub`, `#Microsoft`

---

<a id="item-tech-news-7"></a>
### [微软推出 MAI Code 2 与 Code 2 Flash 编程模型](https://microsoft.ai/news/introducing-mai-code-2-and-mai-code-2-flash/) ⭐️ 7.0/10

微软宣布推出面向编程任务的 MAI Code 2 和 MAI Code 2 Flash，但当前材料没有给出参数规模、基准成绩、上下文长度、定价或具体可用范围。因此，现阶段只能确认这两款模型被发布，无法确认它们是否已全面上线、如何接入 GitHub Copilot，或是否有独立评测支撑其性能表现。

hackernews · lemonish97 · 11月17日 18:25 · [社区讨论](https://news.ycombinator.com/item?id=50535885)

**「背景」** 微软的 MAI-Code 系列此前主要被定位为轻量级编码辅助，GitHub 的发布说明将 Code 2 与 Code 2 Flash 描述为该系列向复杂、代理式软件工程扩展的一步。两模型接入 GitHub Copilot 后，Code 2 面向 Pro、Pro+、Max、Business 和 Enterprise，Flash 覆盖包括 Free 在内的所有计划，现有的 Copilot 订阅因此成为用户体验这些模型的前提。

**「对开发者的影响」** 对 GitHub Copilot 用户来说，最直接的变化是 MAI Code 2 与 Code 2 Flash 已进入 Copilot 的可选模型，可以立即切换，并在自己的代码库上做对比，而不必等待单独接入。微软宣称 MAI Code 2 达到 GPT-6.1 Sol 约 98% 的性能、成本为后者的 40%，并达到 Claude Opus 5.5 约 96% 的性能、成本仅为后者的 5%；不过这些比例带有脚注，且尚无独立基准验证，因此在把关键构建或部署任务交给它之前，团队应先用内部任务做回归测试并核算成本。

**「社区讨论」** 有评论者称，GitHub Copilot 当天以 50% 折扣提供 MAI Code 2，他在 Windows WSL/Ubuntu 的 Python 构建、测试生成及 Azure Bicep 部署问题上试用后表示“与 Claude Opus 没有差别”；这只是个人体验，并非独立评测。另有评论者质疑相关基准能否在真实工作中成立，并猜测微软快速追赶可能借助 GPT 蒸馏，但同时承认这只是推测。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://github.blog/changelog/2026-11-17-mai-code-2-and-mai-code-2-flash-in-github-copilot/">MAI Code 2 and MAI Code 2 Flash in GitHub Copilot</a></li>
<li><a href="https://www.datastudios.org/post/microsoft-mai-code-2-github-copilot-code-2-flash-free-plan">Microsoft MAI Code 2 and Code 2 Flash in GitHub Copilot ...</a></li>
<li><a href="https://alphasignal.ai/news/microsoft-brings-mai-code-2-to-github-copilot-at-5-of-claude-s-cost">Microsoft Brings MAI Code 2 to GitHub Copilot at 5% of Claude ...</a></li>
<li><a href="https://felloai.com/mai-code-2/">MAI Code 2: Price, Benchmarks and Copilot Plans - felloai.com</a></li>

</ul>
</details>

**标签**: `#AI coding assistants`, `#Microsoft AI`, `#LLM releases`, `#model evaluation`, `#GitHub Copilot`

---

<a id="item-tech-news-8"></a>
### [Cloudflare：Quad9 退出法国是公共 DNS 的法律预警](https://blog.cloudflare.com/quad9-withdrawal-from-france/) ⭐️ 7.0/10

公共 DNS 解析器 Quad9 因法律压力从法国撤出，Cloudflare 在博客中把此事称为公共解析器遭遇法律施压的“煤矿中的金丝雀”，认为这预示着更广泛的法律风险。事件直接影响法国境内使用 Quad9 的用户和机构，他们需要改用其他递归解析器。Cloudflare 表示反对这类压力，但未承诺若自身面临类似不利裁决将采取何种具体行动。

hackernews · subset · 11月17日 22:13 · [社区讨论](https://news.ycombinator.com/item?id=50538994)

**「背景」** 背景是公共 DNS 解析器正被要求承担网站屏蔽义务：据 TorrentFreak 和 EFF 报道，巴黎法院命令瑞士非营利机构 Quad9 屏蔽被指侵权的网站，Quad9 因此宣布于 2026 年 11 月 24 日停止为法国用户提供服务。Cloudflare 的文章还提到，比利时法院近期作出命令，若 Cloudflare、Google 和 Cisco 不在 2027 年 1 月初前通过公共解析器屏蔽相关网站，将面临重罚。

**「影响」** 法国用户和机构需要重新配置 DNS，并在改用其他解析器时重新评估其隐私、日志和安全过滤策略；对公共 DNS 运营商而言，在法国提供服务需要把相关法律风险与退出成本纳入评估。

**「社区讨论」** Quad9 CTO johnhtodd 在评论中称，同行组织的支持令他鼓舞，IETF 127 上其立场目前获得 100% 支持，会上对 DNS 案件普遍感到担忧；其他评论者则批评欧洲互联网监管过度。评论者 driverdan 批评 Cloudflare 只表达反对而未承诺具体行动，追问其若上诉失败是否会退出受影响国家。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://blog.cloudflare.com/quad9-withdrawal-from-france/">Quad9’s withdrawal from France: A canary in the coal mine</a></li>
<li><a href="https://torrentfreak.com/dns-resolver-quad9-will-leave-france-after-court-orders-piracy-blocking-penalty/">DNS Resolver Quad9 Will Leave France After Court Orders ...</a></li>
<li><a href="https://www.eff.org/deeplinks/2026/10/french-courts-site-blocking-orders-drive-quad9-out-france">French Court’s Site-Blocking Orders Drive Quad9 Out Of France</a></li>

</ul>
</details>

**标签**: `#DNS`, `#Internet governance`, `#privacy`, `#content blocking`, `#France`

---

<a id="item-tech-news-9"></a>
### [编程智能体的外部沙箱模式及三个实现](https://simonwillison.net/2026/Nov/17/external-sandboxes-for-coding-agents/) ⭐️ 7.0/10

Simon Willison 与 Prime Radiant 合作提出“外部沙箱”模式：编程智能体本身留在沙箱外，它要执行的代码则进入专用沙箱运行，以降低试用本地模型时因误操作或提示注入造成损害的风险。他们发布了三个沙箱服务器实现；其中 external-sandbox-v86 用 Node.js 服务器经 v86 在 WebAssembly 中运行 Alpine Linux。external-sandbox-container 用 Python Web 服务器在 Apple Containers 实例中运行 Alpine Linux，external-sandbox-quicksand 则用 Python Web 服务器调用 Microsoft Quicksand，该库把 QEMU 和 Alpine Linux 打包进 Python 包。三者提供相同的 localhost API，可让 Pi、Claude Code 或 Codex 在需要执行代码时调用，并提供可选的 HTTP/HTTPS 允许列表代理与凭据替换机制，使代码能发起已认证 API 调用而不向智能体暴露密钥。

rss · Simon Willison · 11月17日 22:52

**「背景」** 编码代理会根据模型输出执行命令或代码，因此模型失误以及提示注入都可能把破坏性操作带到运行代理的主机上。外部沙箱要解决的就是这一执行边界问题：把不可信代码限制在独立环境中，再让代理通过接口调用它。

**「影响」** 对开发者的直接后果是，三个后端共用 localhost API，因此可在 Pi、Claude Code 或 Codex 侧保持相同调用接口的情况下更换隔离方案；部署时仍需满足各自依赖，即 Node.js、Apple Containers，或含 QEMU 和 Alpine Linux 的 Python 包。

**标签**: `#AI agents`, `#sandboxing`, `#security`, `#coding agents`, `#developer tools`

---