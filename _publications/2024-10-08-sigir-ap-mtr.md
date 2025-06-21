---
title: "⭐ [SIGIR-AP 2024] Data-Efficient Massive Tool Retrieval: A Reinforcement Learning Approach for Query-Tool Alignment with Language Models"
collection: publications
category: conferences
permalink: /publication/2024-sigir-ap-mtr
excerpt: 'This paper is about a famous math equation, $$E=mc^2$$'
date: 2024-10-08
venue: 'SIGIR-AP'
paperurl: 'https://dl.acm.org/doi/10.1145/3673791.3698429'
citation: # empyty
---

Recent advancements in large language models (LLMs) integrated with external tools and APIs have successfully addressed complex tasks by using in-context learning or fine-tuning. Despite this progress, the vast scale of tool retrieval remains challenging due to stringent input length constraints. In response, we propose a pre-retrieval strategy from an extensive repository, effectively framing the problem as the massive tool retrieval (MTR) task. We introduce the MTRB (massive tool retrieval benchmark) to evaluate real-world tool-augmented LLM scenarios with a large number of tools. This benchmark is designed for low-resource scenarios and includes a diverse collection of tools with descriptions refined for consistency and clarity. It consists of three subsets, each containing 90 test samples and 10 training samples. To handle the low-resource MTR task, we raise a new query-tool alignment (QTA) framework leverages LLMs to enhance query-tool alignment by rewriting user queries through ranking functions and the direct preference optimization (DPO) method. This approach consistently outperforms existing state-of-the-art models in top-5 and top-10 retrieval tasks across the MTRB benchmark, with improvements up to 93.28% based on the metric Sufficiency@k, which measures the adequacy of tool retrieval within the first k results. Furthermore, ablation studies validate the efficacy of our framework, highlighting its capacity to optimize performance even with limited annotated samples. Specifically, our framework achieves up to 78.53% performance improvement in Sufficiency@k with just a single annotated sample. Additionally, QTA exhibits strong cross-dataset generalizability, emphasizing its potential for real-world applications.

<p align=center>
	<img src="/images/papers/2024-sigir-ap/image.png" width="100%">
</p>


<p align=center>
	<img src="/images/papers/2024-sigir-ap/image2.png" width="80%">
</p>