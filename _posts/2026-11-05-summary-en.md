---
layout: default
title: "Horizon Summary: 2026-11-05 (EN)"
date: 2026-11-05
lang: en
---

> From 45 items, 9 important content pieces were selected

---

**Technology News**
1. [Moonshot AI releases Kimi K3.1 Pro open weights](#item-tech-news-1) ⭐️ 8.0/10
2. [OpenAI describes cutting a thousand Linux kernel root paths](#item-tech-news-2) ⭐️ 8.0/10
3. [AI Vulnerability Discovery Forces a Security Debt Reckoning](#item-tech-news-3) ⭐️ 8.0/10
4. [Tencent presents Hy4 open-weight model with HyCell and HyPDE](#item-tech-news-4) ⭐️ 8.0/10
5. [Anthropic Reports Progress on Cryptographic Proofs for LLM Inference](#item-tech-news-5) ⭐️ 8.0/10
6. [Go announces encoding/json/v2, a new standard-library JSON API](#item-tech-news-6) ⭐️ 8.0/10
7. [AMD projects Q4 revenue above Intel for the first time](#item-tech-news-7) ⭐️ 7.0/10
8. [OpenAI to acquire Pierre Computer Company](#item-tech-news-8) ⭐️ 7.0/10
9. [Ricursive Intelligence posts Ripple-65B-Preview dense open-weights model](#item-tech-news-9) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Moonshot AI releases Kimi K3.1 Pro open weights](https://huggingface.co/moonshotai/Kimi-K3.1-Pro) ⭐️ 8.0/10

Moonshot AI has published open weights for Kimi K3.1 Pro on Hugging Face. The supplied material does not include the model card, license terms, parameter count, or independent benchmark results, so the release&\#x27;s practical openness and performance cannot be verified from the item alone.

hackernews · abrarthought · Nov 4, 15:30 · [Discussion](https://news.ycombinator.com/item?id=50366999)

**「Background」** Kimi K3.1 Pro is the first model in Moonshot AI&\#x27;s K3.1 series and, according to its model card, was post-trained from Kimi K3 using large-scale joint reinforcement learning across hundreds of downstream domains. Its predecessor, Kimi K3, was presented as a 2.8T-parameter open-weight multimodal model with a 1-million-token context window, built on Kimi Delta Attention and Attention Residuals.

**「Impact」** For individual users, local deployment may be gated by hardware: one commenter estimates that running the model would require something like an 8×B300 node, while noting plans to stay on a smaller Qwen model instead. The item provides no official hardware requirements, so that estimate is unverified; teams should confirm memory and serving requirements before planning self-hosting.

**「Community discussion」** Commenters are split on benchmark credibility: some call Kimi K3.1 Pro “benchmaxxed” and say it does not clearly beat DeepSeekV4.1-Flash, while another reports that their testing did not show this and rates it as very strong for most use cases. A separate commenter disputes the “open-weight” label, and others point to third-party hosting on OpenRouter as the practical way to access the model.

<details><summary>References</summary>
<ul>
<li><a href="https://huggingface.co/moonshotai/Kimi-K3.1-Pro">moonshotai/ Kimi -K 3 . 1 - Pro · Hugging Face</a></li>
<li><a href="https://github.com/MoonshotAI/Kimi-K3">GitHub - MoonshotAI/ Kimi -K3: Open Frontier Intelligence · GitHub</a></li>

</ul>
</details>

**Tags**: `#open-weight models`, `#LLM release`, `#Moonshot AI`, `#model benchmarks`, `#inference providers`

---

<a id="item-tech-news-2"></a>
### [OpenAI describes cutting a thousand Linux kernel root paths](https://openai.com/index/a-thousand-fewer-paths-to-root/) ⭐️ 8.0/10

OpenAI published a post titled &quot;A thousand fewer paths to root&quot; describing work by an OpenAI team to reduce the number of privilege-escalation paths into the Linux kernel by roughly a thousand. The post&\#x27;s author confirmed in the Hacker News thread that the work is his team&\#x27;s and offered to relay questions, but the supplied material does not specify which kernel versions are affected, whether the fixes are upstreamed, or how the paths were identified. The framing is a reduction on the order of a thousand privilege-escalation routes rather than a single vulnerability fix.

hackernews · dangelosaurus · Nov 4, 23:33 · [Discussion](https://news.ycombinator.com/item?id=50372929)

**「Background」** Local privilege escalation is the Linux kernel bug class in which an ordinary local account gains root by crossing the kernel&\#x27;s privilege boundary; because containers and many services share the host kernel, a single flaw can affect many workloads. OpenAI&\#x27;s post is about an autonomous pipeline that discovers, proves exploitable, and drafts patches for such flaws at scale. According to secondary coverage, one October run reproduced 1,724 vulnerabilities and produced 948 working local privilege escalation exploits.

**「Patch review burden shifts to kernel maintainers」** Linux kernel maintainers and downstream distributions face the review, upstreaming, and backporting work for 948 generated patches; the available summary does not establish that they have been merged or backported. Because these are local privilege-escalation paths, organizations should track when fixes reach their supported kernel rather than assume the reported count has already reduced their exposure.

**「Community discussion」** Commenters turned to the systemic question: Plasmoid asked how the kernel reached a thousand privilege-escalation exploits and whether it is simply too complex to reason about or reflects a flaw in the security model, while nas said local escalation in Linux had long seemed a near-certainty but still found a cited count of 948 &quot;kind of shocking.&quot; rmbryan asked what mitigating factors keep power plants and the wider internet running despite vulnerabilities &quot;sure to exist.&quot;

<details><summary>References</summary>
<ul>
<li><a href="https://openai.com/index/a-thousand-fewer-paths-to-root/">A thousand fewer paths to root - OpenAI</a></li>
<li><a href="https://cybersecuritynews.com/openai-uncovers-948-linux-kernel-vulnerabilities/">OpenAI Cyber Model Uncovers 948 Linux Kernel Privilege ...</a></li>
<li><a href="https://explainx.ai/blog/openai-linux-kernel-948-local-privilege-escalation-exploits-1-2-million-api-cost-pipeline-patch-the-planet-2026">OpenAI Linux Kernel Pipeline: 948 Root Exploits, $1.2M ...</a></li>
<li><a href="https://openai.com/index/a-thousand-fewer-paths-to-root/">A thousand fewer paths to root - OpenAI</a></li>

</ul>
</details>

**Tags**: `#Linux kernel`, `#security`, `#privilege escalation`, `#AI-assisted vulnerability discovery`, `#OpenAI`

---

<a id="item-tech-news-3"></a>
### [AI Vulnerability Discovery Forces a Security Debt Reckoning](https://spectrum.ieee.org/ai-in-cybersecurity-php2shell-vulnerability) ⭐️ 8.0/10

An IEEE Spectrum analysis argues that AI-driven vulnerability discovery is forcing organizations to address roughly 40 years of accumulated security technical debt, using the PHP2Shell vulnerability as its central case. The article&\#x27;s claim concerns a shift in remediation pressure rather than a shipped tool or an independently measured outcome; the supplied item does not include the piece&\#x27;s evidence, PHP2Shell&\#x27;s technical details, or specific timelines.

hackernews · pseudolus · Nov 4, 11:52 · [Discussion](https://news.ycombinator.com/item?id=50364336)

**「The PHP2Shell vulnerabilities」** PHP2Shell refers to two critical PHP vulnerabilities, CVE-2026-109618 and CVE-2026-109619, that allow attackers to execute code on web servers without logging in. The PHP project&\#x27;s guidance is that updating PHP is the only complete fix, because no configuration setting fully mitigates the risk.

**「Impact」** The immediate burden falls on security teams and open-source maintainers, who face a faster-growing queue of vulnerabilities to triage and patch, with discussion commenters noting that some fixes will require restructuring rather than narrow patches.

**「Community Discussion」** Commenters split over whether AI vulnerability discovery amounts to genuine debt repayment or a compulsory “endless treadmill” of feature-neutral fix work; swatcoder argued that many issues require restructuring rather than surgical patches. xbmcuser said the shift makes real the long-assumed promise that open-source code will be audited by others.

<details><summary>References</summary>
<ul>
<li><a href="https://blog.mailfence.com/php2shell-php-vulnerability-mailfence-secure/">PHP 2 Shell Vulnerability : Your Mailfence Account Is... | Mailfence Blog</a></li>
<li><a href="https://www.dynatrace.com/news/blog/cve-2026-109618-cve-2026-109619-php2shell-critical-vulnerability-what-it-is-and-what-to-do/">PHP 2 Shell : What it is and what to do | Dynatrace news</a></li>

</ul>
</details>

**Tags**: `#AI cybersecurity`, `#technical debt`, `#vulnerability discovery`, `#open source security`

---

<a id="item-tech-news-4"></a>
### [Tencent presents Hy4 open-weight model with HyCell and HyPDE](https://hy.tencent.ai/research/hy4) ⭐️ 8.0/10

Tencent&\#x27;s Hy4 research page presents Hy4 as an open-weight foundation model that the company calls one of the strongest open-weight models available, and says Tencent is releasing two science-focused foundation models co-developed by Hy4 and Hyra 2.0: HyCell for single-cell representation and HyPDE for physical field modeling. The page also describes game-development work with Tencent Interactive Entertainment Group developers, including curated training data and evaluations for feature implementation, gameplay logic, state tracking, and asset pipelines, plus adaptations for Unreal Engine, Unity, and Godot and expanded multiplayer capabilities. Tencent acknowledges a notable gap to top proprietary models on internal benchmarks for research-level mathematics, long-horizon coding, model self-improvement, and advanced visual question answering, and says it will continue scaling pre-training and post-training to narrow that gap.

hackernews · Philpax · Nov 4, 14:11 · [Discussion](https://news.ycombinator.com/item?id=50365780)

**「Background」** Hy4 is the latest generation of Tencent&\#x27;s Hy large language model family, and the two science models released with it — HyCell for single-cell representation and HyPDE for physical field modeling — were co-developed by Hy4 and Hyra 2.0. Tencent&\#x27;s release announcement states that model weights and system cards are planned for publication in the coming days, so the open-weight framing on the research page reflects an announced release rather than a completed public download at the time of writing.

**「Self-hosting is open, but heavy」** Developers who want to avoid a hosted API can self-host Hy4: the checkpoint and an FP8 variant are released under Apache 2.0 and can be served through vLLM or SGLang, according to SiliconFlow&\#x27;s write-up. The hardware bar is steep, however — the model is reported at 770B total parameters with 49B active per token, so local deployment means a multi-GPU setup rather than a single node. Teams building game tooling also get engine-specific adaptations for Unreal Engine, Unity, and Godot, which makes those integrations the practical entry point rather than a generic chat deployment.

**「Community discussion」** Commenters welcomed the open-sourcing of science tooling, with areoform contrasting it favorably with American startups that, in their view, restrict scientific research, and frangonf praising Tencent for openly acknowledging Hy4&\#x27;s gap to top proprietary models. simonw highlighted the game-development focus and engine adaptations, while chriddyp reported that in Plotly&\#x27;s data-analytics benchmark Hy4 landed between GPT-6.1 Sol and GPT-6.1 Terra on cost/accuracy but was very slow, running roughly 26 queries per question and sometimes 64.

<details><summary>References</summary>
<ul>
<li><a href="https://hy.tencent.ai/research/hy4?langVersion=en">Tencent Hy</a></li>
<li><a href="https://www.tencent.com/tencent-launches-hy4-joining-the-ranks-of-the-worlds-leading-open-source-ai-models/">Tencent Launches Hy4, Joining the Ranks of the World&#x27;s ...</a></li>
<li><a href="https://kie.ai/blog/what-is-tencent-hy4">What Is Tencent Hy 4 ? 770B MoE, 1M Context</a></li>
<li><a href="https://www.eesel.ai/blog/tencent-hy4-pricing">Tencent Hy 4 pricing 2026: API rates, hardware cost , rivals... | eesel AI</a></li>
<li><a href="https://www.siliconflow.com/blog/tencent-hy4-preview-context-api-guide">Tencent Hy 4 Preview: 1M Context, Coding, and API Guide</a></li>

</ul>
</details>

**Tags**: `#open-weight models`, `#large language models`, `#Tencent`, `#scientific machine learning`, `#game development`

---

<a id="item-tech-news-5"></a>
### [Anthropic Reports Progress on Cryptographic Proofs for LLM Inference](https://www.anthropic.com/research/provable-inference) ⭐️ 8.0/10

Anthropic published research describing progress on cryptographic proofs for verifiable LLM inference, aimed at letting a client confirm that a provider actually ran the claimed model on its prompt. No primary source text was supplied, so the technical specifics come from commenters quoting the post: they describe a commitment of roughly 6.5 MB that covers about 16 million requests before the provider must commit again, with one proof per request and proof checking taking about 17 seconds on 24 threads \(21 seconds single-threaded\). Commenters characterize this as a significant improvement over earlier zero-knowledge results, while still carrying a large compute cost relative to ordinary inference. The work is presented as research progress rather than a deployed verification service.

hackernews · ltononro · Nov 4, 17:17 · [Discussion](https://news.ycombinator.com/item?id=50368626)

**「Background」** Cryptographic inference proofs aim to let a client verify that a stated model produced a given output without trusting the provider or rerunning the model. Anthropic&\#x27;s page compares its result with VerInf, an earlier system that proved Llama 4 Maverick, the same 400B-parameter mixture-of-experts model, at roughly 0.02 tokens per second, and with DeepProve, a peer-reviewed method that certifies an entire generated sequence in a single forward pass.

**「Practical verification cost」** Anthropic&\#x27;s reported FlashProve results put proving throughput at about 110 tokens per second on a single H100, with 19 MB proofs that verify in seconds, while a separate dense 31B model is reported at 53–77 tokens per second — so the overhead lands mostly on prover hardware rather than on the client. A commenter characterizes the overall cost as roughly a 90–100x compute hit, which would confine this to high-value, low-volume requests rather than ordinary chat serving. Deployers also inherit a freshness constraint: the weight commitment is bounded in the number of requests it covers, so providers must periodically re-commit and clients must fetch the new commitment before checking further proofs.

**「Community Discussion」** A commenter identifying as neuwirth says the work builds on VerInf, his own project as a MARS fellow, and alleges it was reused down to the choice of a 400B Maverick model with little attribution. Others argue the closed-model setting is the hard case, with nemo1618 and vessenes contending that open-weight models make verification far cheaper by simply re-running deterministic inference or cross-checking several independent providers rather than paying for zero-knowledge proofs; vintagedave notes that such checks would also catch providers silently routing requests to a different model.

<details><summary>References</summary>
<ul>
<li><a href="https://www.anthropic.com/research/provable-inference">Progress on provable inference for large language models \ Anthropic</a></li>
<li><a href="https://www.anthropic.com/research/provable-inference">Progress on provable inference for large language models \ Anthropic</a></li>

</ul>
</details>

**Tags**: `#provable inference`, `#LLM security`, `#zero-knowledge proofs`, `#AI verification`, `#open-weight models`

---

<a id="item-tech-news-6"></a>
### [Go announces encoding/json/v2, a new standard-library JSON API](https://go.dev/blog/jsonv2) ⭐️ 8.0/10

The Go project has announced encoding/json/v2, a new standard-library API for JSON handling. The change matters to Go developers and existing encoding/json users because JSON parsing and encoding are pervasive in Go services. The supplied material treats this as an announcement and does not provide a release date, compatibility guarantees, or measured performance results.

hackernews · olexsmir · Nov 4, 17:52 · [Discussion](https://news.ycombinator.com/item?id=50369106)

**「From experiment to stable」** Go first shipped \`encoding/json/v2\` and \`encoding/json/jsontext\` as experimental packages in Go 1.25, described in a September 2025 Go blog post that argued for a new major API version and explained the problems with the original \`encoding/json\`. The current post is an updated version of that introduction, and it states that after further feedback and refinement the two packages are stable and generally available in Go 1.27.

**「Impact」** Teams with existing encoding/json code should expect a migration and compatibility review; commenters specifically flag the loss of MarshalIndent as a practical cost because the v2 equivalent is more complex.

**「Community discussion」** Commenters generally welcomed encoding/json/v2, but one cited the absence of MarshalIndent as a migration pain and said the replacement code is complicated and non-obvious. Another reported using jsontext for client-specific error reporting with excellent performance, while noting that it offers no introspection.

<details><summary>References</summary>
<ul>
<li><a href="https://go.dev/blog/jsonv2">A new Go API for JSON - The Go Programming Language</a></li>
<li><a href="https://go.dev/blog/jsonv2-exp">A new experimental Go API for JSON - The Go Programming Language</a></li>

</ul>
</details>

**Tags**: `#Go`, `#JSON`, `#standard library`, `#API design`, `#software engineering`

---

<a id="item-tech-news-7"></a>
### [AMD projects Q4 revenue above Intel for the first time](https://www.tomshardware.com/pc-components/cpus/amd-expects-to-outsell-intel-in-q4-for-the-first-time-in-history-usd17b-guidance-would-exceed-intels-projections) ⭐️ 7.0/10

AMD&\#x27;s fourth-quarter guidance of roughly $17 billion would exceed Intel&\#x27;s own projection, which would make it the first quarter in which AMD&\#x27;s revenue tops Intel&\#x27;s, according to Tom&\#x27;s Hardware. The figure is a company forecast, not a reported result, and &quot;outsell&quot; here refers to revenue rather than CPU unit shipments. The report attributes part of the growth to AMD&\#x27;s Instinct accelerator sales.

hackernews · rbanffy · Nov 4, 15:38 · [Discussion](https://news.ycombinator.com/item?id=50367125)

**「Revenue rivalry」** AMD and Intel have competed for decades in x86 processors, and Intel’s broader PC and data-center business has historically given it larger quarterly revenue than AMD. The Q4 comparison is based on revenue guidance—AMD’s $17 billion projection versus Intel’s own forecast—not necessarily on unit shipments.

**「Where the growth actually comes from」** The revenue crossover is driven by accelerators rather than CPUs: AMD guided Q4 data center revenue to roughly $12.8 billion, up from $8.55 billion in Q3 2026, on the ramp of Instinct MI455X accelerators and Helios systems, inside total Q4 guidance of about $17 billion \(±3%\). Buyers should therefore read the milestone as AI-system demand rather than a shift in x86 server or client processor share, and watch MI455X/Helios supply as the variable that determines whether the projected quarter materializes.

**「Community discussion」** Commenters argued the milestone says more about Intel&\#x27;s execution problems than about an AMD breakthrough, citing Intel&\#x27;s 13th- and 14th-generation voltage issues and its abandoned Optane memory line. Others questioned how AMD&\#x27;s Epyc and Ryzen lines compare with Intel&\#x27;s Xeon and Core, noted that Instinct remains small next to Nvidia&\#x27;s accelerators, and debated whether both companies risk falling behind as Apple and Snapdragon chips pull mainstream laptops away from x86.

<details><summary>References</summary>
<ul>
<li><a href="https://www.tomshardware.com/pc-components/cpus/amd-expects-to-outsell-intel-in-q4-for-the-first-time-in-history-usd17b-guidance-would-exceed-intels-projections">AMD expects to outsell Intel in Q 4 for the first time in... | Tom&#x27;s Hardwar...</a></li>
<li><a href="https://www.techpowerup.com/354470/amd-guidance-points-to-its-first-quarter-ever-with-more-revenue-than-intel">AMD Guidance Points to Its First Quarter Ever With More Revenue ...</a></li>

</ul>
</details>

**Tags**: `#AMD`, `#Intel`, `#CPU market`, `#semiconductors`, `#AI accelerators`

---

<a id="item-tech-news-8"></a>
### [OpenAI to acquire Pierre Computer Company](https://openai.com/index/openai-to-acquire-pierre/) ⭐️ 7.0/10

OpenAI announced plans to acquire Pierre Computer Company; the linked announcement provides no purchase price, closing timeline, or regulatory conditions, so the deal is an announced intention rather than a completed acquisition. The Openai post itself contains only a pointer to a Pierre tweet, so technical detail comes from Hacker News commenters: they describe Pierre as a Git infrastructure company whose Code.Storage product stores generated code and other machine-created artifacts at scale for agentic coding services including Lovable, Bolt, Amp, Poke, Anything, and Parahelp. Commenters also identify Pierre&\#x27;s founders as Jacob Thornton and Mark Otto, the original Bootstrap developers, and point to the company&\#x27;s diffs library at diffs.com. None of those product or personnel details were confirmed in the OpenAI announcement text supplied here.

hackernews · itunpredictable · Nov 4, 15:21 · [Discussion](https://news.ycombinator.com/item?id=50366863)

**「Context」** Pierre Computer Company builds Git-based infrastructure: its Code Storage product is marketed as a way to store code and machine-generated artifacts at scale using Git. The Verge reported that OpenAI had already integrated tools from Pierre into its Codex coding platform before announcing the acquisition.

**「What it means for Code Storage users」** Code Storage is the hosted Git backend that third-party agent products — Lovable, Bolt, Amp, Poke and others, per its own site — rely on to store generated code and artifacts, and those customers now face uncertainty about whether that commercial service continues unchanged once the team is inside OpenAI. On the OpenAI side, Pierre&\#x27;s Trees and Diffs libraries are already embedded in the Codex app&\#x27;s file browsing and change review, so Codex users are affected by maintenance of code they already depend on rather than by a new capability.

**「Community discussion」** Commenters linked the acquisition to OpenAI&\#x27;s earlier &\#x27;Scaling Git at OpenAI&\#x27; engineering post and noted that Mitchell Hashimoto has publicly demoed and backed Pierre, framing the purchase as a response to Git bottlenecks in agentic coding workloads. Others were more skeptical: one joked that the industry needs a term for buying a whole company because it is cheaper than the subscription, and another asked whether labs acquiring successful developer-tool teams are also absorbing insight into how those products are built.

<details><summary>References</summary>
<ul>
<li><a href="https://www.theverge.com/openai">OpenAI | The Verge</a></li>
<li><a href="https://code.storage/">Code Storage — Git Infrastructure at Scale by The Pierre Computer ...</a></li>
<li><a href="https://code.storage/">Code Storage — Git Infrastructure at Scale by The Pierre ...</a></li>
<li><a href="https://openai.com/index/openai-to-acquire-pierre/">OpenAI to acquire Pierre Computer Company, Inc.</a></li>

</ul>
</details>

**Tags**: `#OpenAI`, `#acquisitions`, `#developer tools`, `#Git infrastructure`, `#AI coding`

---

<a id="item-tech-news-9"></a>
### [Ricursive Intelligence posts Ripple-65B-Preview dense open-weights model](https://www.reddit.com/r/LocalLLaMA/comments/1xo2arv/ricursive_intelligence_ripple65bpreview_new_dense/) ⭐️ 7.0/10

A Reddit post reports that Ricursive Intelligence has posted a preview of Ripple-65B-Preview, a 65B dense open-weights model for local and open-model users, with architecture choices including 4:1 sliding-window/global attention, an 80-layer by 5,120-dimension layout, gated attention, global NoPE, and value residuals. The post says the preview uses a standard post-training recipe of midtraining, long-context SFT, and mixed-domain RL but has had relatively light post-training focused on agentic coding; it also describes a pretrain-only checkpoint, and the poster notes that some training details appear contradictory. It claims benchmark comparisons with Muse Spark Open \(816B\) and Reflection&\#x27;s Beam \(501B\), plus Qwen3.8-27B and Qwen3.8-Flash-Next on Terminal-Bench 2.1, SWE-bench Pro, DeepSWE 1.1, IFBench, and GPQA Diamond, but these results are unverified. AtomicChat GGUFs are listed at 68.8 GB for Q8\_0 and 38.8 GB for Q4\_K\_M, with build instructions for a Ricursive llama.cpp fork.

reddit · r/LocalLLaMA · /u/returnity · Nov 4, 22:42

**「Context: another 65B dense entry」** Ricursive describes Ripple-65B-Preview as a general-purpose variant of the proprietary model behind its AI chip-design platform, pretrained on 12 trillion tokens with support for up to 1M context, according to the company&\#x27;s release page. The model card frames its comparison set as currently available US open-weight frontier models, all evaluated at full BF16 precision at maximum effort levels. The Reddit poster also notes the release lands in a size class — roughly 70B dense — that local-model users have been asking for new entries in.

**「Local deployment requires a patched build」** Running Ripple-65B-Preview locally currently means cloning llama.cpp, checking out commit 9e2a04a and applying the supplied ricursive-port.patch, since upstream support appears only as an open feature request rather than a merged change. The lighter listed quantization, Q4\_K\_M, is 38.8 GB, so users need hardware with at least that much combined RAM or VRAM to load it.

<details><summary>References</summary>
<ul>
<li><a href="https://www.ricursive.com/ripple">Recursive Self-Improvement via AI for Chip... - Ricursive Intelligence</a></li>
<li><a href="https://huggingface.co/ricursiveAI/Ripple-65B-Preview">ricursiveAI/ Ripple - 65 B - Preview · Hugging Face</a></li>
<li><a href="https://huggingface.co/AtomicChat/Ripple-65B-Preview-GGUF">AtomicChat/Ripple-65B-Preview-GGUF · Hugging Face</a></li>
<li><a href="https://github.com/ggml-org/llama.cpp/issues/31691">Feature Request: ricursiveAI/Ripple-65B-Preview support - GitHub</a></li>

</ul>
</details>

**Tags**: `#open-weight models`, `#dense LLMs`, `#LLM architecture`, `#benchmarks`, `#local LLMs`

---