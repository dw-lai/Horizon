---
layout: default
title: "Horizon Summary: 2026-11-02 (EN)"
date: 2026-11-02
lang: en
---

> From 29 items, 1 important content pieces were selected

---

**Technology News**
1. [llama2.c TinyStories runs integer-only on an 80 MHz iPod via Rockbox](#item-tech-news-1) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [llama2.c TinyStories runs integer-only on an 80 MHz iPod via Rockbox](https://www.reddit.com/r/LocalLLaMA/comments/1xlboqi/llama2c_on_a_2006_ipod_80_mhz_w_64_mb_ram_and_no/) ⭐️ 7.0/10

A developer has written a Rockbox plugin that runs Karpathy&\#x27;s llama2.c TinyStories models on an iPod Video 5.5G, whose PortalPlayer PP5022 ARM7TDMI CPU runs at 80 MHz with 64 MB of RAM and no FPU. To make this work, the author ported llama2.c&\#x27;s int8 \`runq.c\` path to integer-only math, using lookup tables for exp and softmax and an integer square root for RMSNorm. The 15M-parameter model is 17 MB, so it loads directly off the hard drive into the music buffer. The author notes that music playback is unavailable while inference runs, and says future work includes using both cores and building a more iPod-themed model for local music recommendation.

reddit · r/LocalLLaMA · /u/r0tlier0 · Nov 1, 19:15

**「Prerequisite: llama2.c and its int8 engine」** Karpathy&\#x27;s llama2.c is a minimal pure-C implementation: a Llama 2 architecture model is trained in PyTorch, then run for inference by a roughly 700-line C file. The repository also ships runq.c, an int8-quantized inference engine that reduces memory usage and can improve inference speed while keeping accuracy reasonable. The iPod port starts from that quantized engine and has to remove its floating-point dependencies.

**「Impact」** The demonstration shows that the int8 llama2.c path can be made to run without floating-point hardware on a 2006-era ARM7TDMI, with lookup tables and integer square root replacing the floating-point operations in exp/softmax and RMSNorm. The tradeoff is memory placement: because the 17 MB model occupies the music buffer, the plugin cannot play audio while it works, a practical constraint the author flags rather than solves.

<details><summary>References</summary>
<ul>
<li><a href="https://github.com/karpathy/llama2.c">GitHub - karpathy/llama2.c: Inference Llama 2 in one file of ...</a></li>
<li><a href="https://deepwiki.com/karpathy/llama2.c/2.2-quantized-inference-%28runq.c%29">Quantized Inference (runq.c) | karpathy/llama2.c | DeepWiki</a></li>

</ul>
</details>

**Tags**: `#embedded machine learning`, `#llama2.c`, `#integer-only inference`, `#Rockbox`, `#retro hardware`

---