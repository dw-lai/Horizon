---
layout: default
title: "Horizon Summary: 2026-11-02 (ZH)"
date: 2026-11-02
lang: zh
---

> 从 29 条内容中筛选出 1 条重要资讯。

---

**科技新闻**
1. [Rockbox 插件让 llama2.c 在无 FPU 的 iPod 上运行](#item-tech-news-1) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Rockbox 插件让 llama2.c 在无 FPU 的 iPod 上运行](https://www.reddit.com/r/LocalLLaMA/comments/1xlboqi/llama2c_on_a_2006_ipod_80_mhz_w_64_mb_ram_and_no/) ⭐️ 7.0/10

作者 r0tlier0 发布了一个 Rockbox 插件，在 2006 年的 iPod Video 5.5G 上运行 Karpathy 的 llama2.c TinyStories 模型；该设备采用 80 MHz ARM7TDMI（PortalPlayer PP5022）和 64 MB 内存，且没有 FPU。为绕过浮点运算限制，插件把 llama2.c 的 int8 runq.c 改成纯整数推理：用查找表实现 exp 和 softmax，用整数平方根实现 RMSNorm。15M 参数模型约 17 MB，可直接从硬盘载入音乐缓冲区运行，但运行期间无法同时听音乐。作者表示，后续计划利用双核，并制作一个本地音乐推荐主题模型。

reddit · r/LocalLLaMA · /u/r0tlier0 · 11月1日 19:15

**「项目背景」** karpathy 的 llama2.c 项目用约 700 行纯 C 代码（run.c）实现 Llama 2 架构推理，另外还提供了一份独立的 int8 量化推理实现 runq.c，以量化方式降低内存占用并提升推理速度。而 2006 年的 iPod Video 5.5G 所用的 ARM7TDMI 内核不带浮点运算单元（FPU），浮点运算只能靠软件模拟，因此把 runq.c 改写成纯整数推理时，exp/softmax 与 RMSNorm 等原本依赖浮点的环节都必须另找整数替代方案。

**「影响」** 对嵌入式推理爱好者而言，这个实验展示了在无 FPU、80 MHz 级 ARM7 设备上运行 int8 小模型的可行方式，但复现时需接受模型占用约 17 MB 音乐缓冲区、且推理期间不能播放音乐的约束。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://github.com/karpathy/llama2.c">GitHub - karpathy/llama2.c: Inference Llama 2 in one file of ...</a></li>
<li><a href="https://deepwiki.com/karpathy/llama2.c/2.2-quantized-inference-%28runq.c%29">Quantized Inference (runq.c) | karpathy/llama2.c | DeepWiki</a></li>

</ul>
</details>

**标签**: `#embedded machine learning`, `#llama2.c`, `#integer-only inference`, `#Rockbox`, `#retro hardware`

---