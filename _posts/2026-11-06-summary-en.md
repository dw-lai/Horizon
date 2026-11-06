---
layout: default
title: "Horizon Summary: 2026-11-06 (EN)"
date: 2026-11-06
lang: en
---

> From 52 items, 8 important content pieces were selected

---

**Technology News**
1. [Claude Code Reportedly Leaks User Identifiers via Subagent Headers](#item-tech-news-1) ⭐️ 8.0/10
2. [OpenSSH auth flaw tied to crypt\(\) and musl libc](#item-tech-news-2) ⭐️ 8.0/10
3. [Obscure audio codec fits N64&\#x27;s constrained hardware](#item-tech-news-3) ⭐️ 7.0/10
4. [OpenSSH 10.6p2 Adds Critical Workaround for Alpine Without PAM](#item-tech-news-4) ⭐️ 7.0/10
5. [Baidu releases ERNIE 5.5 Flash Base amid licensing concerns](#item-tech-news-5) ⭐️ 7.0/10
6. [Delta Inference Engine v0.93 Runs DeepSeek-V4.1-Flash on One RTX 3090](#item-tech-news-6) ⭐️ 7.0/10
7. [CCORE Releases 3,918-Example Three.js/GLB 3D Dataset](#item-tech-news-7) ⭐️ 7.0/10

**Financial News**
1. [Paraguay&\#x27;s president resigns after Ueno digital bank collapse](#item-finance-news-1) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Claude Code Reportedly Leaks User Identifiers via Subagent Headers](https://github.com/anthropics/claude-code/issues/107757) ⭐️ 8.0/10

A GitHub issue reports that Claude Code subagents send user identifiers—including name, company, and email—to arbitrary websites through User-Agent headers on HTTP requests. A maintainer responding in the thread said the team became aware of the problem when it surfaced on Reddit and added a built-in plugin, \`cc-plugin-privacy\`, that deterministically blocks the behavior; it is included in version 2.1.317 and later and can be disabled via \`/plugins\`. The issue is a user report with a vendor mitigation, not an independently audited finding, and the source provides no details on which requests or sites are affected.

hackernews · motoroco · Nov 5, 22:17 · [Discussion](https://news.ycombinator.com/item?id=50385272)

**「Background」** The report centers on Claude Code&\#x27;s subagents, which construct their own outbound HTTP requests, including User-Agent strings, when performing web lookups. A maintainer comment in the thread says the team became aware of the behavior a few days earlier after it spread on Reddit and shipped a built-in \`cc-plugin-privacy\` mod to block it deterministically in version 2.1.317 and later, with an opt-out via \`/plugins\`. A separate third-party test cited in the tool results reports that the plugin blocked 10 of 23 attempts against its own README, with 8 leaks and 4 false refusals, so the mitigation&\#x27;s completeness is disputed rather than established.

**「What to Do」** Developers running Claude Code versions before 2.1.317 should upgrade to receive the privacy plugin, and those on 2.1.317+ who have disabled it via \`/plugins\` should confirm it is enabled. Users who rely on subagents making outbound HTTP requests should check whether their identifiers appear in server logs.

**「Community Reaction」** One commenter \(mk89\) attributed a recent surge in personalized spam to switching to Claude, though this is anecdotal and not evidence of causation. Another \(llama052\) shared example User-Agent strings from their own webserver logs showing subagents embedding names, company names, and repository URLs, while O\_H\_E argued the behavior reflects a broader tension in agentic coding between task persistence and deferring to the user.

<details><summary>References</summary>
<ul>
<li><a href="https://github.com/anthropics/claude-code/issues/107757">Bug Report: Privacy violation in User-Agent header · Issue ...</a></li>
<li><a href="https://dev.to/frankchu/8-leaks-pass-anthropics-23-test-email-fix-2e66">8 leaks pass Anthropic&#x27;s 23-test email fix - DEV Community</a></li>

</ul>
</details>

**Tags**: `#privacy leak`, `#Claude Code`, `#AI coding agents`, `#security`, `#User-Agent headers`

---

<a id="item-tech-news-2"></a>
### [OpenSSH auth flaw tied to crypt\(\) and musl libc](https://sshhole.com/) ⭐️ 8.0/10

A Hacker News submission linking to sshhole.com drew discussion of an OpenSSH/sshd authentication issue involving the crypt\(\) function. Commenters describe the attack goal as making sshd&\#x27;s check \`$ret = crypt\($pw, $hash\); $ret == $hash\` succeed, where \`$hash\` is the stored password setting, normally a \`$6$...\` string but \`\*\` or \`\!\` for accounts that should not be able to log in. One commenter reports that musl libc already worked around this class of failure in its crypt\_des path but not in crypt\_sha, leaving that path vulnerable. The submitted item itself is a sparse URL, so the flaw&\#x27;s full severity, affected versions, and fix status are not confirmed in the provided material.

hackernews · josemrb · Nov 5, 12:19 · [Discussion](https://news.ycombinator.com/item?id=50378228)

**「Background」** sshd verifies a password by calling crypt\(\) with the stored hash and accepting the login when the returned string equals that hash; the collision matters because musl&\#x27;s crypt\(\) uses &\#x27;\*&\#x27; to signal a hashing error, while the same &\#x27;\*&\#x27; in a password field conventionally means no usable password. Musl had already added a workaround for that sentinel collision in its DES crypt path but not in its SHA path, according to the thread&\#x27;s analysis, and the resulting OpenSSH/musl interaction affects password-disabled accounts on musl-based systems such as Alpine when PAM is not used.

**「Who is affected and what to do」** The bypass affects OpenSSH servers on musl-based Linux distributions without PAM, including Alpine Linux&\#x27;s default OpenSSH server configuration, as well as OpenWrt, Buildroot, and Yocto under certain authentication configurations. Alpine&\#x27;s advisory says systems using openssh-server-pam with UsePAM yes are not affected, while UsePAM no leaves them exposed, and locked accounts with \`\!\` in /etc/shadow cannot log in with either a password or a key. OpenSSH released version 10.6p2 on November 5, 2026 to fix the flaw, so affected operators should upgrade and check their UsePAM setting.

**「Community discussion」** Commenters attribute the bug to in-band signaling, arguing that \`\*\` should not serve both as a &quot;no password&quot; marker in /etc/passwd and as an error value in crypt\(\), and several advocate returning an explicit failure value instead of magic strings. One commenter notes musl&\#x27;s existing workaround in crypt\_des is itself incorrect when the salt is &quot;x&quot;, and that the equivalent guard was omitted from crypt\_sha.

<details><summary>References</summary>
<ul>
<li><a href="https://arstechnica.com/security/2026/11/vulnerability-allows-attackers-to-log-into-some-linux-devices-sans-password/">Meet *sshole, the vulnerability that lets hackers SSH into ...</a></li>
<li><a href="https://www.bleepingcomputer.com/news/security/openssh-flaw-lets-attackers-log-into-password-disabled-linux-accounts/">OpenSSH flaw lets attackers log into password-disabled Linux ...</a></li>
<li><a href="https://github.com/schappim/sshole-audit">GitHub - schappim/sshole-audit: Find, prove and fix *sshole ...</a></li>
<li><a href="https://www.ox.security/blog/openssh-authentication-bypass-cve-2026-123158/">OpenSSH Bypass: CVE-2026-123158 | OX Security</a></li>
<li><a href="https://alpinelinux.org/posts/2026-11-05-openssh-password-authentication-bypass/">Security advisory: openssh -server password authentication bypass</a></li>
<li><a href="https://www.bleepingcomputer.com/news/security/openssh-flaw-lets-attackers-log-into-password-disabled-linux-accounts/">OpenSSH flaw lets attackers log into password-disabled Linux accounts</a></li>

</ul>
</details>

**Tags**: `#security vulnerability`, `#OpenSSH`, `#authentication`, `#musl libc`, `#crypt`

---

<a id="item-tech-news-3"></a>
### [Obscure audio codec fits N64&\#x27;s constrained hardware](https://phoboslab.org/log/2026/11/n64-ulc-codec) ⭐️ 7.0/10

A technical write-up on phoboslab.org explores an unusual audio codec that suits the Nintendo 64&\#x27;s limited hardware, drawing attention from homebrew and demoscene readers. The article describes a decoder that nearly fills the N64&\#x27;s 4 KB RSP instruction memory \(IMEM\), a detail commenters flagged as a potential conflict with graphics workloads. The source item provides no codec name, version, benchmark, or release details, so the specific codec and its measured performance remain unverified here.

hackernews · frostbyte7 · Nov 5, 12:51 · [Discussion](https://news.ycombinator.com/item?id=50378508)

**「Background」** The N64&\#x27;s audio options were historically limited, which is the premise the author sets up before presenting the codec. The project is published as ulc64, a port of the ulc-codec to the N64, with source available on GitHub.

**「Impact」** For N64 homebrew developers, the reported near-full use of the 4 KB RSP IMEM is the key constraint: a commenter asked whether a game could still use the codec if graphics also need that memory, and the source does not resolve the question. Anyone considering the codec for an interactive title should verify how much RSP instruction space remains for other tasks.

**「Community discussion」** Commenters debated historical and practical angles: one argued the codec would have faced patent problems in 1999, citing Nintendo/Rare&\#x27;s licensing of an MP3 decoder from RAD Game Tools to shield against Fraunhofer patents, while another noted the demo&\#x27;s poor vocal quality matches the original track rather than the codec. A separate commenter suggested the codec might also fit the MAS3507D DSP&\#x27;s 1-kiloword program RAM, though they said public documentation of that program format appears to be nonexistent.

<details><summary>References</summary>
<ul>
<li><a href="https://phoboslab.org/log/2026/11/n64-ulc-codec">Why this Obscure Audio Codec is a Perfect Fit for the N64</a></li>
<li><a href="https://github.com/phoboslab/ulc64">GitHub - phoboslab/ulc64: ulc-codec on the n64 · GitHub</a></li>
<li><a href="https://github.com/phoboslab/ulc64/blob/master/README.md">ulc64/README.md at master · phoboslab/ulc64 · GitHub</a></li>

</ul>
</details>

**Tags**: `#N64`, `#audio codec`, `#homebrew`, `#demoscene`, `#constrained hardware`

---

<a id="item-tech-news-4"></a>
### [OpenSSH 10.6p2 Adds Critical Workaround for Alpine Without PAM](https://www.openssh.org/releasenotes.html#10.6p2) ⭐️ 7.0/10

OpenSSH 10.6p2 is a point release that adds a critical workaround for Alpine systems running without PAM. The release notes are the only supplied source, so the specific defect, affected code path, and exact conditions under which the workaround applies are not described here. The item does not state whether the workaround is a shipped fix or a temporary mitigation, and no independent testing is provided. Users on Alpine or other non-PAM configurations should consult the release notes directly before upgrading.

hackernews · selckin · Nov 5, 11:40 · [Discussion](https://news.ycombinator.com/item?id=50377976)

**「Background」** OpenSSH&\#x27;s portable release notes describe 10.6p2 as containing a critical security workaround for Linux systems using musl libc with PAM disabled, the configuration typical of Alpine. External coverage reports that the flaw allowed attackers to bypass sshd&\#x27;s password authentication on those systems. The item itself provides no further technical detail, so the exact mechanism and affected versions remain unconfirmed here.

**「Who must act」** Administrators of Linux hosts built on musl libc with PAM disabled — Alpine Linux being the best-known case — should upgrade to OpenSSH 10.6p2 or their distribution&\#x27;s patched package, since the flaw lets attackers bypass sshd&\#x27;s password check. Where patching must wait, disabling password authentication \(\`PasswordAuthentication no\`\) or stopping sshd removes the exposure, according to the same advisories.

**「Community Discussion」** Commenters pointed to a related writeup and to additional details from Damien Miller on the openssh-unix-dev mailing list. One commenter endorsed the stated rationale that long embargo periods are now considered dangerous because AI agents have rapidly rediscovered bugs, sometimes within hours, while another noted that white-hat researchers have long had access to embargoed information.

<details><summary>References</summary>
<ul>
<li><a href="https://www.rescana.com/post/openssh-10-6p2-alpine-musl-password-auth-bypass-prepare-now">OpenSSH 10.6p2 Fixes Critical Password Bypass on Alpine and ...</a></li>
<li><a href="https://www.privacyaffairs.com/openssh-alpine-password-bypass/">OpenSSH 10.6p2 Fixes Password Bypass on Alpine Linux</a></li>
<li><a href="https://www.rescana.com/post/openssh-10-6p2-alpine-musl-password-auth-bypass-prepare-now">OpenSSH 10.6p2 Fixes Critical Password Bypass on Alpine and ...</a></li>
<li><a href="https://www.privacyaffairs.com/openssh-alpine-password-bypass/">OpenSSH 10.6p2 Fixes Password Bypass on Alpine Linux</a></li>
<li><a href="https://www.siteguarding.com/security-blog/alpine-openssh-password-login-check/">OpenSSH 10.6p2 on Alpine: Disable SSH Password Login Now</a></li>

</ul>
</details>

**Tags**: `#OpenSSH`, `#security updates`, `#Alpine Linux`, `#vulnerability disclosure`, `#AI-assisted bug discovery`

---

<a id="item-tech-news-5"></a>
### [Baidu releases ERNIE 5.5 Flash Base amid licensing concerns](https://ernie.baidu.com/release/ernie-5-5-flash-base/) ⭐️ 7.0/10

Baidu released ERNIE 5.5 Flash Base, a base model that developers can adapt through fine-tuning or custom training. The supplied release material provides no parameter count, benchmark results, or training details, so its capabilities are not independently established. Hacker News commenters focused on licensing: one said the license forbids use in the European Union, the United Kingdom, and South Korea and makes developers responsible for preventing use by people in those places.

hackernews · pretext · Nov 5, 09:29 · [Discussion](https://news.ycombinator.com/item?id=50377078)

**「Background」** Baidu&\#x27;s ERNIE line has previously been distributed under vendor-controlled terms rather than permissive open-source licenses, so the release format matters as much as the weights. External coverage of this release describes ERNIE 5.5 Flash Base as a 280B-parameter mixture-of-experts pretraining checkpoint with 14B active parameters and a 1M-token context window, published with Baidu&\#x27;s own benchmark table and a custom license that excludes the EU, UK, and South Korea.

**「Impact」** Developers or organizations in the EU, UK, or South Korea, and anyone distributing derivatives, should verify the license before training or deployment, because a commenter says those regions are excluded and derivative developers are responsible for preventing use there; the supplied source does not include the license text.

**「Community discussion」** Commenters were divided between enthusiasm for base-model releases as a route to local customization and concern that the license is too restrictive to build on, while one asked for multi-node training frameworks such as NeMo or Hugging Face TRL with Accelerate. One commenter asserted the model is more powerful than Qwen3.8-27B and Deepseek-v4-Flash, but no benchmark evidence was supplied.

<details><summary>References</summary>
<ul>
<li><a href="https://www.llms.blog/posts/ernie-5-5-flash-base-open-weights-license">Baidu ERNIE 5.5 Flash Base: 280B Weights and License</a></li>
<li><a href="https://www.orcarouter.ai/blog/ernie-5-5-flash-base-open-weights-license">ERNIE-5.5-Flash-Base: 280B open weights, tight licence</a></li>

</ul>
</details>

**Tags**: `#large language models`, `#Baidu ERNIE`, `#base models`, `#software licensing`, `#fine-tuning`

---

<a id="item-tech-news-6"></a>
### [Delta Inference Engine v0.93 Runs DeepSeek-V4.1-Flash on One RTX 3090](https://www.reddit.com/r/LocalLLaMA/comments/1xoq4vq/deepseekv41flash1017_on_one_rtx_3090_big_updates/) ⭐️ 7.0/10

Delta Inference Engine v0.93, a Windows port of Xolotl built on Strata, adds support for 64, 96, and 128 GB RAM configurations, native reading of Unsloth quant Engram tables, and basic multi-GPU. On the author&\#x27;s single RTX 3090 24 GB setup \(i5-13600K, 4x48 GB DDR5-5600, PCIe 4.0 NVMe, Windows\), the Unsloth UD-IQ2\_XXS quant runs at the same 41 tok/s at 192 GB RAM as the previous default, while scoring 57/99 on the author&\#x27;s benchmark versus 52 for the prior ds4 Q2 and 59 for the full API model. The author reports first-token latency dropping from about 3.8 s to 2.3 s on a ~180-token prompt, and 64 GB RAM now yields 21 tok/s with UD-IQ2\_XXS. All figures are self-reported from one machine and have not been independently verified.

reddit · r/LocalLLaMA · /u/musicurgy · Nov 5, 18:23

**「Background」** Delta Inference Engine is a Windows port of Xolotl, itself formerly called Strata-DSV4.1, a project aimed at running the full 552B DeepSeek-V4.1-Flash model locally on a single gaming PC. The engine is MIT-licensed and built on Strata, and the author credits the Xolotl and Project Maya communities for work and public numbers that informed this release.

**「Practical implications」** Users with 64 GB of RAM can now run the model at reduced speed rather than being locked out, and those with 128 GB can use higher-quality quants such as UD-Q2\_K\_XL \(335 GB\) at 26.6 tok/s. The engine requires Windows 10/11, an NVIDIA GPU with at least 12 GB VRAM and driver 580 or newer, a fast NVMe SSD with 233–395 GB free for the model, and an x86-64 CPU with AVX2 as the fast path; AMD GPUs are not supported. The author notes multi-GPU scaling is weak beyond two cards and recommends Project Maya for 3–4+ GPU builds.

<details><summary>References</summary>
<ul>
<li><a href="https://github.com/Indras-Mirror/Xolotl">GitHub - Indras-Mirror/ Xolotl : Xolotl (formerly Strata -DSV4.1): run...</a></li>
<li><a href="https://ai-manual.ru/article/delta-inference-engine-v093-kak-zapustit-kvantovannuyu-deepseek-v41-flash-na-odnoj-rtx-3090/">Delta Inference Engine v0.93: как запустить... | AiManual</a></li>

</ul>
</details>

**Tags**: `#local LLM inference`, `#quantization`, `#GPU benchmarking`, `#inference engine`, `#memory optimization`

---

<a id="item-tech-news-7"></a>
### [CCORE Releases 3,918-Example Three.js/GLB 3D Dataset](https://www.reddit.com/r/LocalLLaMA/comments/1xozbe6/ccore_glb3dcoder_dataset_is_here_3918_rendered/) ⭐️ 7.0/10

The creator of CCORE GLB-3D-Coder has released the dataset used to train the 4B model, which generates 3D assets with Three.js and GLB export. The dataset contains 3,918 examples across 40 domains, including characters, creatures, vehicles, laboratory equipment, musical instruments, architecture, machinery, nature, and everyday props. Each example includes complete conversations, reasoning traces, HTML/JavaScript responses, and a rendered reference image, and the author says every example was tested and rendered with its exported GLB validated before inclusion. The release is split into 3,501 training and 417 validation examples, is MIT licensed, and is accompanied by the model and full weights.

reddit · r/LocalLLaMA · /u/ConfidentDinner6648 · Nov 6, 00:43

**「Background」** The dataset accompanies CCORE GLB-3D-Coder, a 4B coding model built on Qwen3.5-4B that generates standalone Three.js HTML/JavaScript scenes with a preview and an Export GLB button, intended for low-poly game assets and procedural scenes. The release makes the training data behind that model public, so others can fine-tune or build on the same examples rather than only using the weights.

**「Impact」** Practitioners can fine-tune or evaluate models on the MIT-licensed data, which pairs code responses with rendered reference images and validated GLB exports, and can compare results against the released 4B model weights. The author states that static assets and examples with animation and interaction are both included, so users should check which category a given example falls into before relying on it for animated output.

<details><summary>References</summary>
<ul>
<li><a href="https://huggingface.co/ccore/Qwen3.5-4B-GLB-3D-Coder">ccore /Qwen3.5-4B- GLB - 3 D - Coder · Hugging Face</a></li>
<li><a href="https://pirateface.co/ccore/Qwen3.5-4B-GLB-3D-Coder">ccore /Qwen3.5-4B- GLB - 3 D - Coder · Pirate Face</a></li>

</ul>
</details>

**Tags**: `#3D asset generation`, `#Three.js`, `#LLM fine-tuning`, `#open-source dataset`, `#GLB`

---

## Financial News

<a id="item-finance-news-1"></a>
### [Paraguay&\#x27;s president resigns after Ueno digital bank collapse](https://cointelegraph.com/news/paraguay-president-resigns-after-collapse-ueno-digital-bank?utm_source=rss_feed&amp;utm_medium=rss&amp;utm_campaign=rss_partner_inbound) ⭐️ 7.0/10

Paraguayan President Santiago Peña resigned amid scrutiny of his former ties to Ueno Bank&\#x27;s parent company after the digital lender&\#x27;s collapse left millions of customers unable to access their funds, according to Cointelegraph. The report gives no dates, official confirmation, bank-size figures, or policy response.

rss · Cointelegraph · Nov 5, 17:40

**「Background」** Paraguay&\#x27;s central bank seized Ueno Bank on Tuesday, locking an estimated 3 million customers out of their accounts and triggering protests and an impeachment bid against President Santiago Peña, who had remained a business partner of the bank&\#x27;s owner until 2025 and whose central bank chief previously ran the lender.

**「Who is affected」** Ueno&\#x27;s roughly 3 million customers, including pensioners, have had deposits frozen since Paraguay&\#x27;s central bank took over the lender on Tuesday, when its solvency ratio fell below 50% of the legal minimum. The central bank&\#x27;s takeover means deposit-guarantee rules now determine how and when those savers are repaid.

<details><summary>References</summary>
<ul>
<li><a href="https://www.arkansasonline.com/news/2026/nov/04/paraguays-central-bank-seizes-lender-with-ties-to/">Paraguay’s central bank seizes lender with ties to Peña</a></li>
<li><a href="https://www.latimes.com/world-nation/story/2026-11-03/paraguay-seizes-major-digital-bank-tied-to-president-leaving-millions-of-customers-in-limbo">Paraguay seizes major digital bank tied to president, leaving millions of...</a></li>
<li><a href="https://www.zerohedge.com/personal-finance/bank-tied-paraguays-president-just-collapsed-and-depositors-are-streets">Paraguay&#x27;s President Resigns Amid Ueno Bank Crisis... | ZeroHedge</a></li>
<li><a href="https://www.marketcollapse.com/news/ueno-bank-paraguay-what-we-know/">ueno bank Paraguay: what depositors need to know</a></li>
<li><a href="https://en.mercopress.com/2026/11/04/paraguay-takes-over-ueno-bank-with-3-million-customers-and-freezes-its-deposits">Paraguay takes over Ueno Bank, with 3 million customers, and ...</a></li>
<li><a href="https://www.hindustantimes.com/world-news/paraguay-banking-crisis-leaves-millions-locked-out-of-accounts-ueno-bank-santiago-pena-protest-101793879644459.html">‘Lost my life savings’: Paraguay banking crisis triggers ...</a></li>

</ul>
</details>

**Tags**: `#Paraguay`, `#banking crisis`, `#Ueno Bank`, `#political resignation`, `#financial stability`

---