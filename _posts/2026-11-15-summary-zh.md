---
layout: default
title: "Horizon Summary: 2026-11-15 (ZH)"
date: 2026-11-15
lang: zh
---

> 从 28 条内容中筛选出 4 条重要资讯。

---

**科技新闻**
1. [Lovable 应用因 RLS 不足暴露护照与逾 20 万条私信](#item-tech-news-1) ⭐️ 8.0/10
2. [Project Zero 漏洞披露期缩短至 90 天](#item-tech-news-2) ⭐️ 8.0/10
3. [EFF 再批科技公司试图重塑隐私概念](#item-tech-news-3) ⭐️ 7.0/10
4. [tiny-voca：4.5M 参数全开源 TTS，CPU 上 70 倍实时](#item-tech-news-4) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Lovable 应用因 RLS 不足暴露护照与逾 20 万条私信](https://www.crissyfield.de/research/lovable-en/) ⭐️ 8.0/10

一份安全研究报告称，部分由 Lovable 构建的应用因行级安全（RLS）配置不足，暴露了用户的护照信息和超过 20 万条私密消息。Lovable 安全负责人回应称，这些应用的根因正是 RLS 不足，并称平台会在发布前自动扫描每个应用，还提供免费的深度静态应用安全测试（SAST）扫描以及“修复”和自动修复选项。相关讨论将矛头指向 AI 生成应用的不安全默认设置，但上述暴露规模来自该研究报告，所给材料未提供独立核实。

hackernews · armcat · 11月14日 17:43 · [社区讨论](https://news.ycombinator.com/item?id=50499017)

**「背景」** 行级安全（RLS）是 PostgreSQL 和 Supabase 用来按行限制数据库读写权限的机制；Supabase 文档说明，项目的默认权限会随创建时间及 Data API 设置不同，因此旧项目未必自动获得更严格配置。对由 AI 生成并直接连接 Supabase 的应用来说，若表未启用 RLS 或策略过宽，客户端请求就可能绕过前端界面直接读取数据，这正是此次数据暴露事件的技术前提。

**「影响」** 对使用 Lovable 发布应用的开发者而言，这次扫描显示的现实后果是：若数据库未启用足够的行级安全（RLS），护照号、支付信息、论坛资料和私聊消息就可能在无需登录的情况下被读取（扫描覆盖近 16 万个应用，发现超过 20 万条私聊消息和逾 1000 条含护照号码的身份记录）。开发者应把未认证访问测试纳入发布流程，审计现有项目的 RLS 策略，并自行验证默认配置是否真正阻止了匿名读取。

**「社区讨论」** 评论中，SOLAR\_FIELDS 认为 Supabase 也难辞其咎：其称相关默认设置据称已于 10 月 30 日修复，但有报告称现有项目仍沿用旧默认值。liquid\_thyme 主张平台应采用默认拒绝的数据库、最小权限 API 和自动化认证测试等更安全的默认设置；Oras 则指出，这类 AI 生成应用数量多、攻击门槛低，普通用户往往不知道风险。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://supabase.com/docs/guides/api/securing-your-api">Securing your API | Supabase Docs</a></li>
<li><a href="https://cybernews.com/security/lovable-ai-apps-expose-personal-information/">Lovable AI apps exposed sensitive data in open databases ...</a></li>
<li><a href="https://daily.dev/posts/lovable-apps-expose-passport-details-and-more-than-200k-private-messages-6xovsjn6q">Lovable apps expose passport details and more than 200K...</a></li>

</ul>
</details>

**标签**: `#security`, `#AI-generated code`, `#Row-Level Security`, `#Supabase`, `#data exposure`

---

<a id="item-tech-news-2"></a>
### [Project Zero 漏洞披露期缩短至 90 天](https://projectzero.google/2026/11/disclosure-policy.html) ⭐️ 8.0/10

谷歌 Project Zero 宣布，从即日起把漏洞披露期限定为向厂商报告后 90 天，并将于 2027 年 2 月 2 日改为 60 天、2028 年 1 月 3 日进一步改为 30 天。现行规则立即影响收到其漏洞报告的软件厂商和开源维护者；后两个更短期限目前只是已公布的计划，尚未生效。

hackernews · hacb · 11月14日 11:13 · [社区讨论](https://news.ycombinator.com/item?id=50496051)

**「背景」** Project Zero 是 Google 旗下的安全研究团队；其披露规则规定，从向厂商报告漏洞到公开细节之间有一段固定等待期。这个等待期的长短决定了厂商、开源维护者和安全团队需要多快完成修复与发布。

**「影响」** 对厂商和开源维护者而言，修补窗口将从 90 天逐步压缩到 30 天；若无法在期限内发布修复，漏洞细节可能在补丁就绪前公开，因此需要提前调整分诊、修复和发布流程。

**「社区讨论」** 评论中有人认为 Ubuntu 等大型开源项目需要远多于 90 天的时间，也有人主张应更早甚至立即公开，认为不施加压力厂商就不会修复。这些均为评论者观点，并非已确认的事实。

**标签**: `#vulnerability disclosure`, `#Project Zero`, `#software security`, `#open source maintenance`, `#security policy`

---

<a id="item-tech-news-3"></a>
### [EFF 再批科技公司试图重塑隐私概念](https://www.eff.org/deeplinks/2026/11/tech-companies-are-trying-shift-entire-concept-privacy-again) ⭐️ 7.0/10

电子前哨基金会（EFF）于 11 月 14 日发布评论文章，称科技公司正在再次尝试重新定义“隐私”这一概念，并把这种话语层面的转向本身当作需要警惕的对象。这是观点与分析文章，不是产品发布或政策变更，因此文中没有可核对的版本号、公司名单或可测量的结果。由于原始正文未随条目提供，文章的具体论证路径和所指企业的细节无法在此独立核实，读者需回到原文确认其主张。

hackernews · gslin · 11月14日 12:45 · [社区讨论](https://news.ycombinator.com/item?id=50496602)

**「背景」** EFF 的文章由 Thorin Klosowski 撰写，其核心论点是把隐私争论的焦点从“用户是否同意”转向“旁观者是否被记录”：文章列举了可拍摄佩戴者所见并用 AI 描述画面的 Meta 与 Google 智能眼镜、把 Apple Watch 变成转录设备的 Apple Audio Intelligence，以及可全程录音并转写的 Amazon Bee 等消费级产品。标题中的“again”表明这类重新定义隐私边界的主张并非首次出现，而本轮的特殊之处在于 AI 让持续录制与自动转写成为普通硬件的常规能力。

**「社区讨论」** Hacker News 的讨论集中在 AI 会议记录器上：一位评论者称如今几乎每场职业会议——包括直属经理与同事的一对一谈话——都会被可见或不可见的 AI 参会者录音并上传，个人难以在不影响就业的情况下退出，并追问是否有人把“本次会议不需要转录，请先关闭 AI 记录工具”变成惯例。另一位评论者从无障碍角度提出相反考量，认为做得好的实时转录眼镜对聋人和重听者可能是变革性的，本地模型本可以不保存、不导出数据，但“距离长期留存只差一个 if 语句”，因此争议应落在使用边界而非一刀切禁令上；另有评论者引用《世界人权宣言》第 12 条主张不受任意干涉的隐私权。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.eff.org/deeplinks/2026/11/tech-companies-are-trying-shift-entire-concept-privacy-again">Tech Companies Are Trying to Shift the Entire Concept of ...</a></li>
<li><a href="https://aiweekly.my/items/46520/tech-companies-are-trying-to-shift-the-concept-of-privacy-again">Tech Companies Are Trying to Shift the Concept of Privacy (Again)</a></li>

</ul>
</details>

**标签**: `#privacy`, `#AI surveillance`, `#tech policy`, `#EFF`, `#community debate`

---

<a id="item-tech-news-4"></a>
### [tiny-voca：4.5M 参数全开源 TTS，CPU 上 70 倍实时](https://www.reddit.com/r/LocalLLaMA/comments/1xw7zrg/tinyvoca_a_fully_open_45mparameter_tts_code/) ⭐️ 7.0/10

开发者 n4ze3m 发布了名为 tiny-voca 的英文语音合成模型，参数量为 4,537,291（约 18 MB，含波形生成部分），提供一男一女两个 24 kHz 音色。它在 4 个 CPU 线程上约达 70 倍实时速度，可通过 PyTorch、ONNX 运行，也能直接在浏览器本地推理——演示页面不向服务器发送任何内容。该项目宣称完全开放：代码、权重、训练配方和数据集均已公开，并使用自研音素化工具（dizione）；其速度关键在于用小型源-滤波合成器替代神经声码器，整个模型在一块 RTX 4090 上训练 7.7 小时完成。作者同时列出明确局限：仅支持英文和这两个音色、不支持声音克隆、外国人名与生僻拼写常读错、音质略显机械，且训练音频本身由 Qwen3-TTS 合成，因此效果不会超过该合成数据的上限。

reddit · r/LocalLLaMA · /u/nato\_nob · 11月14日 17:26

**「背景」** 多数神经 TTS 流程在声学模型之后还需要神经声码器把中间特征还原成波形，这通常带来额外的计算开销。tiny-voca 改用小型源-滤波器合成器直接生成声音，即让激励源经过声道滤波器来合成语音，因此能在 CPU 上保持高速；这也是它区别于常规神经声码器方案的关键。

**「实际影响」** 对希望在浏览器或低算力设备上做离线语音朗读的开发者来说，18 MB 的体积加 CPU 实时推理意味着无需 GPU 和服务器即可部署，代价是必须接受固定的两个音色、无克隆能力以及合成训练数据带来的音质天花板；作者也正公开征集数字、日期、人名和长句的失败样例，以便改进文本前端。

**标签**: `#text-to-speech`, `#open-source models`, `#on-device AI`, `#efficient inference`, `#tiny models`

---