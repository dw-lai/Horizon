---
layout: default
title: "Horizon Summary: 2026-11-12 (ZH)"
date: 2026-11-12
lang: zh
---

> 从 59 条内容中筛选出 11 条重要资讯。

---

**科技新闻**
1. [电压毛刺解锁 CMP 170HX 的 80GB HBM 与 A100 级算力](#item-tech-news-1) ⭐️ 8.0/10
2. [AWS 发布本地服务模拟器，代码由 AI 代理用 Rust 编写](#item-tech-news-2) ⭐️ 7.0/10
3. [美联航禁止 AI 代理代旅客订票](#item-tech-news-3) ⭐️ 7.0/10
4. [Python 社区悼念《Python 之禅》作者 Tim Peters（1952–2026）](#item-tech-news-4) ⭐️ 7.0/10
5. [一次误报烟雾报警差点冲垮 Jane Street 纽约唯一数据中心](#item-tech-news-5) ⭐️ 7.0/10
6. [WSJ 头条称英伟达准备罢免黄仁勋](#item-tech-news-6) ⭐️ 7.0/10
7. [线性规划能否用于权重空间编程](#item-tech-news-7) ⭐️ 7.0/10
8. [谷歌发布 Gemini Decisions API，支持多模态判定](#item-tech-news-8) ⭐️ 7.0/10
9. [Anthropic IPO 路演视频披露四芯片训练与推理策略](#item-tech-news-9) ⭐️ 7.0/10

**财经新闻**
1. [CoreWeave 第三季度营收超预期，盘前股价涨 15%](#item-finance-news-1) ⭐️ 7.0/10
2. [Bitmine 2026 财年净亏损 63 亿美元，其中 62 亿美元来自数字资产未实现损失](#item-finance-news-2) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [电压毛刺解锁 CMP 170HX 的 80GB HBM 与 A100 级算力](https://blog.kate.land/posts/using-voltage-glitching-to-unlock-the-a100/) ⭐️ 8.0/10

一篇硬件改造记录称，8GB 版 NVIDIA CMP 170HX 矿卡实际板载约 80GB HBM，只是被熔丝关闭；作者用电压故障注入绕过熔丝锁，恢复了全部可用 SM（120–126 个，而 NVIDIA 在 A100 上出货 108 个）、NVLink 和 PCIe Gen4。按该记录，解锁后 FP16 达到 85.9 TFLOP/s，高于零售 A100 的 72.5 TFLOP/s，完整 80GB 可用于推理。该过程并非普通软改：需要改板、自制 STM32 毛刺器，每张卡耗时 1 到 48 小时，且十张卡中有一张只有 64GB 完好。

hackernews · lae · 11月11日 10:48 · [社区讨论](https://news.ycombinator.com/item?id=50451903)

**「背景」** CMP 170HX 是 NVIDIA 基于 GA100 的矿卡，TechPowerUp 列出的 8 GB 版本官方规格为 8 GB HBM2e、250 W。此前社区曾用软件方法把部分卡的内存提高到 64GB；这类禁用状态由芯片内的一次性熔丝锁定，而电压毛刺是在供电瞬间制造异常，使芯片跳过或错误读取熔丝，从而解除对 SM、显存容量或高速接口的限制。

**「实际影响」** 对持有 CMP 170HX 的改装者来说，这条路径要求改板、搭建 STM32 毛刺器并逐卡尝试 1 到 48 小时，且十张卡中有一张只恢复 64GB，意味着时间和结果都不稳定；把它当作可复制的量产解锁方案并不合适。

**「社区讨论」** 评论中有人怀疑这些熔丝并非纯粹市场分层，而可能是因为对应 A100 存在制造缺陷、只能降级为矿卡；这一说法未获证实。另有正在尝试软件解锁 80GB 的用户称两周仍未成功，并认为走熔断/电压毛刺路线风险更高。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.techpowerup.com/gpu-specs/cmp-170hx-8-gb.c3830">NVIDIA CMP 170HX 8 GB Specs | TechPowerUp GPU Database</a></li>

</ul>
</details>

**标签**: `#voltage glitching`, `#GPU hardware hacking`, `#NVIDIA A100`, `#hardware security`, `#reverse engineering`

---

<a id="item-tech-news-2"></a>
### [AWS 发布本地服务模拟器，代码由 AI 代理用 Rust 编写](https://github.com/aws/aws-emulator) ⭐️ 7.0/10

AWS 已在 GitHub 发布官方 AWS 模拟器，让开发者在本地运行其多项服务的克隆，以便测试时无需配置付费 API 密钥。项目用 Rust 编写，相关文章称其由大量自主 AI 代理开发，前三周提交达 29,684 次；目前在 macOS 和 Windows 上需要 Docker 运行。安全文档明确警告不要用它测试 IAM 策略与权限边界、资源型策略（如桶策略）、KMS 密钥策略、跨账户或跨区域访问等安全控制，并说明部分服务的 IAM 评估方式与 AWS 不同。

hackernews · super\_linear · 11月11日 18:21 · [社区讨论](https://news.ycombinator.com/item?id=50456631)

**「背景：本地云模拟器与既有替代方案」** 本地云模拟器让开发者在不连接真实云账号、也不申请付费 API key 的情况下对代码做集成测试；这类需求此前主要由 LocalStack、Floci 等第三方项目以及 Testcontainers 的对应模块满足（评论者提到了这些替代方案）。与真实服务相比，模拟器只复现 API 的形状和部分行为，保真程度取决于其实现覆盖了哪些服务与校验逻辑。

**「本地测试与安全边界」** 开发团队可用与真实 AWS 相同的 CLI 和 SDK 在本地测试几乎所有服务，且无需配置付费凭据；但官方安全说明要求不要用该模拟器验证 IAM 策略、资源策略、KMS 密钥策略或跨账户／跨区域访问，涉及这些权限控制的测试仍须在真实 AWS 上完成。macOS 和 Windows 用户目前还必须安装 Docker，无法仅靠单一二进制运行。

**「社区讨论」** 有评论者质疑该项目究竟只是演示还是会作为正式产品持续维护，并表示 Floci 配合 Testcontainers 已能满足需求，据其说法还可用于 GCP 和 Azure，不过只做了有限试用。另一部分评论则认为，正是 AI 代理让 AWS 有能力为数量庞大的服务构建模拟器，并把这看作本地云测试工具竞争加剧的信号。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://aws.amazon.com/blogs/aws/test-your-applications-against-aws-locally-with-aws-emulator/">Test your applications against AWS locally with AWS Emulator</a></li>

</ul>
</details>

**标签**: `#AWS`, `#cloud emulation`, `#AI agents`, `#open source`, `#developer tooling`

---

<a id="item-tech-news-3"></a>
### [美联航禁止 AI 代理代旅客订票](https://www.cbsnews.com/news/united-airlines-bans-ai-agents-booking-flights/) ⭐️ 7.0/10

据 CBS News 报道，美国联合航空（United Airlines）已禁止 AI 代理代替旅客预订机票，直接受影响的是使用自动化代理完成美联航订票的旅客，以及开发相关自动化工具的开发者。现有报道确认了禁令方向，但没有给出具体条款、生效日期、执行方式或处罚措施，也未说明禁令是否覆盖第三方代理、企业差旅工具或用户自建脚本。就现有信息看，尚不能确认美联航如何识别代理流量，也不能确认禁令在实际订票流程中的执行范围。

hackernews · herpderperator · 11月11日 21:24 · [社区讨论](https://news.ycombinator.com/item?id=50458900)

**「背景」** 航空公司官网的使用条款长期把自动化访问纳入管控范围：订票页面本身就依靠反机器人检测（例如 CAPTCHA）区分人工与脚本，并把购票渠道限定为官网、官方 App 和经批准的合作伙伴接口。据 One Mile at a Time 和 unite.ai 的报道，美联航这次的关键变化是把“旅客授权”与“航司许可”分开：只有通过航司安全审核的集成才能自动订票，而由未经授权的 AI 代理经手的预订可能在不另行通知的情况下被取消，常旅客权益也可能被收回。One Mile at a Time 同时指出，条款措辞较宽，可能连带影响里程票搜索类工具。

**「影响」** 对依赖 AI 代理订美联航机票的旅客和开发者来说，这条自动化订票路径已被政策禁止，相关产品需要准备人工接管或改用其他可订票渠道，否则可能无法完成美联航订单。报道未说明美联航的检测与执行方式，因此实际受阻范围仍不确定。

**「社区讨论」** 评论者对禁令能否执行及是否合理存在分歧：有人质问航司如何阻止浏览器中的计算机使用代理，并称这让自己与商户形成对抗关系；也有人认为订票涉及座位、中转等强控制需求，本就不适合完全自动化，更实际的是让代理比价、通过提供 API/MCP 的代理或旅行社完成预订。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://onemileatatime.com/news/united-airlines-bans-ai-agents-protect-customers/">United Airlines Bans “AI Agents,” Claims It’s To “Protect ...</a></li>
<li><a href="https://cellcog.ai/blog/united-airlines-ai-agents-terms/">United Airlines Bans AI Booking Agents: What the Terms Say</a></li>
<li><a href="https://www.unite.ai/united-airlines-bars-unauthorized-ai-agents-from-booking-travel/">United Airlines Bars Unauthorized AI Agents From Booking ...</a></li>

</ul>
</details>

**标签**: `#AI agents`, `#airline policy`, `#automation`, `#terms of service`, `#bot detection`

---

<a id="item-tech-news-4"></a>
### [Python 社区悼念《Python 之禅》作者 Tim Peters（1952–2026）](https://discuss.python.org/t/in-memoriam-tim-peters-1952-2026/110028) ⭐️ 7.0/10

Python 官方讨论区 discuss.python.org 出现悼念帖《In memoriam: Tim Peters \(1952–2026\)》，帖名标注的生卒年为 1952 与 2026，该帖经 Hacker News 传播后引发关注。Tim Peters 最为人熟知的身份是《Python 之禅》（The Zen of Python）的作者，这段格言至今仍随 CPython 发行，运行 \`python -c &quot;import this&quot;\` 即可打印。评论区补充了他的其他工作：把 pg 的《A Plan for Spam》一文落地为反垃圾邮件程序 SpamBayes，以及参与《Python Cookbook》第二版的写作。需要说明的是，SpamBayes、Cookbook 等具体贡献出自评论者叙述，悼念帖本身在原帖正文中并未逐条列出。

hackernews · ayhanfuat · 11月11日 07:03 · [社区讨论](https://news.ycombinator.com/item?id=50450488)

**「背景」** Tim Peters 是 Python 的长期核心开发者，以《Python 之禅》闻名；该文本被收录为 PEP 20，并作为彩蛋可通过 import this 在解释器中显示。他还设计并实现了 Timsort 排序算法，并在 Python 早期版本发布后不久就开始参与语言设计与实现讨论。

**「社区讨论」** 有评论者直接贴出 \`python -c &quot;import this&quot;\` 的完整输出，以此说明自己是通过这段随解释器分发的文字认识他的；多位资深用户回忆，他们在 comp.lang.python、python-dev 邮件列表和 bugs.python.org 上读他的帖子学习编程，并提到社区里常把他称为“Uncle Timmy”。关于 SpamBayes 的署名，评论者在 Gary Robinson 之外补充了 Robert Woodhead 的贡献，同时对 Rob Hooft 是否参与表示找不到可靠来源——这些均属评论者个人说法，彼此并未完全一致。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Zen_of_Python">Zen of Python - Wikipedia</a></li>
<li><a href="https://grokipedia.com/page/Tim_Peters_%28software_engineer%29">Tim Peters (software engineer) — Grokipedia</a></li>
<li><a href="https://discuss.python.org/t/in-memoriam-tim-peters-1952-2026/110028">In Memoriam: Tim Peters 1952–2026 - Core Development...</a></li>

</ul>
</details>

**标签**: `#Python`, `#open source community`, `#obituary`, `#software engineering`, `#programming culture`

---

<a id="item-tech-news-5"></a>
### [一次误报烟雾报警差点冲垮 Jane Street 纽约唯一数据中心](https://michael.bacarella.com/2026/11/10/false-smoke-alarm-jane-street-datacenter/) ⭐️ 7.0/10

Michael Bacarella 在 11 月 10 日的博客中复盘了 Jane Street 纽约唯一数据中心遭遇的一次误报烟雾报警。按文章叙述，警报本身是假的，但由此触发的应急处置一度接近失控，文章据此检讨了紧急断电（EPO）与消防停机流程。这是当事人视角的单方事故叙述，未附独立事故报告或第三方核实，具体时间线与设备细节仍需以原文为准。

hackernews · mbac32768 · 11月11日 16:38 · [社区讨论](https://news.ycombinator.com/item?id=50455394)

**「背景」** 数据中心通常会把烟感探测与消防、制冷系统联动；一旦发生误报，喷淋系统可能损坏带电设备，运维团队往往需要在喷淋启动前迅速切断电源。Jane Street 的这篇复盘描述的正是这样一次误报烟感事件：机房失去冷却，团队赶在喷淋启动前拔掉所有电源线。

**「对运维团队的影响」** 对自建机房的团队来说，这一事件的直接后果是要把烟感与断电、空调停机的联动边界定清楚：若烟感直接触发 EPO 或关停制冷，一次误报就会升级为整机房非计划断电；若不联动，则必须有人工确认与人员到场流程兜底。文章和讨论都没有给出统一答案，取舍仍取决于当地消防规范与机房规模。

**「评论讨论」** 有评论者（rdl）质疑该机房为何至少没有配备机房内的物理 EPO 按钮以及烟感与 EPO 的联动；另一位从事机房建设的评论者（rainbowzootsuit）则表示，他们为数据大厅编写的 Sequence of Operations 特意不在烟感报警时关停 CRAC，理由是《国际机械规范》（IMC）允许服务单一空间、风量超过 2000 cfm 的空调机组这样做，因为不会把烟雾扩散到建筑其他区域。另有评论者（hackermailman）以自身经历说明，住得离机房近的人常被默认成“紧急到场关服务器”的那个人。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://michael.bacarella.com/2026/11/10/false-smoke-alarm-jane-street-datacenter/">How a false smoke alarm almost drowned Jane Street ’s only NYC ...</a></li>

</ul>
</details>

**标签**: `#datacenter operations`, `#incident response`, `#fire safety systems`, `#infrastructure resilience`, `#Jane Street`

---

<a id="item-tech-news-6"></a>
### [WSJ 头条称英伟达准备罢免黄仁勋](https://www.wsj.com/business/nvidia-is-preparing-to-oust-nvidia-ceo-jensen-huang-30f421ad) ⭐️ 7.0/10

Hacker News 上出现一条指向《华尔街日报》的投稿，标题称英伟达正准备罢免 CEO 黄仁勋；这是所给材料中唯一明确的表层信息。材料没有附文章正文、时间表、继任安排或英伟达回应，因此无法确认该报道的具体内容，也不能把标题视为已经发生的领导层变动。

hackernews · jbredeche · 11月11日 22:31 · [社区讨论](https://news.ycombinator.com/item?id=50459703)

**「背景」** 这一说法来自《华尔街日报》一篇报道的标题，该报道称英伟达董事会正准备罢免 CEO 黄仁勋；当前条目未附报道正文，也没有董事会决议、时间表或公司回应等可核验细节。Hacker News 的讨论还提到黄仁勋与 Kimberly Powell 的婚外情以及对华销售合规问题，但这些属于评论中的未经证实说法，不能当作已确认事实。

**「社区讨论」** 评论区围绕未经证实的个人行为及对华销售指控争论黄仁勋是否应辞职，也有人强调他对 CUDA 和 GPU 通用计算的推动难以替代；这些均是评论者观点，未获所给材料证实。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.techmeme.com/261111/p44">Sources: Nvidia &#x27;s board is preparing to oust Jensen Huang and is...</a></li>
<li><a href="https://news.ycombinator.com/item?id=50459703">Nvidia Is Preparing to Oust Nvidia CEO Jensen Huang | Hacker News</a></li>

</ul>
</details>

**标签**: `#Nvidia`, `#Jensen Huang`, `#corporate governance`, `#AI hardware`, `#semiconductor industry`

---

<a id="item-tech-news-7"></a>
### [线性规划能否用于权重空间编程](https://nathan.rs/posts/weight-space-lp/) ⭐️ 7.0/10

一篇博客文章探讨了线性规划（LP）能否用于权重空间编程，即用线性约束引导神经网络权重编辑。现有材料没有提供具体方法、实验规模或可复现结果，因此这属于探索性分析，而非已展示的突破。

hackernews · emschwartz · 11月11日 12:30 · [社区讨论](https://news.ycombinator.com/item?id=50452655)

**「背景」** 线性规划是在一组线性约束下优化线性目标函数的数学方法；权重空间编程则指通用大语言模型直接读取并写入另一个神经网络的权重，而不依赖梯度下降或训练循环。此次讨论依托的具体案例是 MIT CSAIL 对 Qwen3.5-0.8B 的权重编辑：该编辑用手工调参修正“思考循环”，而相关摘要称这一搜索可被写成线性规划、约一分钟求解，并在 MATH-500、GSM8K 和 IFEval 上与原编辑持平，同时改动权重少 8 倍。

**「社区讨论」** 有评论者认为，如果把“消除某种行为、保留另一些行为”表达为线性约束，LP 可以作为权重编辑的引导工具；也有人建议在训练正则化中实现类似机制，或利用线性规划寻找稀疏权重修改，以进行权重空间蒸馏。上述内容均为讨论中的设想和建议，没有附带实验结果。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Weight-space_programming">Weight-space programming - Wikipedia</a></li>
<li><a href="https://proomt.com/item/can-a-linear-program-do-weight-space-programming-d1a13007-a589-44d0-b87e-067ea543171c">Can a Linear Program Do Weight-Space Programming? · proomt</a></li>

</ul>
</details>

**标签**: `#linear programming`, `#weight-space editing`, `#large language models`, `#model steering`, `#optimization`

---

<a id="item-tech-news-8"></a>
### [谷歌发布 Gemini Decisions API，支持多模态判定](https://simonwillison.net/2026/Nov/11/gemini-decisions-api/) ⭐️ 7.0/10

谷歌推出 Gemini Decisions API 和 Gemini Decision 1 模型，加入 Jev 与 OpenAI 已占据的判定模型类别。该 API 支持是/否、选项选择和评分标准打分三类问题，覆盖文本、图像、音频、视频和 PDF；Jev 仅支持文本和 JSON，OpenAI 支持文本与图像。定价为每百万输入 token 10 美分、输出免费，与 GPT-6 Luna 判定模型相同，Jev 则为每百万 4.2 美分。Simon Willison 用一段机器人视频测试时，模型对“有机器人”“在美国拍摄”给出约 0.923 的概率，对“有龙”“在法国拍摄”给出约 0.05 和 0.083 的概率，而非 Jev 和 OpenAI 那样的 1.0 或 0.0。

rss · Simon Willison · 11月11日 22:03

**「背景」** 决策模型 API 是一类不生成自由文本、只对“是/否”“多选”或“按评分标准打分”这类问题返回结构化答案的接口。在 Gemini Decision 1 之前，Jev 已提供仅支持文本与 JSON 的同类服务，OpenAI 的 GPT-6 Luna 决策模型则把输入扩展到文本和图像；谷歌这次是把同一套问答形式延伸到音频、视频和 PDF 等更多模态。

**「影响」** 对需要判定音频、视频或 PDF 的开发者，Gemini 可直接接收原始媒体，省去先转写或抽帧的步骤；但是/否结果以概率返回，接入现有二值判定流程时需要设置阈值并进行校准。

**标签**: `#Gemini Decisions API`, `#Google AI`, `#decision models`, `#multimodal AI`, `#API pricing`

---

<a id="item-tech-news-9"></a>
### [Anthropic IPO 路演视频披露四芯片训练与推理策略](https://simonwillison.net/2026/Nov/11/anthropic-ipo-roadshow/) ⭐️ 7.0/10

Anthropic 在 IPO 路演视频中公开了此前未披露的算力策略细节：联合创始人 Tom Brown 称，公司目前已在 AWS Trainium、Google TPU、NVIDIA GPU 和 AMD GPU 这四类芯片上训练并服务 Claude。他表示，早期押注「多芯片策略」在当时被认为不划算，因为每种芯片都需要各自定制软件栈和推理栈。他举例说，今年首次接入 AMD GPU，过去引入一个新芯片平台需要数十名工程师花费数月，这次由 Mythos 在三天内、几乎无人工干预地让 Claude 跑在 AMD 上，并移植或编写了近 100% 的 kernel。Brown 还把总算力描述为「物理产能 × 算力乘数」，称乘数会相互叠加，并预期在接近递归自我改进时 Claude 能自行发现算力乘数。这些均为路演视频中的公司说法，目前没有官方文字稿，也没有独立验证；Simon Willison 用 MacWhisper 提取了转录，并指出今年 9 月的故障复盘已经透露过只影响其 TPU 部署的 bug。

rss · Simon Willison · 11月11日 15:11

**「背景」** 多芯片路线的实际门槛不只在硬件，还在于每种芯片都需要独立的训练与推理软件栈，移植和维护成本很高，这也是 Anthropic 将其早期投入称为“非常规押注”的原因。Simon Willison 还指出，Anthropic 在 9 月的故障复盘中曾提到，部分缺陷只影响其 TPU 部署，这已经间接显露了其多芯片并行的架构。

**「影响」** 如果这些说法可以复现，最直接的后果是新增一类芯片平台的工程成本从「数十人月」降到「数天、几乎无人工干预」，这会改变依赖 Anthropic 模型的企业对硬件供应多元化和推理定价的预期。不过该细节出自 IPO 路演宣传材料，尚无第三方复现、官方技术文档或 kernel 代码佐证，使用者应把它当作待验证的声明，而不是已经证实的成本曲线。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://simonwillison.net/2026/Nov/11/anthropic-ipo-roadshow/">Anthropic&#x27;s IPO roadshow video - simonwillison.net</a></li>

</ul>
</details>

**标签**: `#Anthropic`, `#AI infrastructure`, `#IPO`, `#multi-chip strategy`, `#AI hardware`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [CoreWeave 第三季度营收超预期，盘前股价涨 15%](https://cointelegraph.com/markets/coreweave-stock-surges-pre-market-q3-revenue?utm_source=rss_feed&amp;utm_medium=rss&amp;utm_campaign=rss_partner_inbound) ⭐️ 7.0/10

CoreWeave 股价在 11 月 11 日盘前上涨 15%，此前公司公布第三季度营收为 36.6 亿美元、同比增长 168%，较分析师预期高 3.4%。

rss · Cointelegraph · 11月11日 13:02

**「背景」** CoreWeave 是一家总部位于美国新泽西州的云计算公司，主要运营面向人工智能计算的数据中心，此次财报是其作为 AI 基础设施供应商的最新季度业绩。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/CoreWeave">CoreWeave - Wikipedia</a></li>

</ul>
</details>

**标签**: `#CoreWeave`, `#earnings`, `#AI infrastructure`, `#revenue beat`, `#stock move`

---

<a id="item-finance-news-2"></a>
### [Bitmine 2026 财年净亏损 63 亿美元，其中 62 亿美元来自数字资产未实现损失](https://cointelegraph.com/news/bitmine-6b-net-loss-eth-treasury-holdings?utm_source=rss_feed&amp;utm_medium=rss&amp;utm_campaign=rss_partner_inbound) ⭐️ 7.0/10

Bitmine 在 2026 财年录得 63 亿美元净亏损，其中 62 亿美元来自数字资产未实现损失，即所持资产账面价值下降、但尚未出售。截至周日，公司持有 607 万枚 ETH，占以太币总供应量的 4.97%。

rss · Cointelegraph · 11月11日 09:58

**「背景」** Bitmine 是由 Tom Lee 掌舵、以以太币为核心储备资产的财库公司，其财年截至 2026 年 8 月 31 日；该公司所持数字资产按市价计量，因此以太币价格下跌会直接反映为账面亏损。\[tool-1-2\]

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.theblock.co/news/business/2026-11-11-bitmine-6-3-billion-net-loss-437812">Bitmine reports $6.3 billion net loss in latest fiscal year ...</a></li>

</ul>
</details>

**标签**: `#Bitmine`, `#Ether`, `#crypto treasury`, `#unrealized losses`, `#corporate earnings`

---