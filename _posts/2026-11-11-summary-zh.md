---
layout: default
title: "Horizon Summary: 2026-11-11 (ZH)"
date: 2026-11-11
lang: zh
---

> 从 52 条内容中筛选出 6 条重要资讯。

---

**科技新闻**
1. [.NET 11 运行时更新说明：runtime async 与兼容性变化](#item-tech-news-1) ⭐️ 9.0/10
2. [DeepMind 公布 AlphaProof Code，验证范围引争论](#item-tech-news-2) ⭐️ 8.0/10
3. [Chips and Cheese 解析 AMD Zen 6 微架构取舍](#item-tech-news-3) ⭐️ 8.0/10
4. [删除不到 0.05% 权重即可匹配全量微调：Deletion Tuning](#item-tech-news-4) ⭐️ 8.0/10
5. [评论：智能家居设备应能脱离互联网独立运行](#item-tech-news-5) ⭐️ 7.0/10
6. [Chrome 联合 Firefox、MDN、Edge 发布 modern-web-guidance 1.0](#item-tech-news-6) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [.NET 11 运行时更新说明：runtime async 与兼容性变化](https://learn.microsoft.com/en-us/dotnet/core/whats-new/dotnet-11/runtime) ⭐️ 9.0/10

微软已公布 .NET 11 运行时的新特性与兼容性说明，面向计划升级的 .NET/C\# 开发者。社区讨论重点提到 runtime async，认为它能减少状态机并让堆栈更易读，但其在切换运行时后能否保持同等性能仍只是使用者的初步观察。另有评论引用兼容性文档警告 decimal 格式化变化：\(decimal\)0.1 在 .NET 10 输出 0.1，在 .NET 11 输出 0.1000000000000000055511151231，升级前应检查依赖该行为的代码。

hackernews · stevefan1999 · 11月10日 12:20 · [社区讨论](https://news.ycombinator.com/item?id=50439284)

**「背景」** 作为 .NET 11 的主要运行时特性，runtime async 将异步方法所需的基础设施引入运行时层面，目标是改善异步密集代码路径的工具支持与性能；该特性在 Preview 1 的运行时说明中已有介绍。Microsoft Learn 的运行时文档还指出，异步分析器现在同时覆盖 runtime-async 方法和编译器生成的 async 状态机方法，从而为工具提供一致的事件模型。

**「升级前需核查的兼容性影响」** 升级到 .NET 11 的团队需要重点核查数值格式化行为的差异：社区讨论指出，\(decimal\)0.1 在 .NET 10 中输出为 0.1，而在 .NET 11 中变为 0.1000000000000000055511151231，依赖数值字符串输出的序列化、日志和测试断言因此可能出现不一致，应参照官方兼容性文档逐项确认。与此同时，.NET 11 引入的运行时原生 async（Runtime Async V2）把 async 挂起与恢复的职责从编译器生成的状态机转向运行时管理，性能调优和诊断方式需要按新运行时重新评估，不能沿用旧版本的基准假设。

**「社区讨论」** 有评论者认为 C\#/.NET 因历史包袱被低估：外界仍误以为它只能在 Windows 上运行，或仍停留在 .NET Framework 时代，但日常后端开发体验很好。另有评论者对 runtime async 在减少状态机的同时仍可能保持相当性能感到意外。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://learn.microsoft.com/en-us/dotnet/core/whats-new/dotnet-11/runtime">What&#x27;s new in .NET 11 runtime | Microsoft Learn</a></li>
<li><a href="https://github.com/dotnet/core/blob/main/release-notes/11.0/preview/preview1/runtime.md">core/release-notes/11.0/preview/preview1/runtime.md at main ...</a></li>
<li><a href="https://learn.microsoft.com/en-us/dotnet/core/whats-new/dotnet-11/runtime">What&#x27;s new in . NET 11 runtime | Microsoft Learn</a></li>
<li><a href="https://www.c-sharpcorner.com/article/benchmarking-c-sharp-async-tail-await-optimizations-in-net-11/">Benchmarking C# Async Tail-Await Optimizations in . NET 11</a></li>
<li><a href="https://www.linkedin.com/posts/arianzhurovich_dotnet-csharp-aspnetcore-activity-7496861231589253120-ptNB">Runtime Async in . NET 11 Shifts Responsibility from... | LinkedIn</a></li>

</ul>
</details>

**标签**: `#.NET 11`, `#C\#`, `#runtime`, `#async`, `#compatibility`

---

<a id="item-tech-news-2"></a>
### [DeepMind 公布 AlphaProof Code，验证范围引争论](https://deepmind.google/blog/introducing-alphaproof-code/) ⭐️ 8.0/10

DeepMind 通过官方博客公布了 AlphaProof Code，将其定位为面向代码形式化验证的 AI 证明代理；但本条材料未附公告正文，因此版本、可用范围、支持的语言与工具链以及任何基准或实测结果都无法确认，目前只能视为公告层面的信息。Hacker News 的讨论集中在它实际证明了什么：有评论者指出，这类工具验证的是实现是否满足给定规格，并不检验规格本身是否正确。另一位评论者对“对一个历史上出现过缺陷的非平凡库完成形式化验证、且发现零 bug”表示怀疑，猜测可能只证明了较窄的性质，或者定理本身写错了。

hackernews · ilreb · 11月10日 12:11 · [社区讨论](https://news.ycombinator.com/item?id=50439193)

**「背景：形式化验证的前提」** 形式化验证的核心，是先把安全目标写成精确规范，再让 Lean 等证明助理逐行机器检查实现是否满足规范；因此，证明只能覆盖规范所表达的性质，不能自动证明规范本身完整。相关报道显示，AlphaProof Code 采用人类专家与多个 LLM 分工的流程：人类审阅 Signal 协议的形式化规范，智能体生成数百万行 Lean 证明。

**「影响」** 对考虑采用这类证明代理的团队来说，直接约束是规格仍需由人来编写和审查：如果定理只覆盖有限性质，“已验证”就不能替代对规格正确性的检查。评论中 andai 描述的经历——编码代理耗时数小时完成重构、自建测试全部通过，但实现方向完全做反——说明当验证目标本身出错时，工具通过并不能说明结果正确。

**「社区讨论」** hedora 质疑在一个历史上出现过 bug 的非平凡代码库上得到“零 bug”的结果，怀疑定理范围过窄或命题写错；thibsrn 则认为该代理只针对实现、不挑战规格，并追问它与普通编码代理反复编写 Lean 或 Rocq 代码的做法有何本质区别。andai 补充了一次亲身经历：编码代理用数小时完成重构并让自建测试全部通过，但实现方向完全做反，以此说明测试或验证通过本身不足以证明目标正确。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://explainx.ai/blog/google-deepmind-alphaproof-code-signal-protocol-formal-verification-2026">AlphaProof Code: Signal Protocol Verified in 4 Weeks ...</a></li>
<li><a href="https://codingislove.com/alphaproof-code-signal/">DeepMind&#x27;s AlphaProof Code formally verifies Signal&#x27;s ...</a></li>

</ul>
</details>

**标签**: `#AlphaProof`, `#formal verification`, `#AI proof agents`, `#Lean/Rocq`, `#DeepMind`

---

<a id="item-tech-news-3"></a>
### [Chips and Cheese 解析 AMD Zen 6 微架构取舍](https://chipsandcheese.com/p/amds-zen-6-family-feeding-the-beast) ⭐️ 8.0/10

Chips and Cheese 发布了对 AMD Zen 6 系列的技术分析，围绕 I/O 芯片、内存控制器、分支预测、整数乘法与 PDEP/PEXT 吞吐、向量加载及 VNNI 管线梳理其微架构取舍。该文面向关注 CPU 架构和系统性能的读者，但本次没有提供原文内容，因此文章的具体结论和数字无法在此独立核实。社区评论中提到的规格应视为读者转述，而非 AMD 已确认的产品信息。

hackernews · pixelpoet · 11月10日 17:02 · [社区讨论](https://news.ycombinator.com/item?id=50443090)

**「背景」** 这篇 Chips and Cheese 分析以 Zen 5 为参照，考察 Zen 6 的核心微架构变化，并比较 Zen 6 与 Zen 6c 的设计差异。Zen 6 和 Zen 6c 已随 EPYC 9006（Venice）首次亮相，接替采用 Zen 5 与 Zen 5c 的 EPYC 9005（Turin）。

**「社区讨论」** 评论者把 AM5 上 Zen 4/Zen 5 的内存控制器视为主要短板，称双通道下很难超过 3600 MT/s，并期待 Zen 6 改用更小制程的新 I/O 芯片来改善；这一体验是个人报告，尚未在讨论中得到验证。另一些评论则讨论 2-ahead 分支预测的指令级并行、整数乘法单元从三个减到两个、PDEP/PEXT 吞吐下降、每周期四条 256 位向量加载，以及每个 chiplet 32 个 C 核的布局。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://chipsandcheese.com/p/amds-zen-6-family-feeding-the-beast">AMD ’ s Zen 6 Family : Feeding the Beast - by George Cozma</a></li>
<li><a href="https://wccftech.com/amd-zen-6-architecture-ipc-cores-memory-performance-epyc-venice/">AMD Zen 6 Architecture Brings A Phenomenal 27% IPC Increase Over...</a></li>

</ul>
</details>

**标签**: `#AMD Zen 6`, `#CPU architecture`, `#microarchitecture`, `#memory controller`, `#branch prediction`

---

<a id="item-tech-news-4"></a>
### [删除不到 0.05% 权重即可匹配全量微调：Deletion Tuning](https://www.reddit.com/r/LocalLLaMA/comments/1xswmb7/the_surprising_effectiveness_of_deleting_weights/) ⭐️ 8.0/10

一项名为 Deletion Tuning 的研究提出：只学习一个作用于 Transformer 模块 gate projection 的二值掩码，把不到 0.05% 的权重置零、其余参数完全不动，就能在大规模场景下匹配全量微调（FFT）的效果。作者称该方法在三种后训练范式上均成立——可验证奖励的强化学习（RLVR）、监督微调（SFT）和 on-policy 蒸馏——并带来两个实际好处：训练出的掩码比对应的 FFT checkpoint 小数百到数千倍，且灾难性遗忘显著更少。在强化学习设置下，Deletion Tuning 在先前任务上的准确率保持在基座模型附近，而 FFT、LoRA 与随机稀疏微调的基线最多下降 5.4 个百分点。作者还用 stable rank、spectrum drift 与 principal-weight overlap 分析 RL 下权重变化的几何结构，发现 Deletion Tuning 在这三项指标上都最接近 FFT；需要说明的是，这些结论来自单篇论文，尚未经过独立复现验证，目前仅有 Reddit 帖子、GitHub/HuggingFace 仓库、博客与 NeurIPS 2026 poster 链接作为公开材料。

reddit · r/LocalLLaMA · /u/Thrumpwart · 11月10日 19:44

**「背景」** 同一研究线的早期版本以 Bit-Mask Tuning（BMT）为名，在 OpenReview 上描述了类似做法：只学习 Transformer 块 gate projection 上的二值保留/置零掩码。该版本报告掩码比全参数检查点小数千倍，并称在 0.5B 至 8B 模型上，它与全参数微调的 GRPO 差距随模型规模单调缩小。

**「实际影响」** 如果结论可复现，做持续学习与多任务迭代的团队可以只保存和分发极小的掩码文件，而不必为每个新任务保留一份完整权重，从而降低存储与部署成本，并在后续训练中减少对旧能力的覆盖。不过该方法目前只验证了 gate projection 上的二值掩码，且效果对比来自作者自己的实验，实际采用前需要在自己的模型与任务上复现；仓库与掩码已公开，可供检验。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://openreview.net/forum?id=JnfolztAV3">The Surprising Effectiveness of Deleting Weights in LLM ...</a></li>

</ul>
</details>

**标签**: `#LLM fine-tuning`, `#sparse masks`, `#continual learning`, `#reinforcement learning`, `#model efficiency`

---

<a id="item-tech-news-5"></a>
### [评论：智能家居设备应能脱离互联网独立运行](https://docodethatmatters.com/home-automation-overnight-success/) ⭐️ 7.0/10

一篇发表在 docodethatmatters.com 的观点文章主张，智能家居设备的核心功能应在不接入互联网的情况下照常使用，即把开关、温控等基本操作留在本地，而不是依赖厂商云端。这是一篇倡导性文章，不是产品发布、标准变更或可独立验证的测试报告，原文没有给出部署规模或实测数据。文章在 Hacker News 上引发的讨论主要围绕如何识别和挑选“本地优先”设备，而非某项新能力的落地。

hackernews · skittleson · 11月10日 15:25 · [社区讨论](https://news.ycombinator.com/item?id=50441707)

**「背景」** Home Assistant 会为各个设备集成标注“IoT Class”，用来说明通信方式：从本地推送、本地轮询，一直到云端推送、云端轮询；其中本地轮询指 Home Assistant 直接与设备通信，云端推送则依赖云端转发状态。这些分类为讨论“设备能否断网工作”提供了可比较的术语，也解释了为何本地协议和云端集成在离线可用性上差别很大。

**「影响」** 对打算长期使用的家庭，实际后果落在选型标准上：只支持 Wi-Fi 且依赖厂商云端的设备，其可用性系于厂商是否持续运营服务，而 Zigbee、Z-Wave 或可刷开源固件的设备不经过这一环节。评论者建议购买前查看 Home Assistant 为各集成标注的 IoT Class（从“本地推送”到“云端轮询”），优先选择本地级别；代价是需要自备运行 Home Assistant 的主机（如单板计算机或 NAS）并自行维护。

**「社区讨论」** 评论者之间共识多、分歧少，差别主要在门槛高低：scosman 表示自己只使用 Home Assistant 标注为“本地轮询”或更好的集成，并更偏好“本地推送”；driverdan 的规则更严格，商用设备只用 Zigbee 或 Z-Wave 这类离线协议，Wi-Fi 设备除非开源或可替换固件否则不买，且非传感器设备必须在没有 IoT 功能时也能完全使用。另有人提供了另一条路径和一份经验：reasonabl\_human 称自己买最便宜的硬件、收货后刷本地固件，并用单板计算机或 NAS 跑 Home Assistant；mountain\_peak 则提到自家约二十年前安装的 X10/Insteon 系统至今仍在本地运行，作为脱离云端仍可长期使用的个例。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://developers.home-assistant.io/docs/creating_integration_manifest/">Integration manifest | Home Assistant Developer Docs</a></li>
<li><a href="https://github.com/home-assistant/architecture/discussions/1426">The current iot class system in Home Assistant doesn&#x27;t show the full...</a></li>

</ul>
</details>

**标签**: `#smart home`, `#local-first`, `#IoT`, `#Home Assistant`, `#privacy`

---

<a id="item-tech-news-6"></a>
### [Chrome 联合 Firefox、MDN、Edge 发布 modern-web-guidance 1.0](https://github.com/GoogleChrome/modern-web-guidance) ⭐️ 7.0/10

Google Chrome 发布开源项目 modern-web-guidance 1.0，并与 Firefox、MDN 和 Edge 合作，提供 200 多篇指南（约 1.7MB），以 agent skill 和 CLI 的形式，引导编码代理在前端任务中优先使用 \`&lt;dialog&gt;\`、\`CSS.highlights\`、\`field-sizing\` 等平台原生能力，而不是继续沿用 div 加 JavaScript 的旧模式。项目方称，检索组件已从约 500MB 的原生栈缩减为约 7MB 的纯 JavaScript 包，在 CPU 上单次搜索约需 10ms；新增的 \`legacy-scan\` 用 3 万个 GitHub 仓库训练，在留出仓库上的平均精确率为 92%，用于找出可以改用现代写法的旧写法。官方自述的评测覆盖 200 个任务、约 1700 条 Playwright/AST 断言，codex、claude、agy 的通过率从无技能时的 55% 升至启用后的 92%，但这是项目方公布的内部结果，并非独立验证。用户可以通过 \`npx modern-web-guidance@latest install\`、\`search\` 和 \`legacy-scan\` 使用，示例命令设置了 \`DISABLE\_TELEMETRY=1\`。

hackernews · paulirish · 11月10日 18:01 · [社区讨论](https://news.ycombinator.com/item?id=50443812)

**「背景」** 所谓 agent skill，是随编码 agent 一起安装、在识别到相关前端任务时按需加载的一组说明文档，用来补上模型训练数据里缺的领域知识；这个项目还附带一个本地检索 CLI，让 agent 不必把全部内容塞进上下文。发起者指出，模型往往能说出 \`&lt;dialog&gt;\`、\`field-sizing\` 这类 API 的名字，但写代码时仍默认回到 \`&lt;div&gt;\` 加 JavaScript 的旧模式，所以才需要用外部指南把默认选择推向平台原生方案。

**「采用前需核对浏览器支持范围」** 对使用该技能的团队来说，最直接的后果是：在合并代理生成的代码前，需要逐条核对目标浏览器的支持情况。项目自称与 Firefox、Edge 合作，且只推荐 Safari 也支持的最佳实践，但评论者 surround 列出 CSS @function、calc-size\(\)、corner-shape、container scroll-state 查询、scrollsnapchange 事件等一批仅在 Chrome 稳定、Firefox 与 Safari 尚未支持的条目。实际流程上，团队可以先用 legacy-scan 扫描 ./src 找出旧模式，再按需确认兼容性后替换。

**「社区讨论」** 评论者 surround 列举了指南会建议使用、但在 Chrome 稳定、Firefox 和 Safari 尚未支持的特性，包括 CSS \`@function\`、\`calc-size\(\)\`、\`corner-shape\`、容器滚动状态查询和 \`scrollsnapchange\` 事件等；advisedwang 认为这会进一步集中 Chrome 在 Web 标准上的话语权，甚至可能回到“请用某浏览器查看”的局面。simonw 建议在 GitHub Pages 上额外发布可供 grep 的 Markdown 索引，让用户无需安装即可查询，SoftTalker 则提醒网站应保持简单，少用特性以减少日后被弃用时的迁移负担。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://news.ycombinator.com/item?id=50443812">Show HN: Get your coding agent off ~2019 JavaScript, onto modern ...</a></li>

</ul>
</details>

**标签**: `#coding agents`, `#web platform`, `#browser APIs`, `#developer tooling`, `#open source`

---