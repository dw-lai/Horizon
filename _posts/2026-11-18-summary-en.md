---
layout: default
title: "Horizon Summary: 2026-11-18 (EN)"
date: 2026-11-18
lang: en
---

> From 40 items, 9 important content pieces were selected

---

**Technology News**
1. [OpenAI releases GPT-6.2 Astra and Sol with lower API prices](#item-tech-news-1) ⭐️ 9.0/10
2. [Write-up reports narrow Java4Shell RCE in OpenJDK Base64 handling](#item-tech-news-2) ⭐️ 8.0/10
3. [Solid 2.0 release adds server RPC, live/broadcast, diagnostics](#item-tech-news-3) ⭐️ 8.0/10
4. [Datasette Lite rewrite runs full Datasette app in browser via service workers](#item-tech-news-4) ⭐️ 8.0/10
5. [Nvidia stops disclosing Singapore sales as subsidiary revenue hits $104B](#item-tech-news-5) ⭐️ 7.0/10
6. [Microsoft&\#x27;s ONNX Runtime GitHub repository reported unavailable](#item-tech-news-6) ⭐️ 7.0/10
7. [Microsoft Introduces MAI Code 2 and MAI Code 2 Flash](#item-tech-news-7) ⭐️ 7.0/10
8. [Cloudflare calls Quad9&\#x27;s France exit a DNS warning](#item-tech-news-8) ⭐️ 7.0/10
9. [Prime Radiant releases external sandbox servers for coding agents](#item-tech-news-9) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [OpenAI releases GPT-6.2 Astra and Sol with lower API prices](https://openai.com/index/introducing-gpt-6-2-astra-sol/) ⭐️ 9.0/10

OpenAI introduced GPT-6.2 Astra, positioned for demanding projects, and GPT-6.2 Sol, positioned for everyday work, making both available in the API as \`gpt-6.2-astra\` and \`gpt-6.2-sol\`; Simon Willison&\#x27;s LLM 0.38 adds support. Astra costs $8 per million input tokens and $40 per million output tokens, 80% of GPT-6 Astra&\#x27;s $10/$50, with cached input at $0.40 versus $1 per million; Sol is $2/$10, matching GPT-6.1 Sol and half the price of GPT-5.6 Sol. Reception is mixed: Willison reports that Astra trails Claude Fable 5.2 on several benchmarks and has drawn complaints about a confusing communication style.

hackernews · jasondavies · Nov 17, 17:46 · [Discussion](https://news.ycombinator.com/item?id=50535230)

**「Background」** GPT-6.2 Astra and GPT-6.2 Sol extend OpenAI’s GPT-6 model line, with Astra positioned as the frontier tier and Sol as the efficient everyday tier. The release compares Astra with GPT-6 Astra, which cost $10 per million input tokens and $50 per million output tokens, and Sol with GPT-6.1 Sol and GPT-6 Sol, both priced at $2/$10. Those earlier prices are the baseline for the new models’ stated 80% Astra reduction and unchanged Sol pricing.

**「Impact」** Developers should re-test long-running agent workflows before switching: commenters report lower costs and faster responses, but also cases where the models stopped early without the requested answer. Using the new models requires the \`gpt-6.2-astra\` or \`gpt-6.2-sol\` identifiers, or LLM 0.38 for that client.

**「Community discussion」** Several commenters reported lower costs and faster runs—one said Astra&\#x27;s analytics-exam cost fell from about $20 to $4 with similar accuracy, though it sometimes finished early—while others questioned quality: OpenAI&\#x27;s office-work examples were called poor, and PacBench placed Astra just below Kimi K3.1 Pro despite costing about three times as much in that run. A commenter citing the system card also highlighted more evaluation-awareness signs and a greater ability to evade chain-of-thought monitoring in some GPT-6.2 Astra tests.

**Tags**: `#OpenAI`, `#AI models`, `#LLM release`, `#benchmarks`, `#cost efficiency`

---

<a id="item-tech-news-2"></a>
### [Write-up reports narrow Java4Shell RCE in OpenJDK Base64 handling](https://calif.io/java4shell/) ⭐️ 8.0/10

A detailed exploit write-up reports remote code execution in OpenJDK/HotSpot when processing Base64, with exploitation dependent on specific VM, configuration, and network conditions. The described attack performs heap grooming over the network and is sensitive to round-trip time and jitter; the researchers say they tested it over public internet addresses rather than assuming laboratory conditions. The supplied material does not identify a CVE, affected versions, a patch, or a vendor response, so practical exposure remains unclear.

hackernews · werrett · Nov 17, 21:11 · [Discussion](https://news.ycombinator.com/item?id=50538240)

**「Background」** The bug is tracked as CVE-2026-114938. Reporting says Oracle and the OpenJDK project have patched the flaw, which Calif used to take over Jira, Confluence, Jenkins and Keycloak without authentication.

**「Remediation scope」** Operators running HotSpot-based Java runtimes — OpenJDK, Oracle JDK, or GraalVM JDK — need to inventory and patch hosts and containers, while OpenJ9 and GCJ builds are reported by Semgrep&\#x27;s detection notes to be unaffected because only HotSpot emits the exploited stub \(Azul Prime/Zing replaces the relevant C2 component\). Semgrep published free detection scripts that check five exposure conditions, and a community-suggested workaround, running with \`-XX:UseAVX=2\`, remains unconfirmed. The flaw is tracked as CVE-2026-114938 and reported to affect OpenJDK 17.0.6 and later, with Oracle&\#x27;s November builds cited as the patch target.

**「Community discussion」** Commenters described the exploit conditions as highly specific but expected many hosts could still be affected; a Semgrep contributor linked detection scripts that check five conditions, including whether the JVM is HotSpot-based. Another commenter relayed an unconfirmed claim that the flaw involves the AVX-512 Base64 decoder and could be avoided with the -XX:UseAVX=2 flag, which the supplied material does not establish.

<details><summary>References</summary>
<ul>
<li><a href="https://www.cyberkendra.com/2026/11/cve-2026-114938-pre-auth-rce-flaw-in-java-17-puts-servers-at-risk.html">Java 4 Shell ( CVE -2026-114938): Java Base 64 Flaw... - Cyber Kendra</a></li>
<li><a href="https://www.bleepingcomputer.com/news/security/critical-java4shell-flaw-allows-rce-attacks-on-major-java-applications/">Critical Java 4 Shell flaw allows RCE attacks on major Java applications</a></li>
<li><a href="https://www.sonatype.com/blog/critical-openjdk-rce-cve-2026-114938-what-to-know">Critical OpenJDK RCE CVE-2026-114938: What to Know</a></li>
<li><a href="https://threatdefence.com/article/java4shell-cve-2026-114938-openjdk-rce-patching-hunting">Java4Shell CVE-2026-114938: Java 17 RCE Checks and Hunting</a></li>
<li><a href="https://securityonline.info/java4shell-cve-2026-114938/">Java4Shell (CVE-2026-114938): Java SE RCE Explained</a></li>

</ul>
</details>

**Tags**: `#security`, `#OpenJDK`, `#RCE`, `#Base64`, `#exploit research`

---

<a id="item-tech-news-3"></a>
### [Solid 2.0 release adds server RPC, live/broadcast, diagnostics](https://www.solidjs.com/blog/solid-2-0-the-long-hold/) ⭐️ 8.0/10

Solid 2.0 has been released, bringing the JavaScript UI framework&\#x27;s server-client integration and debugging diagnostics into a major-version update for developers building full-stack apps with Solid. The announcement presents server RPC plus &quot;live&quot; and &quot;broadcast&quot; capabilities as a seamless way to connect client and server, and frames the improved diagnostics as useful for both human- and agent-written code. The material available here does not detail migration requirements or package versions.

hackernews · pier25 · Nov 17, 18:56 · [Discussion](https://news.ycombinator.com/item?id=50536387)

**「Background」** Solid 2.0 follows the project&\#x27;s August 2026 release candidate, which said ecosystem libraries including Solid Primitives, Kobalte, Solid Testing Library, Storybook, and AG Grid had supported 2.0 through the betas and were ready for the RC.

**「Impact」** For teams weighing Solid for full-stack work, the first-party server RPC and live/broadcast features offer an alternative to stitching together a separate frontend-backend layer or using LiveView- or htmx-style tools. The available material does not establish migration cost or compatibility with existing Solid apps.

**「Community discussion」** Commenters were largely positive: one argued that Solid&\#x27;s server RPC, &quot;live,&quot; and &quot;broadcast&quot; design feels more natural than LiveView or htmx/Datastar and said Remix never closed the frontend-backend gap. Another described the &quot;Built to Be Written by Agents&quot; features as essentially better debugging diagnostics that also help human developers, questioning the agent-specific marketing.

<details><summary>References</summary>
<ul>
<li><a href="https://www.solidjs.com/blog/solid-2-0-rc-the-big-reveal">Solid 2.0 RC: The Big | SolidJS</a></li>

</ul>
</details>

**Tags**: `#SolidJS`, `#JavaScript frameworks`, `#frontend development`, `#server RPC`, `#developer tools`

---

<a id="item-tech-news-4"></a>
### [Datasette Lite rewrite runs full Datasette app in browser via service workers](https://simonwillison.net/2026/Nov/17/datasette-lite/) ⭐️ 8.0/10

Datasette Lite has been completely rewritten to run the full Datasette Python application in the browser using service workers and Pyodide, replacing the earlier Pyodide-worker and innerHTML approach that could not execute JavaScript-dependent features. Its lite.datasette.io URLs can load SQLite databases, JSON, CSV or SQL files; select a released Datasette version from PyPI or a GitHub commit, tag or branch; choose from more than 100 SQLite versions; and install plugins from PyPI or wheel URLs, including JavaScript visualization plugins. Willison says the result is now almost indistinguishable from server-side Datasette.

rss · Simon Willison · Nov 17, 16:48

**「Background」** Datasette Lite debuted in 2022 as a way to run the Datasette Python application in a browser via WebAssembly and Pyodide. Its original architecture ran Datasette inside a Pyodide web worker, simulated requests, and inserted the returned HTML into the page with innerHTML; that approach broke JavaScript-dependent features because script tags inserted through innerHTML do not execute. The new service-worker architecture replaces that workaround and is what allows the browser version to behave like the server-side app.

**「Impact」** Developers can share URL-addressable demos and bug reproductions pinned to a Datasette ref and SQLite version, as Willison does with a pagination bug under 1.0a42 and its fix under 1.0a43, without running a server. Remote database and metadata URLs must provide open CORS headers, so files hosted on Gists or similar CORS-enabled services are the practical route.

**Tags**: `#Datasette`, `#Pyodide`, `#WebAssembly`, `#Service Workers`, `#Browser-based Python`

---

<a id="item-tech-news-5"></a>
### [Nvidia stops disclosing Singapore sales as subsidiary revenue hits $104B](https://www.ft.com/content/dbde7a30-548c-4f9d-a4be-7898a0c24dcf) ⭐️ 7.0/10

Nvidia has stopped disclosing Singapore sales, the Financial Times reported, while revenue tied to its Singapore subsidiary reached $104 billion. The figure is subsidiary revenue, not a direct measure of GPUs consumed in Singapore, so it does not by itself show where the chips were ultimately used. The change removes a country-level data point for investors and export-control watchers tracking AI-chip flows.

hackernews · louiereederson · Nov 17, 17:12 · [Discussion](https://news.ycombinator.com/item?id=50534631)

**「Background」** Nvidia had been reporting revenue from its Singapore business in its financial disclosures. The Wall Street Journal reported that Nvidia stopped doing so just as scrutiny of Megaspeed was rising, while Fortune reported the change came shortly after a probe into Megaspeed, a Singapore-based company that had become one of Nvidia&\#x27;s largest buyers in Asia.

**「Disclosure gap」** Investors and export-control reviewers lose a country-level revenue signal: Nvidia&\#x27;s $104B Singapore-attributed figure reflects sales booked through its local subsidiary, while Singapore&\#x27;s trade minister has said physical deliveries to the country were less than 1% of revenue. They should treat the figure as an accounting measure rather than a proxy for local chip demand or end destination.

**「Community discussion」** Commenters disputed the implication that the $104 billion figure shows chips were consumed in or routed through Singapore. One argued the number is external revenue of Nvidia&\#x27;s Singapore subsidiary, including orders placed through OEMs, ODMs, and resellers, while another described it as an accounting-attribution question that does not reveal where revenue is generated or where the chips end up.

<details><summary>References</summary>
<ul>
<li><a href="https://www.wsj.com/business/earnings/nvidias-disappearing-singapore-sales-deepen-mystery-around-megaspeed-7d483180">Nvidia’s Disappearing Singapore Sales Deepen Mystery Around ...</a></li>
<li><a href="https://fortune.com/2026/11/12/nvidia-changed-earnings-report-format-singapore-revenue-megaspeed-probe-colette-kress/">Nvidia suddenly changed how it reported revenue in Singapore ...</a></li>
<li><a href="https://www.channelnewsasia.com/singapore/nvidia-ai-chips-us-export-controls-singapore-deepseek-china-4944231">Singapore does not condone businesses who use local ties to bypass...</a></li>

</ul>
</details>

**Tags**: `#Nvidia`, `#AI hardware`, `#export controls`, `#Singapore`, `#corporate disclosure`

---

<a id="item-tech-news-6"></a>
### [Microsoft&\#x27;s ONNX Runtime GitHub repository reported unavailable](https://github.com/microsoft/onnxruntime) ⭐️ 7.0/10

The microsoft/onnxruntime GitHub repository was reported unavailable, with no official explanation or confirmation included in the item. The submitter said the disappearance was discovered that morning when evaluations began failing in their pipelines and that there had been no advance warning.

hackernews · nvader · Nov 17, 23:18 · [Discussion](https://news.ycombinator.com/item?id=50539610)

**「Background」** ONNX Runtime is Microsoft&\#x27;s cross-platform inference and training accelerator for models in the Open Neural Network Exchange \(ONNX\) format. ONNX provides a shared model representation intended to let the same model run across different runtime systems and hardware, including GPUs and specialized AI accelerators.

**「Impact」** Teams whose builds or evaluation jobs fetch ONNX Runtime directly from GitHub may see failures until the repository returns or they switch to a cache, package mirror, or alternate source. The Intel fork cited in comments includes OpenVINO modifications, so it is not a verified drop-in replacement for Microsoft&\#x27;s repository.

**「Community Discussion」** Commenters speculated about a possible package compromise, ONNX telemetry, and backdoored-model attack vectors, but none established the cause of the repository&\#x27;s disappearance. Another commenter pointed to Intel&\#x27;s OpenVINO-modified ONNX Runtime fork as the nearest available alternative.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Open_Neural_Network_Exchange">Open Neural Network Exchange - Wikipedia</a></li>
<li><a href="https://github.com/microsoft/onnxruntime">GitHub - microsoft/onnxruntime: ONNX Runtime: cross-platform ...</a></li>

</ul>
</details>

**Tags**: `#ONNX Runtime`, `#open-source infrastructure`, `#supply chain security`, `#GitHub`, `#Microsoft`

---

<a id="item-tech-news-7"></a>
### [Microsoft Introduces MAI Code 2 and MAI Code 2 Flash](https://microsoft.ai/news/introducing-mai-code-2-and-mai-code-2-flash/) ⭐️ 7.0/10

Microsoft announced two new coding models, MAI Code 2 and a lighter MAI Code 2 Flash, aimed at developer coding-assistant workloads. The announcement page itself supplied no technical details in this feed, so benchmark scores, context limits, pricing, and the exact availability or licensing of the two models remain unverified here. One commenter reported that GitHub Copilot offered MAI Code 2 at a 50% discount and that, after switching to it, the model resolved Python build problems under WSL/Ubuntu, generated passing test cases, and fixed Azure Bicep deployment issues. Treat the model&\#x27;s performance claims as vendor announcements pending independent measurement, and the Copilot discount as a single user&\#x27;s anecdotal report.

hackernews · lemonish97 · Nov 17, 18:25 · [Discussion](https://news.ycombinator.com/item?id=50535885)

**「Background」** MAI Code 2 and Code 2 Flash are the next generation of Microsoft&\#x27;s MAI-Code family; GitHub&\#x27;s changelog describes the earlier generation as focused on lightweight coding assistance. The new pair is positioned for more complex, agentic software engineering and is available through GitHub Copilot.

**「Copilot model choice and cost」** Developers using GitHub Copilot can now switch to MAI Code 2 or MAI Code 2 Flash, with Microsoft positioning Code 2 as near-frontier coding quality at a fraction of rivals&\#x27; cost—claiming 98% of GPT-6.1 Sol&\#x27;s performance at 40% of the cost and 96% of Claude Opus 5.5&\#x27;s at 5% of the cost—while Flash targets quick edits and routine fixes. Because those ratios are vendor claims and carry caveats, teams should validate them on their own workloads and review Copilot&\#x27;s plan and pricing terms before treating the switch as a cost saving.

**「Community Discussion」** Commenters debated how durable the leads of incumbent model providers really are, with one arguing that OpenAI and Anthropic stay ahead only by a few months at a time, and another asking how Microsoft closed the gap so quickly and speculating — without evidence — about distillation from OpenAI models. A separate thread criticized GitHub Copilot&\#x27;s value for the money, with one team saying it cancelled its subscription, while another user&\#x27;s hands-on report placed MAI Code 2 roughly on par with Claude Opus for their debugging and deployment tasks.

<details><summary>References</summary>
<ul>
<li><a href="https://microsoft.ai/news/introducing-mai-code-2-and-mai-code-2-flash/">MAI Code 2 and Code 2 Flash: Everyday coding at scalable ...</a></li>
<li><a href="https://github.blog/changelog/2026-11-17-mai-code-2-and-mai-code-2-flash-in-github-copilot/">MAI Code 2 and MAI Code 2 Flash in GitHub Copilot</a></li>
<li><a href="https://alphasignal.ai/news/microsoft-brings-mai-code-2-to-github-copilot-at-5-of-claude-s-cost">Microsoft Brings MAI Code 2 to GitHub Copilot at 5% of Claude ...</a></li>
<li><a href="https://felloai.com/mai-code-2/">MAI Code 2: Price, Benchmarks and Copilot Plans - felloai.com</a></li>

</ul>
</details>

**Tags**: `#AI coding assistants`, `#Microsoft AI`, `#LLM releases`, `#model evaluation`, `#GitHub Copilot`

---

<a id="item-tech-news-8"></a>
### [Cloudflare calls Quad9&\#x27;s France exit a DNS warning](https://blog.cloudflare.com/quad9-withdrawal-from-france/) ⭐️ 7.0/10

Quad9 has withdrawn from France, and Cloudflare is arguing that the exit is an early warning about legal pressure on public DNS resolvers. Cloudflare frames the withdrawal as a precedent that could affect other resolver operators rather than as a new service change of its own. The post is vendor-framed, and the item analysis says Cloudflare avoids concrete commitments on the issue.

hackernews · subset · Nov 17, 22:13 · [Discussion](https://news.ycombinator.com/item?id=50538994)

**「Background」** Quad9, a Swiss nonprofit that runs a free public DNS resolver, said in October 2026 that it would stop serving users in France on November 24 after a Paris court ordered it to block sites accused of copyright infringement; it was reported as the second DNS resolver to leave the country. Cloudflare&\#x27;s post places that withdrawal in a wider legal context, pointing to a Belgian court order that would impose penalties on Cloudflare, Google, and Cisco if they do not block websites through their public resolvers by early January 2027.

**「Impact」** For users in France, Quad9&\#x27;s withdrawal removes one public DNS resolver from the options available. Cloudflare argues the precedent could push other resolver operators to exit rather than accept blocking obligations.

**「Community discussion」** Quad9&\#x27;s CTO said at IETF 127 that he had encountered 100% support so far for Quad9&\#x27;s position and &quot;general dread&quot; about the DNS legal pressure. Several commenters condemned European internet overregulation, and one asked Cloudflare to commit to withdrawing from affected countries if its appeal fails.

<details><summary>References</summary>
<ul>
<li><a href="https://blog.cloudflare.com/quad9-withdrawal-from-france/">Quad9’s withdrawal from France: A canary in the coal mine</a></li>
<li><a href="https://torrentfreak.com/dns-resolver-quad9-will-leave-france-after-court-orders-piracy-blocking-penalty/">DNS Resolver Quad9 Will Leave France After Court Orders ...</a></li>
<li><a href="https://www.eff.org/deeplinks/2026/10/french-courts-site-blocking-orders-drive-quad9-out-france">French Court’s Site-Blocking Orders Drive Quad9 Out Of France</a></li>

</ul>
</details>

**Tags**: `#DNS`, `#Internet governance`, `#privacy`, `#content blocking`, `#France`

---

<a id="item-tech-news-9"></a>
### [Prime Radiant releases external sandbox servers for coding agents](https://simonwillison.net/2026/Nov/17/external-sandboxes-for-coding-agents/) ⭐️ 7.0/10

Simon Willison and Prime Radiant introduced an “external sandbox” pattern for coding agents, where the agent runs outside a dedicated sandbox and sends code there for execution. They released three implementations with the same localhost API: external-sandbox-v86, a Node.js server using v86 to run Alpine Linux in WebAssembly; external-sandbox-container, a Python server running Alpine Linux in an Apple Containers instance; and external-sandbox-quicksand, a Python server using Microsoft’s Quicksand library, which bundles QEMU and Alpine Linux. Pi, Claude Code, and Codex can be configured to send code-execution calls to that API, and the sandboxes include an optional HTTP/HTTPS allow-list proxy plus credential replacement so agent code can make authenticated calls without being given the secret. Willison frames this as a way to experiment with safer execution of agent-generated code, including local models, but the post reports no independent security evaluation or adoption results.

rss · Simon Willison · Nov 17, 22:52

**「Background」** Coding agents such as Claude Code, Codex, and Pi can execute code and shell commands, so a mistake or prompt-injection attack can otherwise expose the machine they run on. The external-sandbox approach separates the agent process from the execution environment, routing those commands into an isolated VM or container while preserving a localhost API for the agent to call.

**「Impact」** With the shared localhost API, teams can keep an agent outside the execution environment while confining generated code to the v86 WebAssembly emulator, an Apple Containers instance, or a QEMU-backed Quicksand sandbox, and can restrict outbound hosts and substitute credentials at the proxy boundary. Because the post provides no security audit, benchmark, or comparison of the three backends, teams must still evaluate which isolation option fits their threat model.

**Tags**: `#AI agents`, `#sandboxing`, `#security`, `#coding agents`, `#developer tools`

---