---
layout: default
title: "Horizon Summary: 2026-11-11 (EN)"
date: 2026-11-11
lang: en
---

> From 52 items, 6 important content pieces were selected

---

**Technology News**
1. [What&\#x27;s new in .NET 11 runtime: async support and compatibility changes](#item-tech-news-1) ⭐️ 9.0/10
2. [DeepMind announces AlphaProof Code for formal code verification](#item-tech-news-2) ⭐️ 8.0/10
3. [Chips and Cheese Details AMD Zen 6 Core and Memory Tradeoffs](#item-tech-news-3) ⭐️ 8.0/10
4. [Deletion Tuning Claims 0.05% Weight Mask Matches Full Fine-Tuning](#item-tech-news-4) ⭐️ 8.0/10
5. [Essay argues smart-home devices should work without internet](#item-tech-news-5) ⭐️ 7.0/10
6. [Chrome ships modern-web-guidance 1.0 to steer coding agents](#item-tech-news-6) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [What&\#x27;s new in .NET 11 runtime: async support and compatibility changes](https://learn.microsoft.com/en-us/dotnet/core/whats-new/dotnet-11/runtime) ⭐️ 9.0/10

Microsoft&\#x27;s .NET 11 runtime release notes cover runtime-level async support and compatibility changes for developers upgrading to the new release. The release notes link to Microsoft&\#x27;s .NET 11 announcement, and discussion highlights a decimal-formatting break: \`\(decimal\)0.1\` is reported as \`0.1\` on .NET 10 but \`0.1000000000000000055511151231\` on .NET 11.

hackernews · stevefan1999 · Nov 10, 12:20 · [Discussion](https://news.ycombinator.com/item?id=50439284)

**「Background」** Until now, the C\# compiler has translated \`async\` methods into generated state-machine types, so the runtime itself only saw ordinary methods. .NET 11&\#x27;s runtime async instead builds async support into the runtime; Microsoft&\#x27;s Preview 1 release notes describe it as a major .NET 11 feature intended to improve tooling and performance for async-heavy code paths, and the async profiler now instruments both runtime-async and compiler-generated state-machine methods under one event model.

**「Upgrade check」** Teams upgrading existing applications should add targeted regression tests rather than treating .NET 11 as a drop-in runtime: runtime async takes a significant step toward replacing compiler-generated state machines with runtime-managed suspension and resumption, and a commenter reports that \`\(decimal\)0.1\` now yields \`0.1000000000000000055511151231\` instead of \`0.1\`, so async-heavy and decimal-sensitive code paths both need re-checking.

**「Community Discussion」** Commenters were impressed by runtime async, with one surprised that moving async handling into the runtime could preserve equivalent performance while improving stack traces. Others argued C\#/.NET remains underappreciated because of outdated Windows-only and pre-.NET Core perceptions, and one commenter pointed to \`dotnetup\` as an official .NET version manager.

<details><summary>References</summary>
<ul>
<li><a href="https://learn.microsoft.com/en-us/dotnet/core/whats-new/dotnet-11/runtime">What&#x27;s new in .NET 11 runtime | Microsoft Learn</a></li>
<li><a href="https://github.com/dotnet/core/blob/main/release-notes/11.0/preview/preview1/runtime.md">core/release-notes/11.0/preview/preview1/runtime.md at main ...</a></li>
<li><a href="https://learn.microsoft.com/en-us/dotnet/core/whats-new/dotnet-11/runtime">What&#x27;s new in . NET 11 runtime | Microsoft Learn</a></li>

</ul>
</details>

**Tags**: `#.NET 11`, `#C\#`, `#runtime`, `#async`, `#compatibility`

---

<a id="item-tech-news-2"></a>
### [DeepMind announces AlphaProof Code for formal code verification](https://deepmind.google/blog/introducing-alphaproof-code/) ⭐️ 8.0/10

DeepMind has announced AlphaProof Code, an AI proof agent intended to help formally verify code, according to the item title and Hacker News discussion. The supplied material does not include the announcement post, so the supported proof assistants, availability, benchmark results, and exact scope of the verification are unconfirmed. The item provides no evidence that the system is generally available or has been independently evaluated.

hackernews · ilreb · Nov 10, 12:11 · [Discussion](https://news.ycombinator.com/item?id=50439193)

**「What machine-checked proofs establish」** Formal verification means proving that a program meets a written specification, with a proof assistant such as Lean checking every deduction mechanically rather than relying on tests or review. A successful proof therefore rules out implementation bugs relative to the stated specification, but says nothing about whether the specification itself captures the intended security property. AlphaProof Code, as described in coverage of the announcement, is a multi-LLM agent framework that splits this work: humans and models turn security goals into formal specifications that human experts review, after which Gemini-powered agents generate the Lean proofs that the checker validates.

**「Impact」** For teams applying such a tool, the discussion points to a concrete verification gap: proofs can show that code satisfies stated theorems without establishing that those theorems capture the intended behavior, so specification and theorem review remain necessary.

**「Community discussion」** Commenters questioned a reported zero-bug verification result as implausible unless the theorems were narrow or incorrect, and noted that the agent appears to check implementations rather than challenge specifications. One commenter also reported a coding agent producing a passing test suite for a refactor implemented backwards, illustrating how validation can succeed against the wrong properties.

<details><summary>References</summary>
<ul>
<li><a href="https://explainx.ai/blog/google-deepmind-alphaproof-code-signal-protocol-formal-verification-2026">AlphaProof Code: Signal Protocol Verified in 4 Weeks ...</a></li>
<li><a href="https://codingislove.com/alphaproof-code-signal/">DeepMind&#x27;s AlphaProof Code formally verifies Signal&#x27;s ...</a></li>

</ul>
</details>

**Tags**: `#AlphaProof`, `#formal verification`, `#AI proof agents`, `#Lean/Rocq`, `#DeepMind`

---

<a id="item-tech-news-3"></a>
### [Chips and Cheese Details AMD Zen 6 Core and Memory Tradeoffs](https://chipsandcheese.com/p/amds-zen-6-family-feeding-the-beast) ⭐️ 8.0/10

Chips and Cheese has published a microarchitectural analysis of AMD&\#x27;s Zen 6 CPU family, focused on how the cores are fed: branch prediction, vector load throughput, and the memory subsystem. Details quoted and discussed by commenters describe integer multiply units dropping from three to two and PDEP/PEXT throughput falling from three to two instructions per cycle, while the core supports four vector loads per cycle at 256 bits or narrower and adds VNNI pipes; the two-ahead branch predictor carries over from Zen 5. Commenters also say consumer AM5 Zen 6 parts are expected to use a new I/O chiplet on a smaller node, a change they hope will improve the memory controller. The piece is an architecture analysis rather than an AMD launch, and the supplied material contains no measured Zen 6 performance results.

hackernews · pixelpoet · Nov 10, 17:02 · [Discussion](https://news.ycombinator.com/item?id=50443090)

**「Predecessor context」** Zen 6 and its density-focused Zen 6c sibling follow AMD&\#x27;s Zen 5 and Zen 5c cores, which shipped in the EPYC 9005 &quot;Turin&quot; family; the new cores debut in the EPYC 9006 &quot;Venice&quot; line. The Chips and Cheese analysis frames its examination around what changed from Zen 5 and what the split between Zen 6 and Zen 6c reveals about AMD&\#x27;s microarchitectural priorities.

**「Why It Matters」** For AM5 builders, the I/O die is the practical item to watch: one commenter reports that Zen 4 and Zen 5&\#x27;s existing memory controller struggles to exceed 3600 MT/s when both memory channels are populated, and expects the smaller-node I/O chiplet to raise that ceiling. That expectation is not yet supported by measured Zen 6 memory results in the supplied material.

**「Community Discussion」** Commenters pressed on the tradeoffs: one asked whether PDEP/PEXT share circuitry with integer multiply or whether the two throughput reductions are independent, and another speculated that cutting a multiplier may free die area for the VNNI pipes. Others highlighted the 32-core C-core chiplet with more L3 cache and questioned how 32 cores in a single CCD would be grouped below the NUMA level, while one wondered whether the four vector loads per cycle finally make gather performance acceptable.

<details><summary>References</summary>
<ul>
<li><a href="https://chipsandcheese.com/p/amds-zen-6-family-feeding-the-beast">AMD ’ s Zen 6 Family : Feeding the Beast - by George Cozma</a></li>
<li><a href="https://wccftech.com/amd-zen-6-architecture-ipc-cores-memory-performance-epyc-venice/">AMD Zen 6 Architecture Brings A Phenomenal 27% IPC Increase Over...</a></li>

</ul>
</details>

**Tags**: `#AMD Zen 6`, `#CPU architecture`, `#microarchitecture`, `#memory controller`, `#branch prediction`

---

<a id="item-tech-news-4"></a>
### [Deletion Tuning Claims 0.05% Weight Mask Matches Full Fine-Tuning](https://www.reddit.com/r/LocalLLaMA/comments/1xswmb7/the_surprising_effectiveness_of_deleting_weights/) ⭐️ 8.0/10

A study reports that Deletion Tuning, which learns a binary mask zeroing less than 0.05% of a transformer LLM&\#x27;s gate-projection weights and changes nothing else, matches full fine-tuning across reinforcement learning with verifiable rewards, supervised fine-tuning, and on-policy distillation. The authors report that the stored masks are hundreds to thousands of times smaller than FFT checkpoints and that prior-task retention is much better: under reinforcement learning, accuracy stays near the base model while FFT, LoRA, and random sparse fine-tuning lose up to 5.4 points. They release code and trained masks on GitHub and Hugging Face, plus a blog post and NeurIPS 2026 poster. These are single-paper claims that have not been independently verified.

reddit · r/LocalLLaMA · /u/Thrumpwart · Nov 10, 19:44

**「Background」** Post-training methods such as supervised fine-tuning, RLVR, and on-policy distillation normally adapt a pretrained LLM by updating all weights or by training a parameter-efficient adapter such as LoRA. An earlier OpenReview posting of this work, dated May 26, 2026, called the approach Bit-Mask Tuning and reported that a learnable binary keep/zero mask over gate projections was several thousand times smaller than a full checkpoint while retaining prior-task accuracy as model size rose from 0.5B to 8B; the current report recasts the method as Deletion Tuning and extends the claim to matching full fine-tuning across the three post-training regimes.

**「Impact」** Teams doing repeated post-training could preserve each step as a tiny gate-projection mask instead of a full FFT checkpoint, while potentially avoiding the loss of earlier skills reported for FFT, LoRA, and random sparse fine-tuning. Adoption should still depend on independent replication and on confirming parity and retention on the team&\#x27;s own models and tasks.

<details><summary>References</summary>
<ul>
<li><a href="https://openreview.net/forum?id=JnfolztAV3">The Surprising Effectiveness of Deleting Weights in LLM ...</a></li>

</ul>
</details>

**Tags**: `#LLM fine-tuning`, `#sparse masks`, `#continual learning`, `#reinforcement learning`, `#model efficiency`

---

<a id="item-tech-news-5"></a>
### [Essay argues smart-home devices should work without internet](https://docodethatmatters.com/home-automation-overnight-success/) ⭐️ 7.0/10

An essay at docodethatmatters.com argues that smart-home devices should keep working without internet access, treating local operation as a requirement rather than a cloud-dependent add-on. No product, version, or standard is announced, and no measured result or vendor commitment is supplied. The discussion’s concrete reference points are Home Assistant’s “IoT Class” ratings—from “Local Push” to “Cloud Polling”—and local protocols such as Zigbee and Z-Wave.

hackernews · skittleson · Nov 10, 15:25 · [Discussion](https://news.ycombinator.com/item?id=50441707)

**「How local-first is classified」** Home Assistant, the open-source smart-home platform that commenters reference, assigns each integration an &quot;IoT Class&quot; describing how it talks to devices, ranging from local push and local polling to cloud push and cloud polling, with the cloud classes requiring an active internet connection. That label is the vocabulary the discussion uses to separate devices that keep working offline from those that depend on a vendor&\#x27;s cloud service.

**「Impact」** For buyers who adopt the essay’s local-only requirement, the practical consequence is a narrower hardware list and a new purchasing check: whether the device works without its vendor’s cloud and whether its Home Assistant integration is rated “Local Polling” or better, with “Local Push” preferred.

**「Community discussion」** Hacker News commenters describe long-running local setups—including an X10/Insteon system controlled through Indigo and SecuritySpy—and stricter buying rules favoring Zigbee/Z-Wave or Wi-Fi devices with open-source or replaceable firmware. One commenter reports using cheap hardware plus LLM-assisted local firmware, while another pushes back by asking people to use a first draft or refine code themselves without LLMs.

<details><summary>References</summary>
<ul>
<li><a href="https://developers.home-assistant.io/docs/creating_integration_manifest/">Integration manifest | Home Assistant Developer Docs</a></li>
<li><a href="https://github.com/home-assistant/architecture/discussions/1426">The current iot class system in Home Assistant doesn&#x27;t show the full...</a></li>

</ul>
</details>

**Tags**: `#smart home`, `#local-first`, `#IoT`, `#Home Assistant`, `#privacy`

---

<a id="item-tech-news-6"></a>
### [Chrome ships modern-web-guidance 1.0 to steer coding agents](https://github.com/GoogleChrome/modern-web-guidance) ⭐️ 7.0/10

Google Chrome, in collaboration with Firefox, MDN, and Edge, released version 1.0 of modern-web-guidance, an open-source collection of more than 200 guides \(about 1.7 MB\) intended to steer coding agents toward native web primitives such as &lt;dialog&gt;, showModal\(\), field-sizing, and CSS.highlights instead of older div-plus-JavaScript patterns. It is distributed as an agent skill and a pure-JavaScript Agentic RAG CLI \(about 7 MB, with roughly 10 ms local search\), installable through npx, and includes a deterministic legacy-scan trained on 30,000 GitHub repositories; the team claims 92% average precision on held-out repositories. The project also reports an evaluation across 200 tasks and about 1,700 Playwright/AST assertions in which the agents it names—Codex, Claude, and &quot;agy&quot;—improved from 55% pass unguided to 92% guided. These performance figures are vendor claims and were not independently verified in the supplied material.

hackernews · paulirish · Nov 10, 18:01 · [Discussion](https://news.ycombinator.com/item?id=50443812)

**「Background」** Coding agents often reproduce patterns common in their training data, including older JavaScript and div-based UI approaches, even when browsers now provide native alternatives. Chrome&\#x27;s project packages curated guidance as an agent skill and searchable CLI because models may recognize features such as &lt;dialog&gt; and field-sizing by name but do not consistently default to using them.

**「Compatibility checks still required」** Developers using the skill may get faster modernization suggestions from their coding agents, but they should still verify each change against their target browsers. A commenter reported that several recommended features, including \`CSS @function\` and \`scrollsnapchange\`, are stable in Chrome but unsupported in Firefox and Safari, so teams shipping cross-browser code should gate agent rewrites on compatibility data.

**「Community discussion」** One commenter listed browser features they said the skills will direct agents to use that are stable in Chrome but unsupported in Firefox and Safari, including CSS @function, calc-size\(\), corner-shape, text-fit, and container scroll-state queries. Another argued that the project gives Chrome too much influence over how LLMs write for the web, warning of a return to &quot;view in \[dominant browser\]&quot; messaging, while a separate suggestion was to publish a grep-friendly Markdown index on GitHub Pages so agents can use the guides without installing anything.

<details><summary>References</summary>
<ul>
<li><a href="https://developer.chrome.com/docs/modern-web-guidance">Modern Web Guidance | Chrome for Developers</a></li>

</ul>
</details>

**Tags**: `#coding agents`, `#web platform`, `#browser APIs`, `#developer tooling`, `#open source`

---