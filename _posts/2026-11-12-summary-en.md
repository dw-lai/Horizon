---
layout: default
title: "Horizon Summary: 2026-11-12 (EN)"
date: 2026-11-12
lang: en
---

> From 59 items, 11 important content pieces were selected

---

**Technology News**
1. [Voltage glitching unlocks disabled A100 resources on CMP 170HX](#item-tech-news-1) ⭐️ 8.0/10
2. [AWS publishes aws-emulator, a Rust-based local AWS test tool](#item-tech-news-2) ⭐️ 7.0/10
3. [United Airlines Bans AI Agents From Booking Flights for Travelers](#item-tech-news-3) ⭐️ 7.0/10
4. [Tim Peters, author of the Zen of Python, has died](#item-tech-news-4) ⭐️ 7.0/10
5. [False smoke alarm nearly overwhelmed Jane Street&\#x27;s only NYC datacenter](#item-tech-news-5) ⭐️ 7.0/10
6. [WSJ headline claims Nvidia is preparing to oust CEO Jensen Huang](#item-tech-news-6) ⭐️ 7.0/10
7. [Blog Post Asks Whether Linear Programming Can Edit Model Weights](#item-tech-news-7) ⭐️ 7.0/10
8. [Google launches Gemini Decisions API with multimodal Gemini Decision 1](#item-tech-news-8) ⭐️ 7.0/10
9. [Anthropic details multi-chip Claude strategy across four chip families](#item-tech-news-9) ⭐️ 7.0/10

**Financial News**
1. [CoreWeave shares jump 15% premarket on Q3 revenue beat](#item-finance-news-1) ⭐️ 7.0/10
2. [Bitmine reports $6.3 billion net loss for fiscal 2026](#item-finance-news-2) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Voltage glitching unlocks disabled A100 resources on CMP 170HX](https://blog.kate.land/posts/using-voltage-glitching-to-unlock-the-a100/) ⭐️ 8.0/10

For owners of the 8 GB NVIDIA CMP 170HX mining card, a hardware hacker&\#x27;s write-up documents a voltage fault-injection method that bypasses fuse locks and exposes around 80 GB of onboard HBM plus 120–126 working SMs, compared with 108 SMs on a retail A100. She reports 85.9 TFLOP/s FP16 and restored NVLink and PCIe Gen4, with the full 80 GB usable for inference on cards whose HBM is intact; these are her measurements from modified hardware, not an independently verified or vendor-supported capability. The procedure is not a software toggle: it requires board wiring, a custom STM32 glitcher, and 1–48 hours of glitching per card, and one of her ten cards had only 64 GB intact, so brick risk and card-to-card variation remain.

hackernews · lae · Nov 11, 10:48 · [Discussion](https://news.ycombinator.com/item?id=50451903)

**「Background」** NVIDIA&\#x27;s CMP 170HX is a GA100-based mining card sold in 8 GB and 10 GB HBM2e configurations, according to TechPowerUp&\#x27;s GPU database. The 8 GB version is the subject here because its board reportedly carries far more HBM than its retail configuration exposes, leaving a fuse-enforced memory limit as the obstacle.

**「Impact」** CMP 170HX owners and hardware-security researchers now have a documented but non-productized route to recovering disabled HBM and compute; anyone attempting it should treat bricking as a risk and cannot assume the full 80 GB is intact, since one of the ten cards tested had only 64 GB.

**「Community discussion」** Commenters debated whether the disabled HBM and SMs reflect market segmentation or fabrication faults, with one arguing the fuses may have been used because some dies could not meet full A100 specifications. Another reported two weeks of failed software-only attempts to unlock 80 GB and called the fuse-bypass route riskier, while noting the 10 GB CMP 170HX had previously exposed 80 GB but not full CUDA access.

<details><summary>References</summary>
<ul>
<li><a href="https://www.techpowerup.com/gpu-specs/cmp-170hx-8-gb.c3830">NVIDIA CMP 170HX 8 GB Specs | TechPowerUp GPU Database</a></li>
<li><a href="https://www.techpowerup.com/gpu-specs/cmp-170hx-10-gb.c3957">NVIDIA CMP 170HX 10 GB Specs | TechPowerUp GPU Database</a></li>
<li><a href="https://pcpartvalue.com/gpu/nvidia-cmp-170hx-8-gb-ga100-8-gb-2021">CMP 170HX 8 GB GA100 | HBM2e | 8 GB Used Price: What Is It ...</a></li>

</ul>
</details>

**Tags**: `#voltage glitching`, `#GPU hardware hacking`, `#NVIDIA A100`, `#hardware security`, `#reverse engineering`

---

<a id="item-tech-news-2"></a>
### [AWS publishes aws-emulator, a Rust-based local AWS test tool](https://github.com/aws/aws-emulator) ⭐️ 7.0/10

AWS has published aws-emulator, a Rust-based local emulator of AWS services intended to let developers run tests without provisioning paid cloud resources. The project description cites 29,684 commits during its first three weeks, and a guest post by Swaminathan Sivasubramanian on Werner Vogels&\#x27; blog describes it as built by autonomous AI agents. On macOS and Windows it currently requires Docker, and its security documentation warns against using it to test IAM policies and permissions boundaries, resource-based policies such as bucket policies, KMS key policies, cross-account or cross-Region access, or other security controls; some IAM evaluation is supported but differs from AWS. Whether AWS will maintain the emulator as a supported product is not clear from the supplied material.

hackernews · super\_linear · Nov 11, 18:21 · [Discussion](https://news.ycombinator.com/item?id=50456631)

**「Prior local-cloud tooling」** Developers testing against AWS APIs without provisioning real cloud resources have relied on third-party local emulators rather than official AWS software. This release is AWS&\#x27;s own emulator, written in Rust, and it currently requires Docker to run on macOS and Windows rather than shipping as a standalone binary.

**「Security-testing limits」** Teams can use the free, open-source emulator to run local tests with the same CLI and SDK commands, but it should not replace security validation: AWS&\#x27;s guidance says not to use it for IAM policies and permissions boundaries, resource-based or KMS key policies, cross-account or cross-Region access, or other security controls. Keep real-AWS checks for those paths, and note that macOS and Windows users currently need Docker.

**「Community discussion」** Commenters questioned whether the emulator is a real, maintained AWS product rather than an exercise; one recommended Floci and Testcontainers as alternatives, noting limited use of Testcontainers for GCP and Azure. Another commenter highlighted the security documentation&\#x27;s warning that IAM policies, resource-based and KMS key policies, and cross-account or cross-Region access should not be tested, while a self-identified Amazon employee said the project would be valuable if properly maintained.

<details><summary>References</summary>
<ul>
<li><a href="https://aws.amazon.com/blogs/aws/test-your-applications-against-aws-locally-with-aws-emulator/">Test your applications against AWS locally with AWS Emulator</a></li>

</ul>
</details>

**Tags**: `#AWS`, `#cloud emulation`, `#AI agents`, `#open source`, `#developer tooling`

---

<a id="item-tech-news-3"></a>
### [United Airlines Bans AI Agents From Booking Flights for Travelers](https://www.cbsnews.com/news/united-airlines-bans-ai-agents-booking-flights/) ⭐️ 7.0/10

United Airlines has banned AI agents from booking flights on travelers’ behalf, according to a CBS News report. The available summary does not detail the policy’s effective date, enforcement mechanism, or any exceptions for travel agencies or API partners. It also leaves unclear how United will distinguish agent-driven bookings from ordinary customer activity.

hackernews · herpderperator · Nov 11, 21:24 · [Discussion](https://news.ycombinator.com/item?id=50458900)

**「Background」** United&\#x27;s policy separates a traveler&\#x27;s authorization of an AI agent from the airline&\#x27;s permission for that agent to act; reservations touched by unauthorized AI agents may be canceled without notice and loyalty benefits revoked, leaving airline-approved integrations as the only sanctioned automation path. Coverage of the terms notes that their broad wording could also affect award-search tools, not only the final booking step.

**「Impact」** Travelers who rely on AI agents cannot assume a United itinerary can be completed end to end; they may need a manual handoff to finish booking. Developers building booking agents should treat United as a restricted target and verify permitted access paths before promising automated United bookings.

**「Community Discussion」** Commenters questioned whether such a ban is technically enforceable, with one describing browser-based computer-use agents as difficult to block and another arguing that flight booking is a poor fit for automation because it is already fast and users want control over seat and itinerary choices. One suggested using agents for fare search but booking through a travel agency that offers an API.

<details><summary>References</summary>
<ul>
<li><a href="https://onemileatatime.com/news/united-airlines-bans-ai-agents-protect-customers/">United Airlines Bans “AI Agents,” Claims It’s To “Protect ...</a></li>
<li><a href="https://www.unite.ai/united-airlines-bars-unauthorized-ai-agents-from-booking-travel/">United Airlines Bars Unauthorized AI Agents From Booking ...</a></li>

</ul>
</details>

**Tags**: `#AI agents`, `#airline policy`, `#automation`, `#terms of service`, `#bot detection`

---

<a id="item-tech-news-4"></a>
### [Tim Peters, author of the Zen of Python, has died](https://discuss.python.org/t/in-memoriam-tim-peters-1952-2026/110028) ⭐️ 7.0/10

Tim Peters, a widely respected Python community figure and the author of the Zen of Python, has died, according to a Python Discourse post titled “In Memoriam: Tim Peters \(1952–2026\).” The supplied post links to a Reddit r/Python thread and gives no cause of death or further biographical detail. Commenters pointed to \`import this\`, which prints the Zen, and to his work on the SpamBayes spam filter and the second edition of the Python Cookbook.

hackernews · ayhanfuat · Nov 11, 07:03 · [Discussion](https://news.ycombinator.com/item?id=50450488)

**「Context: the Zen of Python and CPython」** Peters is best known for the Zen of Python, the set of design aphorisms he wrote that was adopted as entry 20 in the language&\#x27;s official Python Enhancement Proposals and is embedded in the interpreter as an Easter egg, displayed by typing \`import this\`. He was also a longtime CPython core developer and the designer and implementer of the Timsort algorithm. The Python forum&\#x27;s memorial thread notes that he found Python soon after its initial release and that one of his first contributions was convincing the project that Python should support mixed arithmetic between int and float.

**「Community discussion」** Commenters remembered Peters affectionately as “Uncle Timmy” and described learning from his Usenet and python-dev posts. Another credited him, alongside Gary Robinson, with turning Paul Graham’s “A Plan for Spam” essay into SpamBayes, while an edit added Robert Woodhead to the credit and raised uncertainty about other implementors.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Zen_of_Python">Zen of Python - Wikipedia</a></li>
<li><a href="https://grokipedia.com/page/Tim_Peters_%28software_engineer%29">Tim Peters (software engineer) — Grokipedia</a></li>
<li><a href="https://discuss.python.org/t/in-memoriam-tim-peters-1952-2026/110028">In Memoriam: Tim Peters 1952–2026 - Core Development...</a></li>

</ul>
</details>

**Tags**: `#Python`, `#open source community`, `#obituary`, `#software engineering`, `#programming culture`

---

<a id="item-tech-news-5"></a>
### [False smoke alarm nearly overwhelmed Jane Street&\#x27;s only NYC datacenter](https://michael.bacarella.com/2026/11/10/false-smoke-alarm-jane-street-datacenter/) ⭐️ 7.0/10

An incident account describes how a false smoke alarm nearly overwhelmed Jane Street&\#x27;s only New York City datacenter, focusing on the emergency shutdown and fire-safety decisions it triggered. The piece is a first-person operational narrative, not a vendor announcement or an independently measured postmortem; the supplied item does not include the article text, so alarm, suppression, and power-system specifics remain unverified.

hackernews · mbac32768 · Nov 11, 16:38 · [Discussion](https://news.ycombinator.com/item?id=50455394)

**「Background」** Data-center fire-safety systems often link smoke detection to suppression and equipment shutdown, while cooling equipment may also stop on an alarm. In the Jane Street account, a false smoke alarm left the facility without cooling and sent staff scrambling to cut power before sprinklers could discharge, turning an alarm into a race against heat and water damage.

**「Impact」** For Jane Street, the incident account shows that a false alarm at its only NYC datacenter has no same-city failover, so responders must rely on local shutdown procedures rather than shifting load to another New York site.

**「Community Discussion」** Commenters debated fire-safety automation: one argued that a datacenter should have a physical emergency power off button and a smoke-alarm interlink, while another said the CRAC units they work with are deliberately not shut down on smoke alarm because the International Mechanical Code permits an air handler over 2,000 cfm serving one space to keep running. A third commenter described being the nearby employee who gets called in to shut down servers during off-hours incidents.

<details><summary>References</summary>
<ul>
<li><a href="https://michael.bacarella.com/2026/11/10/false-smoke-alarm-jane-street-datacenter/">How a false smoke alarm almost drowned Jane Street ’s only NYC ...</a></li>

</ul>
</details>

**Tags**: `#datacenter operations`, `#incident response`, `#fire safety systems`, `#infrastructure resilience`, `#Jane Street`

---

<a id="item-tech-news-6"></a>
### [WSJ headline claims Nvidia is preparing to oust CEO Jensen Huang](https://www.wsj.com/business/nvidia-is-preparing-to-oust-nvidia-ceo-jensen-huang-30f421ad) ⭐️ 7.0/10

A Wall Street Journal headline submitted to Hacker News says Nvidia is preparing to remove CEO Jensen Huang, but the item provides no article text, sourcing details, or company confirmation. No timetable, successor, or board action is described, leaving the report unverified. The claim concerns Nvidia&\#x27;s long-serving CEO and would be material to investors and AI-hardware customers if confirmed, but the supplied material does not establish that any leadership change has occurred.

hackernews · jbredeche · Nov 11, 22:31 · [Discussion](https://news.ycombinator.com/item?id=50459703)

**「Background」** The linked Wall Street Journal headline, echoed by Techmeme, says Nvidia&\#x27;s board is preparing to oust CEO Jensen Huang. The item provides no article body or Nvidia confirmation; the Hacker News thread debates unverified allegations about Huang&\#x27;s personal conduct and China sales rather than a disclosed board vote or succession plan.

**「Community Discussion」** Commenters debate Huang&\#x27;s centrality to Nvidia, with one arguing that his early support for CUDA and GPU computing made the company&\#x27;s AI position possible, while others argue that unverified allegations about his conduct and export compliance make his position untenable. The thread offers no independent confirmation of the reported ouster.

<details><summary>References</summary>
<ul>
<li><a href="https://www.techmeme.com/261111/p44">Sources: Nvidia &#x27;s board is preparing to oust Jensen Huang and is...</a></li>
<li><a href="https://news.ycombinator.com/item?id=50459703">Nvidia Is Preparing to Oust Nvidia CEO Jensen Huang | Hacker News</a></li>

</ul>
</details>

**Tags**: `#Nvidia`, `#Jensen Huang`, `#corporate governance`, `#AI hardware`, `#semiconductor industry`

---

<a id="item-tech-news-7"></a>
### [Blog Post Asks Whether Linear Programming Can Edit Model Weights](https://nathan.rs/posts/weight-space-lp/) ⭐️ 7.0/10

A blog post at nathan.rs asks whether linear programming can perform weight-space programming for neural-network model editing, an approach that changes weights directly. The supplied material describes an exploratory analysis rather than a demonstrated capability, reporting no benchmark results, released code, or evidence about performance on large models.

hackernews · emschwartz · Nov 11, 12:30 · [Discussion](https://news.ycombinator.com/item?id=50452655)

**「Background」** Weight-space programming is an approach in which a general-purpose LLM reads, interprets, and directly writes another neural network&\#x27;s weights, without gradient descent or a training loop. The post examines a prior MIT CSAIL weight-space edit to Qwen3.5-0.8B that fixed thinking loops; a summary of the post says its hand-tuned search can be formulated as a linear program matching the original on MATH-500, GSM8K, and IFEval while changing 8× fewer weights.

**「Community discussion」** Commenters treated the post as a practical recipe rather than a finished result: jsw97 argued LP solvers could guide weight edits by imposing constraints to eliminate or preserve behaviors, while dansitu said the simplicity suggests such edits should happen during training through regularization. mirekrusin proposed extending the idea to weight-space distillation, and bcmyguest asked how far it would scale to larger models with multi-variate rewards.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Weight-space_programming">Weight-space programming - Wikipedia</a></li>
<li><a href="https://proomt.com/item/can-a-linear-program-do-weight-space-programming-d1a13007-a589-44d0-b87e-067ea543171c">Can a Linear Program Do Weight-Space Programming? · proomt</a></li>

</ul>
</details>

**Tags**: `#linear programming`, `#weight-space editing`, `#large language models`, `#model steering`, `#optimization`

---

<a id="item-tech-news-8"></a>
### [Google launches Gemini Decisions API with multimodal Gemini Decision 1](https://simonwillison.net/2026/Nov/11/gemini-decisions-api/) ⭐️ 7.0/10

Google has launched the Gemini Decisions API and the Gemini Decision 1 model, letting developers ask yes/no, choice, and rubric-scoring questions through an API category already occupied by Jev and OpenAI. Gemini Decision 1 accepts text, images, audio, video, and PDFs, whereas Jev is text- and JSON-only and OpenAI&\#x27;s decision model handles text and images. It is priced at 10 cents per million input tokens with free output, matching GPT-6 Luna and above Jev&\#x27;s 4.2 cents per million; in Simon Willison&\#x27;s video test, yes/no answers came back as probabilities such as 0.92 rather than the 1.0 or 0.0 returned by Jev and OpenAI.

rss · Simon Willison · Nov 11, 22:03

**「Background」** Decision-model APIs are designed to return structured judgments about supplied content—yes/no answers, one of several choices, or rubric scores—rather than open-ended prose. Google is entering a category where Jev had already established those three question types and OpenAI had introduced a competing decision model supporting text and images.

**「Impact」** Developers can send video, audio, and PDFs directly for decisions instead of adding a separate transcription or extraction step, but yes/no results must be thresholded because Gemini returns probabilities rather than binary values. Teams comparing the three APIs also face a higher input price than Jev&\#x27;s 4.2 cents per million tokens, though Gemini&\#x27;s output is free.

**Tags**: `#Gemini Decisions API`, `#Google AI`, `#decision models`, `#multimodal AI`, `#API pricing`

---

<a id="item-tech-news-9"></a>
### [Anthropic details multi-chip Claude strategy across four chip families](https://simonwillison.net/2026/Nov/11/anthropic-ipo-roadshow/) ⭐️ 7.0/10

Anthropic&\#x27;s IPO roadshow video gives investors and AI-infrastructure teams previously unreleased detail on how the company trains and serves Claude across AWS Trainium, Google TPUs, NVIDIA GPUs, and AMD GPUs. Co-founder Tom Brown says a first-time AMD deployment was brought up in three days with &quot;basically no human intervention,&quot; with a system called Mythos trying it and Claude writing or porting almost 100% of the kernels; these are Anthropic&\#x27;s roadshow claims, not independently verified results. Brown also describes &quot;total effective compute&quot; as physical capacity multiplied by discovered compute multipliers and says Anthropic expects Claude eventually to discover those multipliers itself.

rss · Simon Willison · Nov 11, 15:11

**「Background」** Anthropic&\#x27;s multi-chip effort predates the IPO roadshow: Simon Willison notes that the company&\#x27;s earlier postmortem of three recent issues described bugs affecting only its TPU deployments, an early public hint that some Claude workloads ran on Google TPUs. In the video, co-founder Tom Brown describes the multi-chip bet as unconventional because each chip family needs its own tailored software and inference stack.

<details><summary>References</summary>
<ul>
<li><a href="https://simonwillison.net/2026/Nov/11/anthropic-ipo-roadshow/">Anthropic&#x27;s IPO roadshow video - simonwillison.net</a></li>

</ul>
</details>

**Tags**: `#Anthropic`, `#AI infrastructure`, `#IPO`, `#multi-chip strategy`, `#AI hardware`

---

## Financial News

<a id="item-finance-news-1"></a>
### [CoreWeave shares jump 15% premarket on Q3 revenue beat](https://cointelegraph.com/markets/coreweave-stock-surges-pre-market-q3-revenue?utm_source=rss_feed&amp;utm_medium=rss&amp;utm_campaign=rss_partner_inbound) ⭐️ 7.0/10

CoreWeave shares jumped 15% in premarket trading after the AI infrastructure company reported third-quarter revenue of $3.66 billion, up 168% and 3.4% above analyst estimates. Its revenue backlog reached $132.5 billion.

rss · Cointelegraph · Nov 11, 13:02

**「Background」** CoreWeave is a US cloud-computing company that operates AI-focused data centers built around GPUs, the chips used for parallel computing.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/CoreWeave">CoreWeave - Wikipedia</a></li>

</ul>
</details>

**Tags**: `#CoreWeave`, `#earnings`, `#AI infrastructure`, `#revenue beat`, `#stock move`

---

<a id="item-finance-news-2"></a>
### [Bitmine reports $6.3 billion net loss for fiscal 2026](https://cointelegraph.com/news/bitmine-6b-net-loss-eth-treasury-holdings?utm_source=rss_feed&amp;utm_medium=rss&amp;utm_campaign=rss_partner_inbound) ⭐️ 7.0/10

Bitmine reported a $6.3 billion net loss for fiscal 2026, including $6.2 billion in unrealized losses on digital assets, while holding 6.07 million ETH, or 4.97% of Ether’s supply.

rss · Cointelegraph · Nov 11, 09:58

**「Background」** Bitmine’s fiscal 2026 ended Aug. 31, 2026, and the loss was primarily driven by Ether’s decline; “unrealized” digital-asset losses are paper losses on coins the company still holds rather than losses from selling them.

<details><summary>References</summary>
<ul>
<li><a href="https://www.theblock.co/news/business/2026-11-11-bitmine-6-3-billion-net-loss-437812">Bitmine reports $6.3 billion net loss in latest fiscal year ...</a></li>

</ul>
</details>

**Tags**: `#Bitmine`, `#Ether`, `#crypto treasury`, `#unrealized losses`, `#corporate earnings`

---