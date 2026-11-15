---
layout: default
title: "Horizon Summary: 2026-11-15 (EN)"
date: 2026-11-15
lang: en
---

> From 28 items, 4 important content pieces were selected

---

**Technology News**
1. [Lovable apps exposed passport data and 200K messages via RLS gaps](#item-tech-news-1) ⭐️ 8.0/10
2. [Project Zero to cut vulnerability disclosure windows to 90, 60, then 30 days](#item-tech-news-2) ⭐️ 8.0/10
3. [EFF: Tech Companies Are Again Trying to Redefine Privacy](#item-tech-news-3) ⭐️ 7.0/10
4. [tiny-voca: 4.5M-parameter open TTS runs 70x real time on CPU](#item-tech-news-4) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Lovable apps exposed passport data and 200K messages via RLS gaps](https://www.crissyfield.de/research/lovable-en/) ⭐️ 8.0/10

A security report says apps built with Lovable exposed passport details and more than 200,000 private messages because of insufficient Row-Level Security, affecting users of those apps. Lovable&\#x27;s head of security confirmed in the discussion that insufficient RLS was the root cause and said every app is scanned automatically before publish, with a free deeper SAST scan and options to fix findings or enable auto-fix. The report concerns AI-generated apps using Supabase, and the supplied material does not establish how many apps or users were affected beyond those figures.

hackernews · armcat · Nov 14, 17:43 · [Discussion](https://news.ycombinator.com/item?id=50499017)

**「Why RLS matters here」** Lovable-built apps commonly store their data in Supabase, a Postgres-based backend that exposes tables through an auto-generated Data API and is queried directly from the browser. Access control therefore depends on Postgres Row-Level Security policies, and Supabase&\#x27;s own documentation notes that default privileges vary between projects depending on when the project was created and its Data API settings — meaning a table left without RLS enabled is readable by anyone holding the public anon key embedded in the app&\#x27;s frontend.

**「Audit exposed app data」** For teams running Lovable-built apps, the immediate concern is that passport numbers, payment details, and private messages were reachable without logging in, not merely through an application bug. Developers should verify Row-Level Security and public access settings on every Supabase table and API before continuing to collect identity, payment, or message data.

**「Community discussion」** One commenter argued that Supabase&\#x27;s permissive defaults are a major factor and that the October 30 fix was reported not to apply to existing projects, while another said insecure deployments predate AI but AI-generated apps are easier to probe and far more numerous.

<details><summary>References</summary>
<ul>
<li><a href="https://supabase.com/docs/guides/api/securing-your-api">Securing your API | Supabase Docs</a></li>
<li><a href="https://cybernews.com/security/lovable-ai-apps-expose-personal-information/">Lovable AI apps exposed sensitive data in open databases ...</a></li>
<li><a href="https://startupfortune.com/lovable-ai-apps-left-passport-and-payment-data-open-to-anyone/">Lovable AI Apps Left Passport and Payment Data Open to ...</a></li>
<li><a href="https://daily.dev/posts/lovable-apps-expose-passport-details-and-more-than-200k-private-messages-6xovsjn6q">Lovable apps expose passport details and more than 200K...</a></li>

</ul>
</details>

**Tags**: `#security`, `#AI-generated code`, `#Row-Level Security`, `#Supabase`, `#data exposure`

---

<a id="item-tech-news-2"></a>
### [Project Zero to cut vulnerability disclosure windows to 90, 60, then 30 days](https://projectzero.google/2026/11/disclosure-policy.html) ⭐️ 8.0/10

Google&\#x27;s Project Zero announced a staged tightening of its vulnerability-disclosure policy: it is moving to a &quot;Full 90&quot; window, disclosing bugs 90 days after reporting them to vendors, then to 60 days on Feb. 2, 2027, and 30 days on Jan. 3, 2028. The change affects vendors, open-source maintainers, and security teams that receive Project Zero reports and must patch before public disclosure. The 60-day and 30-day windows are scheduled future changes, not current practice.

hackernews · hacb · Nov 14, 11:13 · [Discussion](https://news.ycombinator.com/item?id=50496051)

**「Why deadlines matter」** A vulnerability disclosure deadline is the fixed window a researcher gives a vendor between reporting a bug and publishing technical details, balancing time to ship a patch against pressure to fix it at all. Ninety days has been a common benchmark — the US Department of Health and Human Services, for example, asks reporters to withhold details for 90 calendar days after acknowledging a report — so Project Zero&\#x27;s staged plan moves from that baseline to windows well below prevailing practice.

**「Impact」** Vendors and maintainers will need to triage, fix, and ship patches within 90 days at first, then 60 and 30 days, so projects with long release cycles may need dedicated security-release paths or face public disclosure of unfixed bugs.

**「Community discussion」** Commenters were split on practicality: one argued for immediate disclosure because only public pressure compels fixes, while another said Ubuntu would need &quot;a LOT more time.&quot; A separate commenter warned that disclosure pressure could become leverage to push vendors and open-source projects toward the bug-finding companies&\#x27; AI products.

<details><summary>References</summary>
<ul>
<li><a href="https://www.hhs.gov/vulnerability-disclosure-policy/index.html">Vulnerability Disclosure Policy | HHS.gov</a></li>

</ul>
</details>

**Tags**: `#vulnerability disclosure`, `#Project Zero`, `#software security`, `#open source maintenance`, `#security policy`

---

<a id="item-tech-news-3"></a>
### [EFF: Tech Companies Are Again Trying to Redefine Privacy](https://www.eff.org/deeplinks/2026/11/tech-companies-are-trying-shift-entire-concept-privacy-again) ⭐️ 7.0/10

An EFF article argues that technology companies are making another attempt to shift the meaning of privacy, framing the change as a contest over norms rather than a single product launch or policy announcement. The accompanying Hacker News discussion focuses on AI notetakers in meetings, surveillance becoming a default, and legal privacy protections. No primary article text was supplied, so the piece&\#x27;s specific examples and any company claims cannot be detailed or independently verified here.

hackernews · gslin · Nov 14, 12:45 · [Discussion](https://news.ycombinator.com/item?id=50496602)

**「Background」** EFF&\#x27;s article, by Thorin Klosowski, frames the shift as privacy moving from a personal-choice issue to a bystander problem: people nearby may be captured by someone else&\#x27;s device. It cites Meta and Google smart glasses that can record what the wearer sees and use AI to describe it, Apple&\#x27;s Audio Intelligence turning the Apple Watch into a transcription device, and Amazon&\#x27;s Bee devices that can record and transcribe ambient audio.

**「Impact」** For meeting participants, the concrete concern raised in the thread is that AI notetakers can record and upload conversations by default, including one-to-one manager discussions, and that opting out may be impractical without risking participation.

**「Community Discussion」** Commenters describe AI notetakers as increasingly unavoidable in professional meetings, with one asking whether it is realistic to set a norm that transcription be turned off when it is not needed. Others argue that live transcription can be transformative for deaf and hard-of-hearing users, while cautioning that even a local, non-exporting system is only one configuration change away from retention.

<details><summary>References</summary>
<ul>
<li><a href="https://aiweekly.my/items/46520/tech-companies-are-trying-to-shift-the-concept-of-privacy-again">Tech Companies Are Trying to Shift the Concept of Privacy (Again)</a></li>

</ul>
</details>

**Tags**: `#privacy`, `#AI surveillance`, `#tech policy`, `#EFF`, `#community debate`

---

<a id="item-tech-news-4"></a>
### [tiny-voca: 4.5M-parameter open TTS runs 70x real time on CPU](https://www.reddit.com/r/LocalLLaMA/comments/1xw7zrg/tinyvoca_a_fully_open_45mparameter_tts_code/) ⭐️ 7.0/10

A developer released tiny-voca, an English text-to-speech model with 4,537,291 parameters \(18 MB including the waveform stage\) whose code, weights, training recipe, dataset and custom phonemizer are all published. It offers two 24 kHz voices, one female and one male, and the author reports it runs about 70x faster than real time on four CPU threads, with PyTorch, ONNX and in-browser execution; a browser demo processes audio locally without sending it to a server. The model was trained from scratch in 7.7 hours on a single RTX 4090 and omits a neural vocoder, generating sound with a small source-filter synthesizer instead. The author states the limits directly: English only, no voice cloning, frequent mispronunciation of foreign names and odd spellings, somewhat synthetic timbre, and training audio that was itself generated by Qwen3-TTS, capping the achievable quality.

reddit · r/LocalLLaMA · /u/nato\_nob · Nov 14, 17:26

**「Background」** A source-filter synthesizer generates speech by driving a simple glottal source through a filter that shapes the vocal tract, rather than predicting every waveform sample with a neural network. tiny-voca uses this signal-processing approach in place of a neural vocoder, allowing its 18 MB model package to include waveform generation and still run efficiently on CPU and in the browser.

**「Impact」** Developers who need offline or on-device speech output can test the 18 MB model in a browser or run it through PyTorch or ONNX on CPU-class hardware, without a GPU or a hosted API. Adoption is constrained by the two fixed English voices and the absence of voice cloning, so it does not substitute for multilingual or custom-voice TTS; the author is soliciting mispronounced inputs — numbers, dates, names and long sentences — tagged with the voice used, to improve the phonemizer.

**Tags**: `#text-to-speech`, `#open-source models`, `#on-device AI`, `#efficient inference`, `#tiny models`

---