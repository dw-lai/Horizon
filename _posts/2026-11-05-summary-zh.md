---
layout: default
title: "Horizon Summary: 2026-11-05 (ZH)"
date: 2026-11-05
lang: zh
---

> 从 45 条内容中筛选出 9 条重要资讯。

---

**科技新闻**
1. [Moonshot AI 发布 Kimi K3.1 Pro 开放权重](#item-tech-news-1) ⭐️ 8.0/10
2. [OpenAI 称减少 Linux 内核上千条提权路径](#item-tech-news-2) ⭐️ 8.0/10
3. [AI 漏洞发现迫使组织处理技术债](#item-tech-news-3) ⭐️ 8.0/10
4. [腾讯发布开放权重模型 Hy4，并开源 HyCell 与 HyPDE](#item-tech-news-4) ⭐️ 8.0/10
5. [Anthropic 公布 LLM 可验证推理加密证明进展](#item-tech-news-5) ⭐️ 8.0/10
6. [Go 推出新 JSON API encoding/json/v2](#item-tech-news-6) ⭐️ 8.0/10
7. [AMD 预计第四季度营收首次超过英特尔](#item-tech-news-7) ⭐️ 7.0/10
8. [OpenAI 宣布计划收购 Pierre Computer Company](#item-tech-news-8) ⭐️ 7.0/10
9. [Ricursive 发布 Ripple-65B-Preview：65B 稠密开源权重模型预览](#item-tech-news-9) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Moonshot AI 发布 Kimi K3.1 Pro 开放权重](https://huggingface.co/moonshotai/Kimi-K3.1-Pro) ⭐️ 8.0/10

Moonshot AI 已在 Hugging Face 上发布 Kimi K3.1 Pro 的开放权重，相关讨论在 Hacker News 上获得约 400 分、108 条评论。由于现有材料没有提供模型卡细节、许可证条款或独立评测，目前能确认的只是权重已经公开；至于它是否真正属于“开放权重”，以及基准成绩是否经过针对性调优，社区仍存在分歧。已有第三方推理服务商在 OpenRouter 等平台托管该模型，一位评论者称 Together 的吞吐量约为 Moonshot AI 官方端点的两倍，Modal 又是 Together 的两倍，且价格相同——这属于社区观察，并非独立验证的结果。

hackernews · abrarthought · 11月4日 15:30 · [社区讨论](https://news.ycombinator.com/item?id=50366999)

**「前代 Kimi K3 的背景」** Kimi K3.1 Pro 并非从零训练：其 Hugging Face 页面称，它是在 Kimi K3 基础上通过大规模联合强化学习后训练而来，也是 K3.1 系列的首个模型。更早的 Kimi K3 是 2.8 万亿参数的开源权重多模态代理模型，采用 KDA 与 AttnRes，支持 100 万 token 上下文，因此 K3.1 Pro 可视为同一模型谱系的迭代。

**「实际影响」** 对想使用该模型的开发者而言，更现实的路径是通过 OpenRouter 等第三方推理服务调用，而不是自行部署；有评论者估计，自托管可能需要类似 8 张 B300 的节点。如果第三方服务商之间的吞吐差异确实存在，那么在同一价格下，推理成本仍有下降空间，用户值得比较不同提供商的吞吐与定价。

**「社区讨论」** 评论在热情与质疑之间明显分裂：一位评论者称在自己的测试中并未观察到“benchmaxxed”（针对基准过度调优）现象，认为这是略低于前沿、但对多数用例足够好用的开放模型；另一位则认为其表现相对 DeepSeekV4.1-Flash 提升不大，在第三方公布的内部基准上也不及 Opus5.5，因而怀疑成绩被基准优化。还有评论者直接质疑“开放权重”的定性，并强调自托管硬件成本高昂。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://huggingface.co/moonshotai/Kimi-K3.1-Pro">moonshotai/ Kimi -K 3 . 1 - Pro · Hugging Face</a></li>
<li><a href="https://github.com/MoonshotAI/Kimi-K3">GitHub - MoonshotAI/ Kimi -K3: Open Frontier Intelligence · GitHub</a></li>

</ul>
</details>

**标签**: `#open-weight models`, `#LLM release`, `#Moonshot AI`, `#model benchmarks`, `#inference providers`

---

<a id="item-tech-news-2"></a>
### [OpenAI 称减少 Linux 内核上千条提权路径](https://openai.com/index/a-thousand-fewer-paths-to-root/) ⭐️ 8.0/10

OpenAI 发布文章，称其工作减少了 Linux 内核中约一千条可通往 root 的提权路径。现有材料只有标题、简短说明和 Hacker News 讨论，没有正文，因此无法确认这些路径涉及哪些内核版本、是否已形成上游补丁，或是否经过独立复现；对 Linux 用户和维护者来说，“减少一千条”目前应视为发布方说法，而非已核实的结果。

hackernews · dangelosaurus · 11月4日 23:33 · [社区讨论](https://news.ycombinator.com/item?id=50372929)

**「背景：本地提权与自动化漏洞流水线」** 本地提权（LPE）漏洞指的是已拿到普通账户权限的攻击者，利用内核缺陷把权限提升到 root；因此这类缺陷是 Linux 主机上从「普通用户」走到「最高权限」的关键一步。据 OpenAI 2026 年 11 月 4 日的研究帖，其自主漏洞发现、利用与修补流水线在一次运行中以约 121 万美元的 API 成本复现了 1,724 个漏洞，并为其中 948 个 Linux 本地提权漏洞验证、生成了补丁。

**「影响」** 对 Linux 内核维护者和发行版而言，实际负担转向补丁审查与回移：OpenAI 称其流水线发现并验证了 948 个本地提权漏洞，并为它们生成补丁，但在这些补丁被上游接受并由发行版发布前，现有系统不会因这次发现自动修复。对多用户主机或容器环境，这意味着攻击者一旦取得普通账户，仍有大量本地提权路径需要靠及时更新来关闭。

**「社区讨论」** 评论区主要围绕内核安全的规模与系统性风险展开：有评论者称 948 个漏洞令人震惊，并追问内核是否已复杂到难以推理、问题是否出在安全模型或语言实现；也有人反问，在如此多已知和未知漏洞下，互联网和关键基础设施为何仍能运行，并追问有哪些缓解因素。文章作者在讨论中确认这是其团队的工作并邀请提问，但可见评论没有补充具体技术细节。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://openai.com/index/a-thousand-fewer-paths-to-root/">A thousand fewer paths to root - OpenAI</a></li>
<li><a href="https://cybersecuritynews.com/openai-uncovers-948-linux-kernel-vulnerabilities/">OpenAI Cyber Model Uncovers 948 Linux Kernel Privilege ...</a></li>
<li><a href="https://explainx.ai/blog/openai-linux-kernel-948-local-privilege-escalation-exploits-1-2-million-api-cost-pipeline-patch-the-planet-2026">OpenAI Linux Kernel Pipeline: 948 Root Exploits, $1.2M ...</a></li>
<li><a href="https://openai.com/index/a-thousand-fewer-paths-to-root/">A thousand fewer paths to root - OpenAI</a></li>

</ul>
</details>

**标签**: `#Linux kernel`, `#security`, `#privilege escalation`, `#AI-assisted vulnerability discovery`, `#OpenAI`

---

<a id="item-tech-news-3"></a>
### [AI 漏洞发现迫使组织处理技术债](https://spectrum.ieee.org/ai-in-cybersecurity-php2shell-vulnerability) ⭐️ 8.0/10

IEEE Spectrum 的一篇文章认为，AI 驱动的漏洞发现正在迫使组织处理长期积累的技术债，并以 PHP2Shell 漏洞为具体案例。文章讨论的重点是自动化发现如何把原本被搁置的修复工作推到台前，而不是宣布某一轮修复已经完成。Hacker News 上的讨论对此提出分歧：这究竟是在偿还旧债，还是开启持续不断、不增加功能的修复工作。

hackernews · pseudolus · 11月4日 11:52 · [社区讨论](https://news.ycombinator.com/item?id=50364336)

**「背景：PHP 2 Shell 漏洞」** 文章用一个具体案例来说明 AI 漏洞发现带来的修复压力：被称为“PHP 2 Shell”的两个严重 PHP 漏洞，编号为 CVE-2026-109618 和 CVE-2026-109619。据 Mailfence 与 Dynatrace 的说明，攻击者无需登录即可利用这两个漏洞在 Web 服务器上执行代码；PHP 团队明确表示，升级 PHP 是唯一完整的修复方式，没有任何配置项能完全缓解风险。

**「影响」** 对开发和运维团队而言，直接压力在于把更多工程时间转向漏洞修复和安全审计，而不是新增功能；依赖开源组件的组织也需要重新评估“总会有人审计”的假设。

**「社区讨论」** swatcoder 质疑这是否真的是“偿还”技术债，认为很多问题需要重构，因而可能变成强制性的、无休止的修复工作。xbmcuser 则认为开源软件长期存在“总有人审计”的安全错觉，AI 审计有望让这一承诺真正落地。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://blog.mailfence.com/php2shell-php-vulnerability-mailfence-secure/">PHP 2 Shell Vulnerability : Your Mailfence Account Is... | Mailfence Blog</a></li>
<li><a href="https://www.dynatrace.com/news/blog/cve-2026-109618-cve-2026-109619-php2shell-critical-vulnerability-what-it-is-and-what-to-do/">PHP 2 Shell : What it is and what to do | Dynatrace news</a></li>

</ul>
</details>

**标签**: `#AI cybersecurity`, `#technical debt`, `#vulnerability discovery`, `#open source security`

---

<a id="item-tech-news-4"></a>
### [腾讯发布开放权重模型 Hy4，并开源 HyCell 与 HyPDE](https://hy.tencent.ai/research/hy4) ⭐️ 8.0/10

腾讯在 Hy4 研究页面上公布了这款开放权重基础模型，页面自述其为当前最强的开放权重模型之一，同时明确承认在研究级数学、长时程编程、模型自我改进和高级视觉问答等内部基准上，与顶级闭源模型仍有明显差距。随 Hy4 一同开源的还有两个科学基础模型：用于单细胞表征的 HyCell 和用于物理场建模的 HyPDE；页面称这两个模型由 Hy4 与 Hyra 2.0 共同开发。游戏开发方面，腾讯称与互动娱乐事业群（IEG）的职业开发者合作整理训练数据并构建评测，覆盖功能实现、玩法逻辑、状态追踪和资产管线，并针对 Unreal Engine、Unity 与 Godot 做了适配，还扩展到多人游戏开发。以上能力描述均来自腾讯自己的研究页面，暂无独立的第三方评测确认。

hackernews · Philpax · 11月4日 14:11 · [社区讨论](https://news.ycombinator.com/item?id=50365780)

**「背景」** Tencent 的发布稿称 Hy4 是其最新一代大语言模型，并计划在随后几天公布模型权重和系统卡；这意味着研究页面上的“开放权重”发布仍需等待实际权重落地。页面同时说明，已开源的 HyCell（单细胞表示）和 HyPDE（物理场建模）由 Hy4 与 Hyra 2.0 共同开发。

**「部署与选型影响」** 对开发者而言，最直接的后果是部署路径：据外部报道，Hy4 采用 770B 总参数、每 token 激活 49B 的 MoE 结构，并以 Apache 2.0 许可发布标准 checkpoint 与 FP8 版本，可通过 vLLM、SGLang 自托管——许可和推理框架支持允许自建与商用部署，但这一参数量意味着自托管需要相当规模的硬件，小团队更可能转向 API。用于游戏开发时，官方称已针对 Unreal Engine、Unity 和 Godot 做适配并扩展到多人游戏逻辑，团队可在既有引擎工作流中试用；不过评论者 chriddyp 在其数据分析基准上测得 Hy4 精度处于 GPT-6.1 Sol 与 Terra 之间、但明显偏慢，每题约执行 26 次查询、个别达 64 次，选型时需权衡延迟与成本。

**「社区讨论」** 评论者 areoform 将 HyCell 与 HyPDE 的开源视为与部分美国公司限制研究用途的做法形成反差，认为这是把做科研的手段开放出来；frangonf 则赞赏页面坦承与顶级闭源模型之间的差距。chriddyp 报告称，在 Plotly 的数据分析基准上，Hy4 落在 GPT-6.1 Sol 与 GPT-6.1 Terra 之间，但运行非常慢——每题约执行 26 次查询、个别达到 64 次，并提到其中一次查询耗时约一小时。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://hy.tencent.ai/research/hy4?langVersion=en">Tencent Hy</a></li>
<li><a href="https://www.tencent.com/tencent-launches-hy4-joining-the-ranks-of-the-worlds-leading-open-source-ai-models/">Tencent Launches Hy4, Joining the Ranks of the World&#x27;s ...</a></li>
<li><a href="https://kie.ai/blog/what-is-tencent-hy4">What Is Tencent Hy 4 ? 770B MoE, 1M Context</a></li>
<li><a href="https://www.siliconflow.com/blog/tencent-hy4-preview-context-api-guide">Tencent Hy 4 Preview: 1M Context, Coding, and API Guide</a></li>

</ul>
</details>

**标签**: `#open-weight models`, `#large language models`, `#Tencent`, `#scientific machine learning`, `#game development`

---

<a id="item-tech-news-5"></a>
### [Anthropic 公布 LLM 可验证推理加密证明进展](https://www.anthropic.com/research/provable-inference) ⭐️ 8.0/10

Anthropic 公布了一项针对大语言模型推理的加密证明研究进展，目标是让请求方核验服务端实际使用的模型权重与推理结果；目前这是研究展示，不是已上线的生产服务。评论者给出了更具体但未经独立核实的数字：该方案约有 90–100 倍计算开销，客户端需下载约 6.5 MB 的承诺，之后每个请求生成一份证明，验证一份证明在 24 线程上约需 17 秒、单线程约 21 秒（含离线阶段检查），同一承诺约可用于 1600 万次请求。由于提供的材料没有原文内容，上述性能数字和归属说法均来自评论，尚不能视为 Anthropic 的官方结论或独立测量结果。

hackernews · ltononro · 11月4日 17:17 · [社区讨论](https://news.ycombinator.com/item?id=50368626)

**「背景」** 可验证推理要解决的问题是：服务方如何在不公开模型权重和内部计算的前提下，向用户证明某次输出确实由指定模型生成；零知识证明是主要技术路线之一。Anthropic 的研究页面在介绍这项工作时给出的先前基准是，VerInf 曾在 Llama 4 Maverick（400B 参数 MoE）上完成证明，但吞吐仅约 0.02 tok/s，而作为对比的 DeepProve 则以单次前向证明整段生成序列。

**「影响」** 对闭源模型的客户而言，FlashProve 提供了在不获取权重的情况下核验单次响应的路径：证明约 19 MB，验证需数秒，单张 H100 上的证明生成速度为 110 tokens/秒。部署时需为每次响应的证明传输、存储和数秒验证延迟预留预算，并将其纳入客户端或网关流程。

**「社区讨论」** 评论区的争议集中在归属和路线选择：neuwirth 称该方案大量沿用其 VerInf 工作，并在 400B Maverick 等选择上归属不足；nemo1618 则认为开放权重模型只需确定性重跑即可验证，vessenes 也提出用多家独立推理提供方做概率性交叉核验，可能比 ZKP 路线便宜得多。这些说法均来自评论者，帖文可用材料未作回应，也未提供独立验证。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.anthropic.com/research/provable-inference">Progress on provable inference for large language models \ Anthropic</a></li>
<li><a href="https://www.anthropic.com/research/provable-inference">Progress on provable inference for large language models \ Anthropic</a></li>
<li><a href="https://interestingengineering.com/ai-robotics/anthropic-flashprove-cryptographic-model-verification">Anthropic unveils cryptographic tool to verify model outputs</a></li>

</ul>
</details>

**标签**: `#provable inference`, `#LLM security`, `#zero-knowledge proofs`, `#AI verification`, `#open-weight models`

---

<a id="item-tech-news-6"></a>
### [Go 推出新 JSON API encoding/json/v2](https://go.dev/blog/jsonv2) ⭐️ 8.0/10

Go 官方博客宣布了新的 JSON API \`encoding/json/v2\`，面向 Go 开发者，尤其是现有 \`encoding/json\` 的使用者。公告将这项变动置于标准库层面，但现有材料没有给出具体版本、默认启用方式或兼容与迁移时间表。因此，现有项目是否需要改代码、新旧 API 如何并存，仍需等待更完整的官方说明。

hackernews · olexsmir · 11月4日 17:52 · [社区讨论](https://news.ycombinator.com/item?id=50369106)

**「背景」** Go 1.25 曾于 2025 年 9 月引入实验性的 encoding/json/v2 和 encoding/json/jsontext 包，用来解决原有 encoding/json 长期存在的问题，并论证了为什么需要一个新的主版本 API。据 Go 官方博客的更新说明，这两个包在收集更多反馈并经过修订后已经稳定，随 Go 1.27 正式可用；本次公告即是对当初那篇实验性介绍的更新版本。

**「社区讨论」** 有评论者认可 \`encoding/json/v2\` 的方向，但不满 \`MarshalIndent\` 被移除，认为格式化输出的等价写法复杂且不直观，会增加迁移成本。另一位开发者则分享了在实际项目中使用 \`jsontext\` 的经验：为需要细分错误信息的难缠客户端保持高性能，并称其没有反射式内省、适合非直白解析场景。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://go.dev/blog/jsonv2">A new Go API for JSON - The Go Programming Language</a></li>
<li><a href="https://go.dev/blog/jsonv2-exp">A new experimental Go API for JSON - The Go Programming Language</a></li>

</ul>
</details>

**标签**: `#Go`, `#JSON`, `#standard library`, `#API design`, `#software engineering`

---

<a id="item-tech-news-7"></a>
### [AMD 预计第四季度营收首次超过英特尔](https://www.tomshardware.com/pc-components/cpus/amd-expects-to-outsell-intel-in-q4-for-the-first-time-in-history-usd17b-guidance-would-exceed-intels-projections) ⭐️ 7.0/10

AMD 预计其第四季度营收将首次超过英特尔：公司给出的约 170 亿美元季度营收指引高于英特尔同期的预测。AMD 将增长部分归因于 Instinct 加速器产品的强劲销售。这一比较基于两家公司的业绩指引与预测，尚不代表已经实现的销售结果。

hackernews · rbanffy · 11月4日 15:38 · [社区讨论](https://news.ycombinator.com/item?id=50367125)

**「背景」** 长期以来，Intel 凭借服务器与客户端 CPU 的出货规模在季度营收上压过 AMD，因此两家公司整体营收的对比并不等同于 CPU 出货量或市场份额的对比。Instinct 是 AMD 面向数据中心的加速卡产品线，直接与 Nvidia 的 GPU 竞争，报道将 Instinct 销售列为推动增长的因素之一。需要说明的是，约 170 亿美元的 Q4 数字来自公司指引，是对尚未结束季度的预测，而非已公布的财报结果。

**「对数据中心采购的影响」** 对计划在 2027 年部署 AI 算力的数据中心买家而言，AMD 的指引显示其数据中心业务收入将从 2026 年第三季度的 85.5 亿美元增至第四季度约 128 亿美元，增量主要由 Instinct MI455X 加速器和 Helios 机架级系统放量推动，这意味着 AMD 将首次以规模化机架级供应商的身份进入采购选项。不过这只是公司指引而非已交付结果：约 170 亿美元（±3%）的季度营收目标能否兑现，取决于 MI455X 与 Helios 的产能爬坡执行情况。

**「社区讨论」** 有评论者认为，这一预测更多反映英特尔自身的失误，而非 AMD 在 AI 领域的突破；也有人指出 AMD 的增长主要来自 Instinct 加速器，但其规模仍远小于英伟达，并质疑 x86 架构的长期前景。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.tomshardware.com/pc-components/cpus/amd-expects-to-outsell-intel-in-q4-for-the-first-time-in-history-usd17b-guidance-would-exceed-intels-projections">AMD expects to outsell Intel in Q 4 for the first time in... | Tom&#x27;s Hardwar...</a></li>
<li><a href="https://www.techpowerup.com/354470/amd-guidance-points-to-its-first-quarter-ever-with-more-revenue-than-intel">AMD Guidance Points to Its First Quarter Ever With More Revenue ...</a></li>

</ul>
</details>

**标签**: `#AMD`, `#Intel`, `#CPU market`, `#semiconductors`, `#AI accelerators`

---

<a id="item-tech-news-8"></a>
### [OpenAI 宣布计划收购 Pierre Computer Company](https://openai.com/index/openai-to-acquire-pierre/) ⭐️ 7.0/10

OpenAI 于 11 月 4 日宣布计划收购 Pierre Computer Company，但交易金额、具体条款和完成时间均未披露，因此目前只是收购意向，而非已完成交易。HN 讨论引述其产品介绍称，Pierre 的 Code.Storage 以 Git 为基础，为 Lovable、Bolt、Amp 等客户存储大规模 agent 生成的代码和持续变化的产品文件。讨论还将这笔收购与 OpenAI 此前关于大规模 Git 的工程文章联系起来，但公告本身没有说明 OpenAI 将如何整合 Pierre 的技术或团队。

hackernews · itunpredictable · 11月4日 15:21 · [社区讨论](https://news.ycombinator.com/item?id=50366863)

**「背景：Pierre 与 Code Storage」** 据 The Verge 报道，OpenAI 在宣布这笔交易前已将 Pierre 的部分工具整合进 Codex，而 Codex 是 OpenAI 的 AI 编程平台。Pierre 的 Code Storage 提供基于 Git、面向大规模智能体工作负载的基础设施，用于存储代码和其他机器生成产物。

**「影响」** OpenAI 计划在 Pierre 的 Git 工作流上继续构建，而 Codex 应用的文件浏览和变更审查已经使用 Pierre 的 Trees、Diffs 库；依赖这些开源库的开发者应关注交易完成后的维护、许可和版本安排。对使用 Code Storage 存放智能体生成代码和制品的团队，现有公开信息未给出价格和交割安排，也未说明 API 与服务条款是否会调整。

**「社区讨论」** 评论者主要从战略契合度解读这笔交易：有人把它与 OpenAI 的 Git 扩展问题及其编码代理工作流相连，并称 Mitchell Hashimoto 是 Pierre 的公开支持者，且可能是投资者；也有人引述 Code.Storage 的客户名单，强调它在大规模机器生成代码存储中的使用。另有评论提出，大实验室收购成功开发者产品的团队，可能同时是在获取这些产品如何被打造出来的经验数据。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.theverge.com/openai">OpenAI | The Verge</a></li>
<li><a href="https://code.storage/">Code Storage — Git Infrastructure at Scale by The Pierre Computer ...</a></li>
<li><a href="https://code.storage/">Code Storage — Git Infrastructure at Scale by The Pierre ...</a></li>
<li><a href="https://openai.com/index/openai-to-acquire-pierre/">OpenAI to acquire Pierre Computer Company, Inc.</a></li>
<li><a href="https://cellcog.ai/blog/openai-acquires-pierre/">OpenAI to Acquire Pierre: Code Storage Comes to Codex</a></li>

</ul>
</details>

**标签**: `#OpenAI`, `#acquisitions`, `#developer tools`, `#Git infrastructure`, `#AI coding`

---

<a id="item-tech-news-9"></a>
### [Ricursive 发布 Ripple-65B-Preview：65B 稠密开源权重模型预览](https://www.reddit.com/r/LocalLLaMA/comments/1xo2arv/ricursive_intelligence_ripple65bpreview_new_dense/) ⭐️ 7.0/10

Reddit 用户 /u/returnity 发帖称，Ricursive Intelligence（与 Flint 的开发方 Recursive 无关）放出了稠密 65B 开源权重模型 Ripple-65B-Preview 的预览版，并给出了与 Muse Spark Open（816B）、Reflection 的 Beam（501B）互有胜负的基准对比。帖子列出的设计包括 4:1 的滑动窗口与全局注意力比例、80 层 × 5120 维的“窄而深”结构、FFN 激活裁剪、门控注意力、全局 NoPE 与 value residuals，另有一个未经 midtraining、也没用合成 QA 数据的纯预训练检查点，以及 DFlash2 草稿模型。按帖中引述，官方训练流程为 midtraining、长上下文、SFT、长上下文 SFT 与混合领域 RL，而预览版只做了“较轻的后训练”，侧重 agentic coding。作者同时贴出与 Qwen 系列的对比（Terminal-Bench 2.1 为 80.5 对 73.0，SWE-bench Pro 为 61.4 对 61.7 和 62.5，GPQA Diamond 为 85.2 对 89.2 和 91.7），并给出 AtomicChat 的 GGUF 量化大小（Q8\_0 68.8 GB、Q4\_K\_M 38.8 GB）以及在 llama.cpp 上打补丁编译的方法。需要注意，以上均为单一社区帖子的说法，基准成绩与训练细节尚未经独立验证，帖内也自述发布方对训练的表述存在不一致之处。

reddit · r/LocalLLaMA · /u/returnity · 11月4日 22:42

**「背景」** Ripple-65B-Preview 由 Ricursive Intelligence 发布，官方介绍称它是驱动其 AI 芯片设计平台的专有模型的通用版本，预训练使用了 12 万亿 token，并支持最长 1M 上下文（这一说法来自厂商页面，尚未经独立验证）。与当前美国开源权重前沿常见的超大规模模型不同，帖中拿来对标的 Muse Spark Open 为 816B、Reflection Beam 为 501B，而“稠密（dense）”意味着每个 token 都要走完全部参数，因此本地与开源社区此前一直在等待一个 70B 级别的稠密选择。官方模型卡也说明，其基准比较对象是当前可获得的美国开源权重前沿模型，并以完整 BF16 精度测试，这些对比同样属于厂商自报结果。

**「本地部署仍需自行打补丁」** 想在本地跑这个模型的用户暂时无法直接用上游 llama.cpp：需要克隆仓库、切到 commit 9e2a04a、应用 ricursive-port.patch 再自行编译，上游对应的支持目前只是一个 feature request（issue \#31691）。量化权重由 AtomicChat 提供（tool-3-1），其中 Q4\_K\_M 为 38.8 GB、Q8\_0 为 68.8 GB，前者意味着实际运行需要 40 GB 级别的显存或统一内存来容纳权重。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.ricursive.com/ripple">Recursive Self-Improvement via AI for Chip... - Ricursive Intelligence</a></li>
<li><a href="https://huggingface.co/ricursiveAI/Ripple-65B-Preview">ricursiveAI/ Ripple - 65 B - Preview · Hugging Face</a></li>
<li><a href="https://huggingface.co/AtomicChat/Ripple-65B-Preview-GGUF">AtomicChat/Ripple-65B-Preview-GGUF · Hugging Face</a></li>
<li><a href="https://github.com/ggml-org/llama.cpp/issues/31691">Feature Request: ricursiveAI/Ripple-65B-Preview support - GitHub</a></li>

</ul>
</details>

**标签**: `#open-weight models`, `#dense LLMs`, `#LLM architecture`, `#benchmarks`, `#local LLMs`

---