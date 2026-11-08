---
layout: default
title: "Horizon Summary: 2026-11-08 (ZH)"
date: 2026-11-08
lang: zh
---

> 从 29 条内容中筛选出 7 条重要资讯。

---

**科技新闻**
1. [MaxxBench 质疑 DeepSWE 高分：扰动任务规格后分数大幅波动](#item-tech-news-1) ⭐️ 8.0/10
2. [微软研究院 AI Frontiers 小组据报解散](#item-tech-news-2) ⭐️ 7.0/10
3. [《极品飞车：地下狂飙 2》浏览器多人版可玩](#item-tech-news-3) ⭐️ 7.0/10
4. [Asahi Linux 7.3 进展报告：Fedora Asahi Remix 实现同日发布](#item-tech-news-4) ⭐️ 7.0/10
5. [Coldframe：伪装冷柜控制器的 Python 蜜罐](#item-tech-news-5) ⭐️ 7.0/10
6. [调查称 Mac 内置未公开的家庭成员分类器](#item-tech-news-6) ⭐️ 7.0/10
7. [Qwen3.8 27B KV 缓存量化：8 位近乎无损](#item-tech-news-7) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [MaxxBench 质疑 DeepSWE 高分：扰动任务规格后分数大幅波动](https://maxxbench.unlap.ai/research/why-maxxbench/) ⭐️ 8.0/10

MaxxBench 发布了一项针对 DeepSWE 编程基准的分析，做法是对任务规格做扰动，再观察分数变化，以此检验高分是否对应真实能力。结果显示分数会随规格扰动而明显变化，规模较小的模型退化最严重，而且 DeepSWE 基准本身似乎存在若干 bug。对于依据 DeepSWE 分数挑选模型或评估编程 agent 的开发者来说，这意味着单一榜单分数不宜直接当作能力结论。该分析发布在 maxxbench.unlap.ai，属自出版研究而非同行评审结果，其结论应理解为对基准有效性的质疑，而非对具体模型能力的最终判定。

hackernews · antiuniverse · 11月7日 17:19 · [社区讨论](https://news.ycombinator.com/item?id=50406222)

**「背景」** DeepSWE 是一个面向编码智能体的长周期软件工程基准，其任务从零编写，旨在避免数据污染。MaxxBench 围绕这一基准的得分是否稳健展开检验。

**「对选型决策的影响」** 对靠 DeepSWE 分数挑编码智能体的团队来说，最直接的后果是单一分数不足以支撑选型：MaxxBench 通过改动任务规格让模型重跑，分数出现明显波动，并且参数量较小的模型下滑最多；而 DeepSWE 定位是对前沿编码智能体做长周期软件工程评测，一旦把它当作横向比较的唯一依据，就可能把在任务表述轻微变化下表现不稳的模型排到前面。可行的做法是在采纳某个“最高分”配置前先做同类扰动复测，观察分数是否保持，再决定是否将其纳入生产流程。

**「社区讨论」** 评论者认为“改动一个参数、看分数变化多少”这种一阶检验简单且有效，并指出结果图中规模较小的模型分数下滑最严重；但也有人提醒 GLM-5.3 与 GLM-5.3-flash 属于不同谱系，不能按同一模式解读。另有评论表示，DeepSWE 存在 bug 让其对基准更加怀疑，并把“不要用 max 模式”视为最实际的结论；还有人认为问题更多出在实验室构建的 RL 环境缺乏变化，使小模型对这类简化任务过拟合，而非直接针对基准训练。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://deepswe.datacurve.ai/">DeepSWE measures frontier coding agents on original, long-horizon...</a></li>
<li><a href="https://deepswe.net/">DeepSWE Benchmark : GPT vs Claude for Agentic Coding</a></li>

</ul>
</details>

**标签**: `#benchmarks`, `#llm-evaluation`, `#coding-agents`, `#benchmark-robustness`, `#ai-research`

---

<a id="item-tech-news-2"></a>
### [微软研究院 AI Frontiers 小组据报解散](https://hunch.net/?p=13764006) ⭐️ 7.0/10

Hacker News 上的一则提交链接到报道，称微软研究院（Microsoft Research）已结束其 AI Frontiers 小组，研究员 John Langford 同时离职。该提交本身只包含存档和报道链接，没有报道正文，因此小组的具体研究范围、结束时间及人员安置无法从现有材料核实。

hackernews · srean · 11月7日 18:02 · [社区讨论](https://news.ycombinator.com/item?id=50406563)

**「背景」** AI Frontiers 是微软研究院于 2023 年 ChatGPT 发布后成立的约 50 人研究团队，产出包括用于协调多智能体的 AutoGen 框架和可操作计算机执行任务的智能体 Fara，部分成员还探索不依赖单纯扩大模型规模的改进方法。据媒体报道，该团队负责人 John Langford 此次离职与微软 AI 部门优先扩展规模的研究路线分歧有关，内部 AI 团队正更多嵌入产品部门而非独立研究单位。

**「影响」** 若报道属实，最直接受影响的是该小组研究人员和依赖其公开成果的外部合作者：探索性 AI 研究少了一个由企业研究机构支持的载体，而现有材料没有说明人员是否转岗、项目是否迁移，或论文与开源工作是否继续。

**「社区讨论」** 评论者多把此事解读为大型公司减少探索性 AI 研究、优先 transformer 规模化迭代的又一信号。也有评论指出标题易被误读为“AI 前沿的终结”，强调被解散的只是名为 AI Frontiers 的研究组，并认为研究与规模化不应互相挤压。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://emergent.sh/news/john-langford-exits-microsoft-ai-frontiers">John Langford Exits Microsoft as AI Frontiers Group Closes</a></li>
<li><a href="https://www.indiatoday.in/technology/news/story/microsoft-ai-research-clash-john-langford-quits-declares-ai-frontiers-over-3034334-2026-11-07">Microsoft AI research clash: John Langford quits, declares AI ...</a></li>
<li><a href="https://daily.dev/posts/microsoft-researcher-john-langford-exits-ai-frontiers-group-declared-finished-t8nprypt6">Microsoft Researcher John Langford Exits. AI Frontiers Group ...</a></li>

</ul>
</details>

**标签**: `#AI research`, `#Microsoft Research`, `#industry trends`, `#research funding`, `#Hacker News discussion`

---

<a id="item-tech-news-3"></a>
### [《极品飞车：地下狂飙 2》浏览器多人版可玩](https://nfsu2.xyz/) ⭐️ 7.0/10

一个名为 nfsu2.xyz 的浏览器版《极品飞车：地下狂飙 2》项目在 Hacker News 上引发关注；该项目被描述为通过逆向工程和 WebGPU 实现，玩家可直接在浏览器中进入支持多人联机的游戏。当前公开的是一个可玩网站，而非技术说明，项目的授权与法律状态尚不明确。社区评论称可在手机上游玩并与朋友联机，但 Linux 上的 Chromium 需要启用不安全的 WebGPU 特性才能运行。

hackernews · fluxusars · 11月7日 09:36 · [社区讨论](https://news.ycombinator.com/item?id=50403052)

**「背景」** 《极品飞车：地下狂飙 2》原是一款商业发行的竞速游戏；社区评论提到，它已不再通过官方渠道销售，原版在现代 PC 上也存在兼容性问题。这个浏览器版本通过逆向工程还原游戏，并借助 WebGPU 在网页中调用 GPU 渲染，才使无需安装客户端即可多人游玩成为可能。

**「实际影响」** 对想尝试的玩家来说，这是一个与 EA 无关的独立粉丝项目，页面自述未获 Electronic Arts 授权或认可；而“abandonware（弃置软件）”在法律上并不构成一种正式状态，因此该站点能否长期在线并无保障，不宜当作稳定的游玩途径。评论者还提到，Linux 上的 Chromium 需要开启不安全的 WebGPU 特性（unsafe WebGPU）才能运行该页面，也就是说部分用户需自行调整浏览器启动参数后才能进入游戏。

**「社区讨论」** 有玩家报告已在手机上游玩，并有人与朋友完成多人比赛，认为体验令人惊讶；同时有人质疑该项目涉及版权内容却接受捐赠，并担心站点走红后会被下架。Linux 用户还报告需在 Chromium 中启用不安全的 WebGPU 特性才能运行。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://thegametake.com/guides/need-for-speed-browser">Need for Speed Browser Ports: Fan Projects, Legal Notes ...</a></li>
<li><a href="https://thelegalguide.org/is-abandonware-legal-understanding-software-ownership-rights/">Is Abandonware Legal? Understanding Software Ownership and ...</a></li>

</ul>
</details>

**标签**: `#browser-based gaming`, `#WebGPU`, `#game preservation`, `#reverse engineering`, `#multiplayer`

---

<a id="item-tech-news-4"></a>
### [Asahi Linux 7.3 进展报告：Fedora Asahi Remix 实现同日发布](https://asahilinux.org/2026/11/progress-report-7-3/) ⭐️ 7.0/10

据 Asahi Linux 7.3 进展报告，Fedora Linux 45 于 11 月 3 日发布当天，Fedora Asahi Remix 也同步推出；项目称这是首次让新版 Fedora Asahi Remix 与上游 Fedora 同日发布。对在 Apple Silicon Mac 上使用 Fedora 的用户来说，这减少了等待移植版本的时间。现有材料还提到项目对宽松许可证被利用的担忧，但未说明具体的许可变更或时间表。

hackernews · ackyshake · 11月7日 05:20 · [社区讨论](https://news.ycombinator.com/item?id=50401867)

**「背景」** Fedora Asahi Remix 是 Asahi Linux 项目面向 Apple Silicon Mac 提供的 Fedora 发行版。Asahi Linux 的 7.3 进度报告称，Fedora Linux 45 于 11 月 3 日发布，而该 Remix 首次做到与上游 Fedora 同日发布，这为理解本次更新中的发布节奏提供了背景。

**「影响」** 对 Apple Silicon 上的 Fedora 用户来说，Fedora Asahi Remix 已能随 Fedora Linux 45 同日发布，这是首次做到与上游同日；因此新装或升级时可直接获得同日发布的 Fedora 版本，而不必等待 Remix 追赶。

**「社区讨论」** 有评论者表示，USB-C 外接显示器支持仍是其不愿安装 Asahi Linux 的主要障碍，并质疑项目为何优先支持更新的 CPU；也有人讨论项目对宽松许可证被商业利用的担忧。另有开发者借机介绍自己的 Gravity Linux 项目，称已支持 Vulkan 1.4 并推进 M4/M5 与休眠支持，但这些说法未在给定材料中独立验证。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://asahilinux.org/2026/11/progress-report-7-3/">Progress Report: Linux 7.3 - Asahi Linux</a></li>
<li><a href="https://asahilinux.org/2026/11/progress-report-7-3/">Progress Report: Linux 7.3 - Asahi Linux</a></li>

</ul>
</details>

**标签**: `#Asahi Linux`, `#Apple Silicon`, `#Linux`, `#Fedora`, `#open source`

---

<a id="item-tech-news-5"></a>
### [Coldframe：伪装冷柜控制器的 Python 蜜罐](https://github.com/hedgerow-dev/coldframe) ⭐️ 7.0/10

作者发布了 Coldframe：一个伪装成 Danfoss AK-SM 800A 和 Dixell XWEB 超市制冷控制器的蜜罐，主体为单个仅用 Python 标准库实现的文件。项目称其依据 Shodan 上真实设备的记录匹配 HTTP 头顺序、页面标题、证书字段和 TLS 版本，使两种伪装不被 Shodan 标为蜜罐；它还能识别 CVE-2025-41450 等 Danfoss 登录绕过和 XWEB 漏洞尝试，并记录“当日代码”是否正确。默认口令登录后会进入带除霜按钮的假门店仪表盘，以便观察攻击者的后续动作。作者称两个实例已上线一天，目前只看到通用扫描器和 Shodan 爬虫 refrigerator.census.shodan.io，尚无真实攻击数据或独立验证。

hackernews · hedgerow-dev · 11月7日 17:27 · [社区讨论](https://news.ycombinator.com/item?id=50406292)

**「背景」** Danfoss AK-SM 800A 通过嵌入式 Web 管理界面提供管理功能，攻击面正来自这些页面和登录流程。Danfoss 在 2025 年 3 月的安全公告中确认 AK-SM8xxA 系列存在认证绕过，并给出 4.2 版补丁；Claroty 对 AK-SM 800A Web 管理界面的研究也列出了多处相关漏洞。

**「对运营方的实际意义」** 对超市与制冷设备安装商而言，真正的暴露点在于管理界面本身：据 Zscaler 2026 年 8 月的分析，Danfoss AK-SM 800A 与 Copeland XWEB Pro 的固件修复已发布数月，仍有数千个管理接口可从公网直接访问，因此仅靠打补丁并不能消除风险，还需把控制器置于 VPN 或访问控制之后。Coldframe 为防御方提供了一种低成本方式来观察这类暴露接口上到底会发生什么，但作者称两个实例上线一天只看到通用扫描器和 Shodan 爬虫，尚未捕获针对性利用，目前还不能用它验证攻击是否真实发生；Cato Networks 也指出相关漏洞在已报告攻击中的实际利用尚未得到确认。

**「社区讨论」** 评论区中，supriyo-biswas 对用 Shodan 数据校准蜜罐表示怀疑，认为网上许多同类设备本身就是蜜罐或已被入侵，建议先取得真实漏洞设备进行探测；作者则回应称超市通常没有安全团队，补丁、VPN 和强口令需要由厂商或安装商默认提供。另有评论者 xrd 追问，大规模冷柜故障究竟是否已被确认为黑客攻击，而不是同一时间推送软件更新造成的现象。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.danfoss.com/en/service-and-support/coordinated-vulnerability-disclosure/danfoss-security-advisories/dsa-2025-03-01/">DSA-2025-03-01 | Danfoss</a></li>
<li><a href="https://claroty.com/team82/research/freeze-the-controller-defrost-the-food-uncovering-vulnerabilities-in-danfoss-refrigeration-controllers">Freeze the Controller, Defrost the Food: Uncovering ...</a></li>
<li><a href="https://www.zscaler.com/blogs/product-insights/fix-has-been-out-year-controller-still-exposed">Cold Chain OT Security: Refrigeration Controllers | Zscaler</a></li>
<li><a href="https://www.catonetworks.com/blog/cato-ctrl-threat-brief-attacks-against-refrigeration-controllers/">Attacks Against Refrigeration Controllers | Cato Networks</a></li>

</ul>
</details>

**标签**: `#honeypots`, `#IoT security`, `#OT security`, `#vulnerability research`, `#Python`

---

<a id="item-tech-news-6"></a>
### [调查称 Mac 内置未公开的家庭成员分类器](https://8rank.ai/game/apple-intelligence-personal-knowledge-graph) ⭐️ 7.0/10

一篇调查文章及其 Hacker News 讨论称，苹果在 Mac 上运行未公开的系统，用来构建个人知识图谱并判断用户与家庭成员、熟人之间的关系；文章称相关守护进程自 2022 年起随 Mac 提供，但这些说法尚未得到独立验证。讨论的核心不是已发布功能，而是这类本地关系数据是否应被明确告知、用户能否有效同意，以及它是否符合人们对隐私的预期。由于没有可用的原文内容，具体数据来源、存储位置、保留期限和关闭方式均无法从现有材料确认。

hackernews · infwhispers · 11月7日 09:46 · [社区讨论](https://news.ycombinator.com/item?id=50403097)

**「背景」** 这篇文章所说的“个人知识图谱”，指系统在本地建立人物、关系与互动上下文的数据层；文章称相关守护进程自 2022 年起随 macOS 提供，涉及 macOS 13 及以上的 Intel 和 Apple 芯片 Mac。

**「影响」** 若调查成立，受影响的是 2022 年以来的 Mac 用户：人物关系推断在设备本地进行，并不自动等同于用户已充分知情；未公开的处理流程会削弱用户判断数据用途和同意范围的能力。苹果是否提供逐项开关、删除入口或面向开发者的说明，现有材料无法确认。

**「社区讨论」** 评论中的张力在于用途与边界：aetherspawn 认为这类上下文可帮助 Siri 或本地模型区分“哪个 James”、理解“老板”等称呼，thomascountz 则担忧持续记录会破坏人际交流中“不必全部记住”的社会默契。elgertam 表示并不意外，因为 Photos 已能识别人脸和宠物；consumer451 引用乔布斯关于隐私必须明确告知的旧言论表达质疑。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://8rank.ai/game/apple-intelligence-personal-knowledge-graph">Anatomy of Apple &#x27;s Personal Knowledge Graph — Eighth Rank</a></li>

</ul>
</details>

**标签**: `#Apple`, `#macOS`, `#privacy`, `#personal knowledge graph`, `#AI`

---

<a id="item-tech-news-7"></a>
### [Qwen3.8 27B KV 缓存量化：8 位近乎无损](https://www.reddit.com/r/LocalLLaMA/comments/1xqbesv/effects_of_kv_cache_quantization_on_qwen38_27b/) ⭐️ 7.0/10

一项针对 Qwen3.8 27B 的社区 KLD 基准测试，覆盖 llama.cpp、ExLlamaV3 和 vLLM 中的 35 个权重与检查点量化，并将上下文延伸至 64k token，对比 16 位、8 位及部分 4 位 KV 缓存相对 bf16 参考模型的输出分布偏移。结果显示，在 llama.cpp（q8\_0）和 ExLlamaV3 中使用 8 位 KV 缓存可将缓存大小减半，KLD 变化低于 0.00012，基本落在数值噪声范围内；vLLM 的 FP8 缓存则让每个检查点的 KLD 增加约 0.0004–0.0006，仍然很小。4 位缓存的影响明显更大：llama.cpp 的 q4\_0 增加约 0.0016–0.0027 KLD，对高精度权重量化的相对损害更大，且这种损失在 16–32k 上下文中比前 4k token 高约 15–30%，因此作者不推荐使用 4 位 KV 缓存。

reddit · r/LocalLLaMA · /u/Hefty\_Wolverine\_553 · 11月7日 17:09

**「背景」** 在自回归推理中，KV 缓存保存已处理 token 的注意力键和值，避免每生成一个 token 都重新计算；量化该缓存能明显降低显存占用，但可能改变模型输出的下一 token 概率分布。KL 散度（KLD）用于衡量量化模型相对 bf16 全精度参考模型的输出分布偏移，0 表示分布未变。该测试沿用作者此前 Qwen3.6 基准的 KLD 方法，并以 bf16 模型作为参考。

**「影响」** 对显存受限的用户，最直接的选择是启用 8 位 KV 缓存：按文中 64k 上下文估算，缓存从约 4.00 GiB 降到 2.00–2.13 GiB，而 llama.cpp 和 ExLlamaV3 的 KLD 变化低于 0.00012；但若权重本身已是 Q8\_0，4 位缓存会把 KLD 从 0.0007 推高到 0.0034，反而差于使用 16 位缓存的 UD-Q5\_K\_XL，因此应优先保留 8 位或 16 位缓存。

**标签**: `#KV cache quantization`, `#LLM inference`, `#llama.cpp`, `#ExLlamaV3`, `#vLLM`

---