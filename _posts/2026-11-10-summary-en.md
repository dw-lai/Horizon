---
layout: default
title: "Horizon Summary: 2026-11-10 (EN)"
date: 2026-11-10
lang: en
---

> From 49 items, 4 important content pieces were selected

---

**Technology News**
1. [watched.earth finds satellite passes and shows available imagery](#item-tech-news-1) ⭐️ 8.0/10
2. [Google Announces TPU 8tx and 8i Max for Agentic AI](#item-tech-news-2) ⭐️ 8.0/10
3. [E-means claims k-means-quality clustering in one-tenth the epochs](#item-tech-news-3) ⭐️ 7.0/10
4. [Claim: Consumer Gemini Connected Apps Expose Drive, Gmail to Human Review](#item-tech-news-4) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [watched.earth finds satellite passes and shows available imagery](https://www.watched.earth/) ⭐️ 8.0/10

watched.earth, launched as a Show HN project, lets anyone enter a place and see every satellite pass over it in the past seven days, then view Sentinel-2, Landsat, or NASA imagery from those passes when a real image exists. The open-source browser tool runs SGP4 against the CelesTrak catalog in roughly half a second, renders about 17,000 objects on the GPU while solving Kepler&\#x27;s equation each frame, and does not store the user&\#x27;s location. Its author reports zero missed passes in brute-force checks at the poles, the antimeridian, and tiny swaths, and says the tool corrects Sentinel-2 timestamps that are often 5–10 minutes off the actual overpass.

hackernews · a585gupt · Nov 9, 17:51 · [Discussion](https://news.ycombinator.com/item?id=50428907)

**「Background」** Pass prediction relies on SGP4, a standard orbital propagator that converts a cataloged element set into a satellite position at a given time. CelesTrak publishes the satellite catalog and SGP4 implementation guidance used to perform that calculation locally rather than on a server.

**「Impact」** Users can search a location&\#x27;s seven-day overpass history and retrieve matching Sentinel-2, Landsat, or NASA imagery in the same browser session; because the tool labels a place “watched” only when a real image exists, missing labels should be read as absent coverage in those sources rather than as proof that no satellite passed overhead.

**「Community discussion」** A geospatial professional called it a strong satellite-overview site specifically because it shows the exact image a satellite took, while another commenter reported that it offered more data and easier access than Copernicus for planning backpacking trips. Other commenters praised the execution and the combined orbit, ground-track, and time-series views.

<details><summary>References</summary>
<ul>
<li><a href="https://celestrak.org/satcat/">CelesTrak: Satellite Catalog (SATCAT)</a></li>
<li><a href="https://celestrak.org/software/tutorials/sgp4.php">CelesTrak: SGP4 Software Tutorial</a></li>

</ul>
</details>

**Tags**: `#satellite-tracking`, `#geospatial`, `#remote-sensing`, `#SGP4`, `#GPU-rendering`

---

<a id="item-tech-news-2"></a>
### [Google Announces TPU 8tx and 8i Max for Agentic AI](https://blog.google/innovation-and-ai/infrastructure-and-cloud/global-network/tpu-8i-max-and-8tx/) ⭐️ 8.0/10

Google announced two new TPUs, 8tx and 8i Max, positioned for agentic AI workloads. The supplied item does not include technical specifications, performance figures, pricing, availability, or compatibility details, so the chips&\#x27; practical capabilities and comparisons with prior TPUs or Nvidia hardware cannot be verified. The available material also does not establish whether the chips are shipping or only announced.

hackernews · \_benx\_ · Nov 9, 21:56 · [Discussion](https://news.ycombinator.com/item?id=50432831)

**「Background」** Google&\#x27;s TPU lineup is organized by workload: TPU 8t is intended for scale-up training and TPU 8i for low-latency reasoning \(tool-1-1\). Google says the 8i pairs 288 GB of high-bandwidth memory with 384 MB of on-chip SRAM and delivers nearly three times the compute per pod of its previous generation \(tool-1-2\). The newly announced 8tx variant adds confidential computing and fifth-generation AMD EPYC processors for security-sensitive customers, while the 8i Max is positioned for very large context windows and the highest compute density per rack \(tool-1-3, tool-1-1\).

**「Deployment implications」** Teams choosing TPU infrastructure now face a workload split: confidential-inference workloads should target TPU 8tx, which pairs TPU 8t with fifth-generation AMD EPYC processors and hardware protection for data and model weights even during processing, while long-context workloads should target TPU 8i Max, which combines two TPU chips in one package for more compute and memory. The supplied material does not include pricing, watt/token, or dollar/token figures, so cost comparisons with equivalent Nvidia offerings cannot yet be made.

**「Community Discussion」** Commenters pressed on commercial access and cost: one asked why Google does not sell these TPUs, and another requested watt/token and dollar/token figures plus comparisons with Nvidia&\#x27;s price-equivalent parts. A separate commenter said Google Colab&\#x27;s most powerful available TPU remains v6e-1, which they consider too small for serious work; these are user opinions and requests, not verified product details.

<details><summary>References</summary>
<ul>
<li><a href="https://blog.google/innovation-and-ai/infrastructure-and-cloud/global-network/tpu-8i-max-and-8tx/">Introducing TPU 8 tx and TPU 8 i Max</a></li>
<li><a href="https://mindmodemedia.com/googles-tpu-8t-and-tpu-8i-address-agentic-ai/">Google &#x27;s TPU 8 t and TPU 8 i address agentic AI - mindmodemedia.com</a></li>
<li><a href="https://dzen.ru/a/avHlCl56vGiwEiaH">Google расширила линейку тензорных процессоров ( TPU )... | Дзен</a></li>
<li><a href="https://habr.com/ru/companies/bothub/articles/1105552/">Google представила TPU 8 i Max и 8 tx — системы для... / Хабр</a></li>
<li><a href="https://trashexpert.ru/news/hardware-news/google-tpu-8tx-max">Google представит TPU 8 tx и 8 i Max для разных задач ИИ</a></li>

</ul>
</details>

**Tags**: `#TPU`, `#AI hardware`, `#Google Cloud`, `#machine learning infrastructure`, `#agentic AI`

---

<a id="item-tech-news-3"></a>
### [E-means claims k-means-quality clustering in one-tenth the epochs](https://e-means.github.io/) ⭐️ 7.0/10

E-means, a proposed alternative to k-means for clustering, claims comparable or better results in roughly one-tenth the epochs, according to its project site. Early practitioner reports are mixed but concrete: a 146× GPU speedup after adapting it to an IVF index and 2.5× faster bulk reindexing, versus no improvement in a spherical-mesh relaxation test and little end-to-end change for incremental insertion.

hackernews · porridgeraisin · Nov 9, 18:45 · [Discussion](https://news.ycombinator.com/item?id=50429734)

**「Background」** K-means groups data by repeatedly assigning points to the nearest centroid and recalculating the centroids, an approach suited to compact, spherical clusters. Distance calculations dominate its runtime, and on very large datasets the repeated passes can overload a system, which is the cost baseline e-means claims to improve by needing fewer epochs.

**「Impact」** The reported gains are concentrated in workloads that repeatedly scan a large dataset, such as rebuilding a vector index in bulk; teams with those workloads have a concrete reason to benchmark e-means against Lloyd&\#x27;s algorithm. The reports do not support treating it as a universal replacement: incremental indexing and the spherical-mesh test saw little or no benefit.

**「Community discussion」** Commenters contributed mixed practitioner results—146× GPU speedup for an IVF index and 2.5× faster bulk reindexing, while jlhawn reported it was “definitely not better” for spherical-mesh relaxation—and one noted that incremental insertion barely changed overall. shiandow argued the method may be interpretable as expectation maximization with a friction term, emphasizing that its update keeps centroids within the convex hull.

<details><summary>References</summary>
<ul>
<li><a href="https://www.geeksforgeeks.org/machine-learning/dbscan-clustering-in-ml-density-based-clustering/">DBSCAN Clustering in ML - Density based clustering - GeeksforGeeks</a></li>
<li><a href="https://www.academia.edu/112847973/Using_bagging_and_mapreduce_in_k_means_clustering_for_detection_of_cancer">(PDF) Using bagging and mapreduce in k - means clustering for...</a></li>

</ul>
</details>

**Tags**: `#clustering`, `#k-means`, `#machine-learning-algorithms`, `#performance-optimization`, `#GPU-acceleration`

---

<a id="item-tech-news-4"></a>
### [Claim: Consumer Gemini Connected Apps Expose Drive, Gmail to Human Review](https://github.com/thisisme6598/gemini_files/) ⭐️ 7.0/10

A GitHub repository discussed on Hacker News claims that consumer Google Gemini with Connected Apps can route personal Drive files and Gmail data to human annotators. The item provides no source content and is not established reporting, so the claim remains unverified. Commenters distinguish this from Workspace Gemini, which they say still claims not to be subject to human review.

hackernews · gf74918 · Nov 9, 18:24 · [Discussion](https://news.ycombinator.com/item?id=50429426)

**「Background」** Google&\#x27;s 2023 launch language for Gemini Workspace extensions promised that personal content from Gmail, Docs and Drive was not seen by human reviewers, according to search results, which say Google later changed that commitment in an October 16, 2026 Help policy edit that allowed connected Drive and Gmail data into human-review pipelines. Consumer Gemini with Connected Apps and Gemini for Google Workspace are governed differently, and reviewers reportedly receive summaries, excerpts, generated media and inferences rather than raw documents.

**「Impact」** Consumers who connect personal Gmail or Drive to Gemini may want to review connected-app permissions or disconnect them if they do not want that content exposed to potential human review; organizations using Workspace have a different stated policy, according to the discussion.

**「Community Discussion」** Commenters focused on scope, with one arguing the issue is specifically consumer Gemini with Connected Apps while Workspace Gemini still claims no human review. Others described suspected cases where Gemini responses seemed tuned to their email content, though these are anecdotes rather than confirmation.

<details><summary>References</summary>
<ul>
<li><a href="https://aiweekly.co/alerts/google-gemini-routes-personal-drive-gmail-to-human-reviewers">Google Gemini Routes Personal Drive, Gmail to Human Reviewers</a></li>
<li><a href="https://www.strac.io/blog/gemini-data-privacy">Gemini Data Privacy: What Google Collects &amp; Reviews (2026)</a></li>
<li><a href="https://www.aib.vote/en/news/gemini-connected-drive-email-human-review">Repository Reports Gemini File Exposure | AIB</a></li>

</ul>
</details>

**Tags**: `#AI privacy`, `#Google Gemini`, `#data governance`, `#human review`, `#enterprise AI`

---