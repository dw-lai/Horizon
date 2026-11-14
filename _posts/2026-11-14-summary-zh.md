---
layout: default
title: "Horizon Summary: 2026-11-14 (ZH)"
date: 2026-11-14
lang: zh
---

> 从 37 条内容中筛选出 3 条重要资讯。

---

**科技新闻**
1. [llama.cpp 发布 v1.0，Hugging Face 同步推出 Llama 桌面应用](#item-tech-news-1) ⭐️ 8.0/10
2. [KORS 实时航空波段：GPU 全频段转写与温哥华地面停飞](#item-tech-news-2) ⭐️ 7.0/10
3. [Qwen3.5-9B 借助 MTP 投机解码在未改装的 PS4 上离线运行](#item-tech-news-3) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [llama.cpp 发布 v1.0，Hugging Face 同步推出 Llama 桌面应用](https://www.reddit.com/r/LocalLLaMA/comments/1xv8t2e/llamacpp_v10_is_here/) ⭐️ 8.0/10

Hugging Face 的 Merve 在 Reddit 发帖宣布，llama.cpp 正式发布 v1.0。她表示项目今后会继续覆盖所有平台和所有模型类型，同时让 llama.cpp 对基于它构建的下游应用保持稳健和精简。同一帖子里还宣布，Hugging Face 一直在发布基于 llama.cpp 构建的 Llama 桌面应用（llama.app），目标是把上手本地 AI 的门槛降到只需点击几次。该帖是简短的宣传性公告，没有披露 v1.0 的具体技术变更、兼容性说明或性能数据，只给出指向博客和 llama.app 的链接。

reddit · r/LocalLLaMA · /u/unofficialmerve · 11月13日 14:07

**「背景」** llama.cpp 已开发约 3.5 年；据 ggml-org 的发布说明，此次 v1.0.0 同时为 libllama 和 ggml 引入语义化版本管理。维护者表示，今后只有主版本号升级才会反映 API 和 ABI 不兼容变更，这为依赖这些库的下游应用提供了更明确的兼容性约定。

**「影响」** 对想跑本地模型的用户来说，最直接的变化是可以走 llama.app 桌面应用，而不必自己编译 llama.cpp；对在其上构建的下游开发者，公告只承诺继续维护平台与模型类型的覆盖，并未说明 v1.0 是否带来 API 或行为上的不兼容变更，升级前应先查看其链接的博客。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://aiweekly.co/alerts/llamacpp-ships-v100-with-semver-for-libllama-and-ggml">llama.cpp Ships v1.0.0 With Semver for libllama and ggml</a></li>

</ul>
</details>

**标签**: `#llama.cpp`, `#local LLM inference`, `#open source`, `#GGML`, `#Hugging Face`

---

<a id="item-tech-news-2"></a>
### [KORS 实时航空波段：GPU 全频段转写与温哥华地面停飞](https://orcasairband.com/) ⭐️ 7.0/10

一个名为 orcasairband.com 的实时监听项目在 KORS（Orcas Island）用 ETTUS B210 接收航空波段全频段，并在双 4090 GPU 主机上通过 CUDA 多相信道化器拆分、解调、检测通话，再生成转写。项目作者 mmaunder 称，温哥华地区这次地面停飞让该项目意外派上用场，方便当地飞行员了解空域内的相关通话。他公布的原始片段包括维多利亚地面频率提到“通信问题”导致交通停止，以及温哥华中心频率上飞行员谈论替代计划。这些转写未经编辑且可能含无法辨识内容，不能当作官方 ATC 记录。

hackernews · mmaunder · 11月13日 22:04 · [社区讨论](https://news.ycombinator.com/item?id=50490593)

**「技术前提」** ETTUS B210 是 Ettus Research 的 USRP 软件无线电，官方标称覆盖 70 MHz–6 GHz、最高 56 MHz 瞬时带宽，并通过 USB 3.0 连接主机（tool-2-1、tool-2-2）。这类宽带前端先把大段频谱数字化，再由主机侧的 DSP 划分为多个窄带信道，因此同一套硬件可以同时处理原本需要多台接收机分别覆盖的多个频道。

**「影响」** 对该项目的听众而言，实际好处是一次接收即可覆盖多个 ATC 频率，而不必逐频调谐；想复制这一能力则需要 B210 与双 GPU 的 CUDA 处理链。

**「社区讨论」** 作者 mmaunder 在评论中补充了双 4090 与 CUDA 信道化器的架构，并贴出与停飞相关的原始转写；molsongolden 则指出，帖子发布时段的一段通话明确确认了温哥华地面停飞。plipt 对大量通话听起来含混表示意外，ltrg 将其类比为用公共 KiwiSDR 解码船舶 DSC 信号的爱好者项目。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.ettus.com/all-products/ub210-kit/">USRP B210 USB Software Defined Radio (SDR) - Ettus Research</a></li>
<li><a href="https://files.ettus.com/manual/page_usrp_b200.html">USRP Hardware Driver and Device Manual: USRP B2x0 Series Hi all. Thanks for the interest. I&#x27;m going to post an ... B200/B210/B200mini/B205mini/B206mini - Ettus Knowledge Base USRP B210 | COSMOS Wiki N200/N210 - Ettus Knowledge Base USRP Hardware Driver and USRP Manual: USRP B2x0 Series</a></li>

</ul>
</details>

**标签**: `#software-defined radio`, `#airband`, `#CUDA`, `#GPU signal processing`, `#ATC transcription`

---

<a id="item-tech-news-3"></a>
### [Qwen3.5-9B 借助 MTP 投机解码在未改装的 PS4 上离线运行](https://www.reddit.com/r/LocalLLaMA/comments/1xvbn2m/qwen359b_running_on_a_ps4s_gpu_offline_using_its/) ⭐️ 7.0/10

开源项目 garlic-llm 的作者称，Qwen3.5-9B 可在未改装的 PS4 GPU 上完全离线运行，速度达到 31–39 tok/s。其做法是把权重重新打包为自定义的 4 位和 3 位格式，以压缩到约 4.5 GiB，并利用 Qwen3.5 自带的 MTP 头进行投机解码：该头一次最多草拟两个 token，再由完整模型一次校验，使同一块老 GPU 上的速度从 22 tok/s 提升到 31–39 tok/s。作者表示该方案不需要云端、订阅或 Linux，代码在 GitHub、权重在 Hugging Face 提供下载。上述吞吐与实现细节均为作者在 Reddit 上的自述，尚无独立验证。

reddit · r/LocalLLaMA · /u/leonardo\_alegria · 11月13日 16:00

**「背景」** MTP（多 token 预测）是 Qwen3.5-9B 随模型提供的草稿模块；在投机解码中，它先提议后续 token，再由完整模型一次性校验，从而减少串行前向次数。推理引擎必须显式实现 MTP 投机解码，才能获得这项加速；仅有模型文件中的 MTP 张量并不够；若第三方导出漏掉该模块，还需恢复权重与配置。

**「影响」** 对想用现成 PS4 做本地推理的用户来说，这个项目的实际门槛在于必须使用项目自行重打包的 3/4 位权重，而不能直接加载原始 Qwen3.5-9B 权重；同时 31–39 tok/s 的速率目前只有作者自报，部署前应自行复现测量。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://ollama.com/aiconjured/Qwen3.5-9B-Uncensored-HauhauCS-Aggressive-MTP-GGUF-NVFP4">aiconjured/ Qwen 3 . 5 - 9 B -Uncensored-HauhauCS-Aggressive...</a></li>
<li><a href="https://empero.org/writing/qwythos-9b-v2">Qwythos- 9 B -v2: a 9 B that knows when to stop — Empero</a></li>

</ul>
</details>

**标签**: `#local LLM inference`, `#speculative decoding`, `#quantization`, `#PS4 homebrew`, `#open-source project`

---