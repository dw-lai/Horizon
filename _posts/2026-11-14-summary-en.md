---
layout: default
title: "Horizon Summary: 2026-11-14 (EN)"
date: 2026-11-14
lang: en
---

> From 37 items, 3 important content pieces were selected

---

**Technology News**
1. [llama.cpp reaches v1 with desktop apps announced](#item-tech-news-1) ⭐️ 8.0/10
2. [Live KORS airband monitor captures ATC chatter during ground stop](#item-tech-news-2) ⭐️ 7.0/10
3. [Qwen3.5-9B runs offline on stock PS4 GPU, author claims](#item-tech-news-3) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [llama.cpp reaches v1 with desktop apps announced](https://www.reddit.com/r/LocalLLaMA/comments/1xv8t2e/llamacpp_v10_is_here/) ⭐️ 8.0/10

Hugging Face&\#x27;s Merve announced that llama.cpp has released v1, saying the project will continue covering every platform and model type while keeping the inference stack robust and lean for downstream applications. The post gives no release notes, supported-platform details, API changes, or benchmark results. It also announces Llama desktop apps built on llama.cpp, intended to reduce local AI setup to a few clicks, with details linked to llama.app and a Hugging Face blog post.

reddit · r/LocalLLaMA · /u/unofficialmerve · Nov 13, 14:07

**「Background」** llama.cpp is an open-source engine for local language-model inference, and its v1.0.0 release also covers the companion ggml library. The release formalizes semantic versioning for both projects: after roughly 3.5 years of development, API and ABI incompatibilities will be reserved for major-version bumps, giving downstream app developers a clearer compatibility contract.

**「Impact」** Developers building on llama.cpp and users seeking a simpler local-AI setup have a new v1 designation and a packaged desktop-app option, but the post itself does not specify breaking changes, platform availability, or application requirements, so the linked release notes are needed before upgrading.

<details><summary>References</summary>
<ul>
<li><a href="https://huggingface.co/blog/ggml-org/llama-cpp-v1">llama.cpp v1.0.0 : A stronger foundation for the local AI ...</a></li>
<li><a href="https://tbreak.com/llama-cpp-1-0-stable-release/">llama.cpp 1.0 reaches stable release for local AI - tbreak.com</a></li>
<li><a href="https://aiweekly.co/alerts/llamacpp-ships-v100-with-semver-for-libllama-and-ggml">llama.cpp Ships v1.0.0 With Semver for libllama and ggml</a></li>

</ul>
</details>

**Tags**: `#llama.cpp`, `#local LLM inference`, `#open source`, `#GGML`, `#Hugging Face`

---

<a id="item-tech-news-2"></a>
### [Live KORS airband monitor captures ATC chatter during ground stop](https://orcasairband.com/) ⭐️ 7.0/10

During a Vancouver-area ground stop, a live airband-monitoring site at orcasairband.com published raw ATC transcripts for listeners around KORS, including exchanges on 126.400 Victoria Ground and 134.800 Vancouver Centre. The operator says the system uses an Ettus B210 receiver connected to a dual-RTX-4090 machine, with CUDA-based polyphase channelization covering the entire airband, automatic transmission detection, and removal of data transmissions before transcription. The posted transcripts were unedited and generated at posting time; one Victoria Ground excerpt is flagged as a weak signal and another contains unintelligible text, so the feed should not be treated as an authoritative operational record.

hackernews · mmaunder · Nov 13, 22:04 · [Discussion](https://news.ycombinator.com/item?id=50490593)

**「Background」** The setup uses a general-purpose software-defined radio rather than a conventional airband receiver: Ettus&\#x27;s USRP B210 tunes from 70 MHz to 6 GHz, supports up to 56 MHz of instantaneous bandwidth, and connects over USB 3.0. The project then uses that wide capture with a CUDA polyphase channelizer on two RTX 4090 GPUs to split the airband into individual channels for demodulation, transmission detection, and transcription.

**「Impact」** Because the published excerpts are raw and can be weak or unintelligible, listeners following a disruption should verify clearances and ground-stop details against official ATC or airport sources.

**「Community discussion」** One commenter said they could understand only about half of the transmissions and expressed admiration for the professionals who do, while another pointed to a 14:03 exchange in the feed in which &quot;Encore 3325&quot; confirmed a ground stop into Vancouver. A third compared the setup to a project that decodes ships’ DSC signals from public KiwiSDR receivers.

<details><summary>References</summary>
<ul>
<li><a href="https://www.ettus.com/all-products/ub210-kit/">USRP B210 USB Software Defined Radio (SDR) - Ettus Research</a></li>

</ul>
</details>

**Tags**: `#software-defined radio`, `#airband`, `#CUDA`, `#GPU signal processing`, `#ATC transcription`

---

<a id="item-tech-news-3"></a>
### [Qwen3.5-9B runs offline on stock PS4 GPU, author claims](https://www.reddit.com/r/LocalLLaMA/comments/1xvbn2m/qwen359b_running_on_a_ps4s_gpu_offline_using_its/) ⭐️ 7.0/10

An open-source project, garlic-llm, claims Qwen3.5-9B can run fully offline on a stock PS4 GPU at 31–39 tok/s, with weights repacked into custom 4- and 3-bit formats that fit in about 4.5 GiB. The author says the model&\#x27;s bundled MTP head provides the main speedup: it drafts up to two tokens that the full model checks in one pass, raising throughput from 22 tok/s. The implementation is linked on GitHub and Hugging Face, but the performance and hardware claims are self-reported on Reddit and have not been independently verified.

reddit · r/LocalLLaMA · /u/leonardo\_alegria · Nov 13, 16:00

**「Background」** Qwen3.5-9B ships with a native multi-token-prediction \(MTP\) head, a small module that proposes draft tokens for the main model to verify in one pass—the mechanism behind speculative decoding. Using that head for a speedup requires an inference engine that actually implements MTP draft-and-verify; otherwise the module sits unused. This project&\#x27;s work is wiring that MTP path into a custom offline inference stack on the PS4&\#x27;s GPU.

**「Impact」** Local-inference developers can inspect the project&\#x27;s 3/4-bit packing and MTP-based speculative decoding, but should reproduce its memory use and throughput before relying on them because the results are PS4-specific and unverified.

<details><summary>References</summary>
<ul>
<li><a href="https://ollama.com/aiconjured/Qwen3.5-9B-Uncensored-HauhauCS-Aggressive-MTP-GGUF-NVFP4">aiconjured/ Qwen 3 . 5 - 9 B -Uncensored-HauhauCS-Aggressive...</a></li>
<li><a href="https://empero.org/writing/qwythos-9b-v2">Qwythos- 9 B -v2: a 9 B that knows when to stop — Empero</a></li>

</ul>
</details>

**Tags**: `#local LLM inference`, `#speculative decoding`, `#quantization`, `#PS4 homebrew`, `#open-source project`

---