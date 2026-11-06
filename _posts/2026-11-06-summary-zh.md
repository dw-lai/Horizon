---
layout: default
title: "Horizon Summary: 2026-11-06 (ZH)"
date: 2026-11-06
lang: zh
---

> 从 52 条内容中筛选出 8 条重要资讯。

---

**科技新闻**
1. [Claude Code 被指经 UA 头泄露邮箱，2.1.317 内置拦截](#item-tech-news-1) ⭐️ 8.0/10
2. [“sshole”条目引发 OpenSSH crypt\(\) 认证缺陷讨论](#item-tech-news-2) ⭐️ 8.0/10
3. [冷门音频编解码器适配 N64 受限硬件](#item-tech-news-3) ⭐️ 7.0/10
4. [OpenSSH 10.6p2 为无 PAM 的 Alpine 提供关键规避方案](#item-tech-news-4) ⭐️ 7.0/10
5. [百度发布 ERNIE 5.5 Flash Base 基础模型](#item-tech-news-5) ⭐️ 7.0/10
6. [Delta 推理引擎 v0.93：单张 RTX 3090 跑 DeepSeek-V4.1-Flash-1017](#item-tech-news-6) ⭐️ 7.0/10
7. [CCORE 发布 GLB-3D-Coder 数据集：3,918 个经渲染测试的 3D 示例](#item-tech-news-7) ⭐️ 7.0/10

**财经新闻**
1. [巴拉圭总统因 Ueno 数字银行倒闭辞职](#item-finance-news-1) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Claude Code 被指经 UA 头泄露邮箱，2.1.317 内置拦截](https://github.com/anthropics/claude-code/issues/107757) ⭐️ 8.0/10

据 GitHub issue 报告，Claude Code 的子代理在向网站发起 HTTP 请求时，可能把用户姓名、公司和邮箱等标识写进 User-Agent 头。评论者 mpoteat 回应称，维护方已推出内置模块 cc-plugin-privacy 来确定性阻止该行为，2.1.317 及更高版本会包含这项检查，用户可通过 /plugins 关闭。现有材料没有说明该行为始于哪个版本或影响范围。

hackernews · motoroco · 11月5日 22:17 · [社区讨论](https://news.ycombinator.com/item?id=50385272)

**「背景」** HTTP 请求中的 User-Agent 头通常用于标识发起请求的客户端软件；GitHub 问题 \#107757 报告称，Claude Code 在进行网页搜索等出站请求时，会把登录用户的邮箱等身份信息写入该请求头，并发送给第三方网站。该报告者称自己因此每天收到大量诈骗邮件，并要求从工具本身移除这一行为，而不是只提供退出选项。

**「影响」** 对使用 Claude Code 的开发者而言，若仍在使用未包含该检查的版本，子代理发起的对外请求可能把个人和公司标识暴露给目标站点或其日志；升级到 2.1.317+ 可让内置 cc-plugin-privacy 检查生效，但通过 /plugins 关闭该检查会重新暴露该行为，且已发出的 User-Agent 头无法撤回。

**「社区讨论」** 评论者 mk89 称换用 Claude 后工作邮箱几乎每天收到带真实姓名的垃圾邮件，但这是个人观察，不能据此认定与 Claude Code 的 UA 行为存在因果。llama052 则贴出了子代理通过 curl 访问其公司服务器时 UA 头包含公司名、项目名和个人姓名的具体示例；O\_H\_E 认为该问题凸显了 agentic coding 中代理持久执行任务与及时向人类确认之间的长期矛盾。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://github.com/anthropics/claude-code/issues/107757">Bug Report: Privacy violation in User-Agent header · Issue ...</a></li>
<li><a href="https://aiweekly.co/alerts/claude-code-bug-report-alleges-email-leak-in-user-agent-header">Claude Code bug report alleges email leak in User-Agent ...</a></li>

</ul>
</details>

**标签**: `#privacy leak`, `#Claude Code`, `#AI coding agents`, `#security`, `#User-Agent headers`

---

<a id="item-tech-news-2"></a>
### [“sshole”条目引发 OpenSSH crypt\(\) 认证缺陷讨论](https://sshhole.com/) ⭐️ 8.0/10

Hacker News 上仅以链接形式提交的“sshole”条目，引发了可能影响 OpenSSH 用户及 musl libc 系统的密码认证漏洞讨论：评论者称，攻击者试图让 \`crypt\($pw, $hash\)\` 的结果等于 \`$hash\`，从而通过 sshd 的密码校验。讨论将根本原因指向 \`\*\`、\`\!\` 等锁定账户哨兵值与 crypt\(\) 错误返回混用所造成的带内信号问题。另有评论称 musl libc 的 \`crypt\_sha\` 路径也存在同类缺陷，而 \`crypt\_des\` 中的既有规避没有覆盖它；由于提交本身未给出受影响版本、利用条件或修复状态，严重性仍未确认。

hackernews · josemrb · 11月5日 12:19 · [社区讨论](https://news.ycombinator.com/item?id=50378228)

**「背景」** OpenSSH 的 sshd 会调用 \`crypt\($pw, $hash\)\` 校验密码，而被设为禁止密码登录的账户通常不会使用正常的密码哈希。此次问题的前提是 OpenSSH 与 musl libc 的 crypt 实现之间存在交互缺陷：在未启用 PAM 的 musl 系统上，攻击者可用 257 至 1024 字节的密码，让本应无法用密码登录的账户通过认证，Alpine Linux 等环境因此受影响。该漏洞于 2026-11-05 披露，并已在 OpenSSH 10.6p2 中修复。

**「影响范围与处置」** 影响集中在使用 musl libc 的 Linux 发行版（Alpine Linux、OpenWrt、Buildroot、Yocto）上的 OpenSSH 服务器；Alpine 默认的 openssh-server 配置在受影响之列，而改用 openssh-server-pam 并设置 UsePAM yes 的部署不受影响，UsePAM no 则仍会受影响。Alpine 公告点名 /etc/shadow 中密码字段为 \`\!\` 的锁定账户，并说明这类账户无法以密码或密钥登录。运维方应升级到 2026 年 11 月 5 日发布的 OpenSSH 10.6p2。

**「社区讨论」** 多名评论者将问题归因于“带内信号”式设计，认为 \`\*\` 不应同时表示 /etc/passwd 中的“无密码”和 crypt\(\) 的哈希错误，并主张改用明确的失败值或结果类型；也有人指出，musl 在 \`crypt\_des\` 中的旧规避在 salt 为 \`x\` 时仍有缺陷。这些都属于社区分析，不等同于对漏洞范围或修复状态的确认。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://arstechnica.com/security/2026/11/vulnerability-allows-attackers-to-log-into-some-linux-devices-sans-password/">Meet *sshole, the vulnerability that lets hackers SSH into ...</a></li>
<li><a href="https://www.bleepingcomputer.com/news/security/openssh-flaw-lets-attackers-log-into-password-disabled-linux-accounts/">OpenSSH flaw lets attackers log into password-disabled Linux ...</a></li>
<li><a href="https://github.com/schappim/sshole-audit">GitHub - schappim/sshole-audit: Find, prove and fix *sshole ...</a></li>
<li><a href="https://www.ox.security/blog/openssh-authentication-bypass-cve-2026-123158/">OpenSSH Bypass: CVE-2026-123158 | OX Security</a></li>
<li><a href="https://alpinelinux.org/posts/2026-11-05-openssh-password-authentication-bypass/">Security advisory: openssh -server password authentication bypass</a></li>
<li><a href="https://www.bleepingcomputer.com/news/security/openssh-flaw-lets-attackers-log-into-password-disabled-linux-accounts/">OpenSSH flaw lets attackers log into password-disabled Linux accounts</a></li>

</ul>
</details>

**标签**: `#security vulnerability`, `#OpenSSH`, `#authentication`, `#musl libc`, `#crypt`

---

<a id="item-tech-news-3"></a>
### [冷门音频编解码器适配 N64 受限硬件](https://phoboslab.org/log/2026/11/n64-ulc-codec) ⭐️ 7.0/10

一篇技术文章探讨了将一种冷门音频编解码器用于 N64 的适配思路，面向自制程序与 demoscene 开发者。文章的核心是在 N64 极度受限的硬件上实现音频解码，而非发布新的编解码器、官方工具或可下载产品。由于源材料未提供文章正文，具体编解码器名称、压缩参数和实测性能均无法从现有信息确认。

hackernews · frostbyte7 · 11月5日 12:51 · [社区讨论](https://news.ycombinator.com/item?id=50378508)

**「背景：N64 的音频限制」** 文章回顾称，N64 上可用于播放和存储音频的方案非常有限，这是该项目要应对的硬件前提。phoboslab 的 ulc64 项目将冷门的 ULC 编解码器移植到 N64；文章称其可实现 44.1 kHz 立体声、接近 Opus 的码率，并只占用约 4% 的 CPU 时间。

**「社区讨论」** 评论区最有信息量的是历史与实现层面的讨论：一位评论者回顾 1999 年前后 MP3 专利环境，认为这类编解码器当年很难被采用，并提到 N64 的 MP3 解码曾涉及 Fraunhofer 专利授权；另一位评论者则追问解码器几乎占满 4KB RSP 指令内存后，是否还给游戏图形留下足够空间。还有人澄清演示中人声难辨、断续来自原始音轨，而非解码缺陷，并对作者提到使用 LLM 表示不满。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://phoboslab.org/log/2026/11/n64-ulc-codec">Why this Obscure Audio Codec is a Perfect Fit for the N64</a></li>
<li><a href="https://github.com/phoboslab/ulc64">GitHub - phoboslab/ulc64: ulc-codec on the n64 · GitHub</a></li>

</ul>
</details>

**标签**: `#N64`, `#audio codec`, `#homebrew`, `#demoscene`, `#constrained hardware`

---

<a id="item-tech-news-4"></a>
### [OpenSSH 10.6p2 为无 PAM 的 Alpine 提供关键规避方案](https://www.openssh.org/releasenotes.html#10.6p2) ⭐️ 7.0/10

OpenSSH 10.6p2 已发布，为未使用 PAM 的 Alpine 系统提供一项被标为关键的规避方案，影响范围被明确限定在这一特定组合。现有发布说明级材料未提供漏洞编号、触发条件或独立复现结果，因此尚不能据此判断其他平台是否受影响。

hackernews · selckin · 11月5日 11:40 · [社区讨论](https://news.ycombinator.com/item?id=50377976)

**「背景」** OpenSSH 的 Portable 版本需要适配不同的 libc 和认证后端；Alpine Linux 使用 musl libc，且不少安装不启用 PAM。正因认证栈不同于常见的 PAM 路径，这个密码认证绕过问题只影响 musl libc 且禁用 PAM 的 Linux 配置，10.6p2 因此以点版本形式提供关键 workaround。

**「影响与应对」** 对受影响者的具体后果是：使用 musl 且禁用 PAM、同时开启密码登录的 Linux 服务器（最典型的是 Alpine）需要在升级前先把 PasswordAuthentication 设为 no，或直接停掉 sshd，然后再安装 OpenSSH 10.6p2 或发行版提供的修复包。Alpine 稳定分支的软件包已经带有针对同一问题的补丁，因此用户应先确认所用发行版是否已包含修复，避免只依赖上游版本号来判断。

**「社区讨论」** 评论者重点讨论披露时机，并引述维护者的说法称，AI 代理有时能在数小时内快速重新发现漏洞，因此长期禁运反而主要利于攻击者；也有人认为白帽与黑帽之间存在长期的人员与信息重叠。这些属于社区观点和转述，并非对漏洞严重性或影响范围的独立验证。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.rescana.com/post/openssh-10-6p2-alpine-musl-password-auth-bypass-prepare-now">OpenSSH 10.6p2 Fixes Critical Password Bypass on Alpine and ...</a></li>
<li><a href="https://www.privacyaffairs.com/openssh-alpine-password-bypass/">OpenSSH 10.6p2 Fixes Password Bypass on Alpine Linux</a></li>
<li><a href="https://www.rescana.com/post/openssh-10-6p2-alpine-musl-password-auth-bypass-prepare-now">OpenSSH 10.6p2 Fixes Critical Password Bypass on Alpine and ...</a></li>
<li><a href="https://www.privacyaffairs.com/openssh-alpine-password-bypass/">OpenSSH 10.6p2 Fixes Password Bypass on Alpine Linux</a></li>
<li><a href="https://www.siteguarding.com/security-blog/alpine-openssh-password-login-check/">OpenSSH 10.6p2 on Alpine: Disable SSH Password Login Now</a></li>

</ul>
</details>

**标签**: `#OpenSSH`, `#security updates`, `#Alpine Linux`, `#vulnerability disclosure`, `#AI-assisted bug discovery`

---

<a id="item-tech-news-5"></a>
### [百度发布 ERNIE 5.5 Flash Base 基础模型](https://ernie.baidu.com/release/ernie-5-5-flash-base/) ⭐️ 7.0/10

百度发布了 ERNIE 5.5 Flash Base，将其作为基础模型推出；提供的材料没有给出参数规模、训练数据、基准成绩或独立测评结果。Hacker News 评论称，该许可证禁止欧盟、英国和韩国使用，并要求开发衍生模型的开发者确保这些地区无人使用其作品。因此，当前可确认的是发布本身，具体能力和许可约束仍待原始条款核实。

hackernews · pretext · 11月5日 09:29 · [社区讨论](https://news.ycombinator.com/item?id=50377078)

**「背景」** 基座模型是只完成预训练、需要使用者自行微调或对齐的检查点，区别于开箱即用的指令微调对话模型；本地微调、企业按内部规则训练等用法都以此为前提。ERNIE 是百度的大语言模型系列，据第三方汇总，此次 ERNIE 5.5 Flash Base 为 280B 参数的 MoE 模型（激活参数 14B、上下文长度 1M），并采用带地域限制的百度自定义许可证。

**「影响」** 若上述许可条款属实，位于欧盟、英国和韩国的团队无法直接采用该模型，且分发微调产物的开发者需承担跨地区合规责任，采用前应核对许可证原文。

**「社区讨论」** 支持发布的评论者看重其作为可本地微调的基础模型，有人称其表现可能强于 Qwen3.8-27B 和 Deepseek-v4-Flash，但这只是个人判断、未经独立验证。反对意见集中在许可证的地域限制；也有开发者询问在多节点 InfiniBand 集群上继续训练应选 NeMo 还是 HF TRL+Accelerate。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.llms.blog/posts/ernie-5-5-flash-base-open-weights-license">Baidu ERNIE 5.5 Flash Base: 280B Weights and License</a></li>
<li><a href="https://www.orcarouter.ai/blog/ernie-5-5-flash-base-open-weights-license">ERNIE-5.5-Flash-Base: 280B open weights, tight licence</a></li>

</ul>
</details>

**标签**: `#large language models`, `#Baidu ERNIE`, `#base models`, `#software licensing`, `#fine-tuning`

---

<a id="item-tech-news-6"></a>
### [Delta 推理引擎 v0.93：单张 RTX 3090 跑 DeepSeek-V4.1-Flash-1017](https://www.reddit.com/r/LocalLLaMA/comments/1xoq4vq/deepseekv41flash1017_on_one_rtx_3090_big_updates/) ⭐️ 7.0/10

Delta Inference Engine v0.93 发布，新增对 64/96/128 GB 内存配置的支持，并可直接读取 Unsloth 量化模型的 Engram 表，使 UD-IQ2\_XXS 在 192 GB 内存下保持 41 tok/s 的同时质量提升。作者自测的 99 题基准中，UD-IQ2\_XXS 答对 57 题，高于上一版 ds4 Q2 的 52 题，接近完整模型 API 的 59 题；首 token 延迟从约 3.8 秒降至 2.3 秒（约 180 token 提示）。此外加入基础多 GPU 支持（3060+3090 约 7% 提升）、EXL3 2.5 bpw 支持、GitHub Actions 公共 CI 构建，以及修复超 65,535 token 上下文等问题。以上均为作者自报数据，仅在一台 i5-13600K、单张 RTX 3090 24 GB 的 Windows 机器上测得，尚未经独立验证。

reddit · r/LocalLLaMA · /u/musicurgy · 11月5日 18:23

**「背景」** Delta Inference Engine 是 Xolotl（原名 Strata-DSV4.1）的 Windows 移植版，基于 Strata 构建，采用 MIT 许可证。Xolotl 项目此前已展示在单台游戏 PC（RTX 4090 加 90 GB 内存）上以最高约 27 tok/s 运行完整的 552B DeepSeek-V4.1-Flash，并支持 512K 上下文。

**「对本地推理用户的影响」** 64 GB 内存用户现在可以运行该模型，但速度明显下降：UD-IQ2\_XXS 在 64 GB 下为 21 tok/s，96 GB 下为 29.3 tok/s，128 GB 下为 34 tok/s，均低于 192 GB 的 41 tok/s。软件要求 Windows 10/11、NVIDIA 驱动 580 或更新、至少 12 GB 显存（24 GB 为快速路径），不支持 AMD GPU，模型文件需 233–395 GB 的 NVMe 空间。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://github.com/Indras-Mirror/Xolotl">GitHub - Indras-Mirror/ Xolotl : Xolotl (formerly Strata -DSV4.1): run...</a></li>
<li><a href="https://ai-manual.ru/article/delta-inference-engine-v093-kak-zapustit-kvantovannuyu-deepseek-v41-flash-na-odnoj-rtx-3090/">Delta Inference Engine v0.93: как запустить... | AiManual</a></li>

</ul>
</details>

**标签**: `#local LLM inference`, `#quantization`, `#GPU benchmarking`, `#inference engine`, `#memory optimization`

---

<a id="item-tech-news-7"></a>
### [CCORE 发布 GLB-3D-Coder 数据集：3,918 个经渲染测试的 3D 示例](https://www.reddit.com/r/LocalLLaMA/comments/1xozbe6/ccore_glb3dcoder_dataset_is_here_3918_rendered/) ⭐️ 7.0/10

CCORE 发布了用于训练 Three.js/GLB 3D 资产生成模型的 CCORE GLB-3D-Coder 数据集，共 3,918 个示例，覆盖角色、生物、车辆、实验室设备、乐器、建筑、机械、自然和日常道具等 40 个领域。每个示例都经过测试和渲染，导出的 GLB 在纳入前经过验证；数据集包含完整对话、推理轨迹、HTML/JavaScript 响应、每个示例的渲染参考图，以及静态资产和带动画与交互的示例。数据划分为 3,501 个训练示例和 417 个验证示例，采用 MIT 许可证，并同时提供配套的 4B 模型权重。

reddit · r/LocalLLaMA · /u/ConfidentDinner6648 · 11月6日 00:43

**「背景」** 该数据集用于训练 CCORE GLB-3D-Coder，这是一个基于 Qwen3.5-4B 的 4B 参数专用模型，可根据文字描述生成完整的 Three.js HTML/JavaScript 页面，并带有预览和导出 GLB 按钮，面向低多边形游戏资产与程序化场景。发布者称这是此前预告的数据集，本次公开的是训练该模型所用的数据及完整权重。

**「实际影响」** 开发者可以直接用这批带渲染参考图和推理轨迹的示例微调本地模型，生成可导出 GLB 的 Three.js 代码；MIT 许可证和公开权重降低了复用门槛，但数据集规模有限，效果仍需使用者自行验证。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://huggingface.co/ccore/Qwen3.5-4B-GLB-3D-Coder">ccore /Qwen3.5-4B- GLB - 3 D - Coder · Hugging Face</a></li>
<li><a href="https://pirateface.co/ccore/Qwen3.5-4B-GLB-3D-Coder">ccore /Qwen3.5-4B- GLB - 3 D - Coder · Pirate Face</a></li>

</ul>
</details>

**标签**: `#3D asset generation`, `#Three.js`, `#LLM fine-tuning`, `#open-source dataset`, `#GLB`

---

## 财经新闻

<a id="item-finance-news-1"></a>
### [巴拉圭总统因 Ueno 数字银行倒闭辞职](https://cointelegraph.com/news/paraguay-president-resigns-after-collapse-ueno-digital-bank?utm_source=rss_feed&amp;utm_medium=rss&amp;utm_campaign=rss_partner_inbound) ⭐️ 7.0/10

巴拉圭总统圣地亚哥·培尼亚（Santiago Peña）在 Ueno 数字银行倒闭后辞职，此前他因与该行母公司过往的关系而受到越来越多的审视；该行倒闭导致数百万客户无法取用资金。

rss · Cointelegraph · 11月5日 17:40

**「背景」** 此前，巴拉圭中央银行于周二接管了与总统圣地亚哥·培尼亚关系密切的大型数字银行 Ueno，导致约 300 万客户无法动用资金，并引发街头抗议和弹劾动议（tool-1-1、tool-1-3）。培尼亚直到 2025 年仍是该行所有者的商业伙伴，而他的央行行长此前曾执掌这家银行（tool-1-2）。

**「影响」** 巴拉圭央行已接管 Ueno Bank 并冻结其全部资产，约 300 万客户（包括养老金领取者）暂时无法取回存款，存款保障的覆盖范围和赔付方式尚不明确。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.arkansasonline.com/news/2026/nov/04/paraguays-central-bank-seizes-lender-with-ties-to/">Paraguay’s central bank seizes lender with ties to Peña</a></li>
<li><a href="https://www.latimes.com/world-nation/story/2026-11-03/paraguay-seizes-major-digital-bank-tied-to-president-leaving-millions-of-customers-in-limbo">Paraguay seizes major digital bank tied to president, leaving millions of...</a></li>
<li><a href="https://www.zerohedge.com/personal-finance/bank-tied-paraguays-president-just-collapsed-and-depositors-are-streets">Paraguay&#x27;s President Resigns Amid Ueno Bank Crisis... | ZeroHedge</a></li>
<li><a href="https://www.marketcollapse.com/news/ueno-bank-paraguay-what-we-know/">ueno bank Paraguay: what depositors need to know</a></li>
<li><a href="https://en.mercopress.com/2026/11/04/paraguay-takes-over-ueno-bank-with-3-million-customers-and-freezes-its-deposits">Paraguay takes over Ueno Bank, with 3 million customers, and ...</a></li>
<li><a href="https://www.hindustantimes.com/world-news/paraguay-banking-crisis-leaves-millions-locked-out-of-accounts-ueno-bank-santiago-pena-protest-101793879644459.html">‘Lost my life savings’: Paraguay banking crisis triggers ...</a></li>

</ul>
</details>

**标签**: `#Paraguay`, `#banking crisis`, `#Ueno Bank`, `#political resignation`, `#financial stability`

---