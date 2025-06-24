---
title: "[EMNLP 2024] HoLLMwood: Unleashing the Creativity of Large Language Models in Screenwriting via Role Playing"
collection: publications
category: conferences
permalink: /publication/2024-11-12-hollmwood
excerpt: 'Screenwriting, Large Language Models (LLMs), Role Playing, Creative Generation, Multi-Agent Collaboration'
date: 2024-11-12
venue: 'EMNLP'
paperurl: 'https://aclanthology.org/2024.findings-emnlp.474/'
bibtexurl: # empty
citation: # empyty
slidesurl: # empyty
---

**关键词**
- 剧本写作 / Screenwriting  
- 大语言模型 / Large Language Models (LLMs)  
- 角色扮演 / Role Playing  
- 创意生成 / Creative Generation  
- 多智能体协作 / Multi-Agent Collaboration  
- 自动化写作 / Automated Writing

Arxiv地址：[https://arxiv.org/abs/2406.11683](https://arxiv.org/abs/2406.11683)

EMNLP 2024: [https://aclanthology.org/2024.findings-emnlp.474/](https://aclanthology.org/2024.findings-emnlp.474/)

## 背景

近年来，生成式人工智能（Generative AI）在艺术创作，尤其是计算机视觉领域取得了突破性进展。但在自然语言处理领域，尤其是文学创作任务（如剧本写作），大语言模型（LLMs）尚未展现出与人类专家同等水平的创造力和复杂性。  
剧本写作不仅要求精密的情节设计、深刻的人物塑造，还需要理解人类情感和动机。尽管已有研究尝试用LLM进行故事生成或人机共写，但现有方法在对话自然度、人物交互以及整体剧本质量上仍有不足，且大多需要人工干预，自动化程度有限。

<p align=center>
	<img src="/images/papers/2024-hollmwood/hollmwood-1.png" width="80%">
</p>

## 方法

本论文提出了一种全自动化的剧本写作框架——**HOLLMWOOD**，旨在模拟好莱坞专业编剧的创作过程，最大化挖掘LLMs在剧本创作中的潜能。核心创新包括：

1. **多角色分工机制**  
   - **Writer（编剧）**：设计角色并基于初步故事线规划情节大纲。  
   - **Editor（编辑）**：针对角色和情节大纲提供结构化反馈，进行多轮润色与修订。  
   - **Actors（演员）**：通过角色扮演机制，让LLM以第一人称视角代入具体角色，推动对话和故事发展，增强人物互动和情节丰富度。

2. **剧本生成流程分阶段执行**  
   - **情节规划（Plot Planning）**：围绕初步故事线设计主要角色与两层级的情节大纲。  
   - **反馈/修订机制（Feedback/Revision）**：模拟真实写作中编辑和作者间的互动，迭代提升角色和情节合理性。  
   - **故事扩展（Story Expansion）**：细化每个子情节，生成具体章节，保证故事连贯性。  
   - **剧本脚本生成（Screenplay Generation）**：将扩展后的章节转换为剧本格式，包含场景、动作、台词等。  
   - **角色扮演机制（Role-Playing）**：赋予LLM真实“演员”身份，根据角色设定和故事背景，自然生成个性化台词和互动。

3. **流程模块解耦**  
   - 支持每一环节引入人工干预或调整，具备高度灵活性和可扩展性。

<p align=center>
	<img src="/images/papers/2024-hollmwood/hollmwood-2.png" width="100%">
</p>

## 实验

1. **数据集**  
   - 采用LLM自动生成六大主流影视题材（爱情、科幻、恐怖、剧情、犯罪、喜剧）的初步故事线，共60个样本。

2. **对比基线方法**  
   - **Plan-then-Write**：常规的角色设计+情节大纲+分步剧本生成流程。  
   - **DOC-screen**：借用细致大纲控制的长文本生成方法，并基于每章转写为剧本。

3. **评价方法**  
   - **自动化评测**：通过GPT-4进行成对脚本主观评价（连贯性、相关性、趣味性、整体质量）；还包括n-gram重复率、Distinct、Entropy、Self-BLEU等指标。  
   - **人工评测**：三位有经验的人工标注者进行小规模对比分析。  
   - **消融实验**：分别去除反馈/修订与角色扮演模块，评估各部分的作用和贡献。

## 结果

1. **主观评测**  
   - 无论使用GPT-3.5还是GPT-4，HOLLMWOOD在连贯性、相关性、趣味性和整体质量四个维度都大幅优于基线方法，尤其在趣味性和整体质量上提升明显。
   - 人工评测结果与自动化评测一致，显示出方法的普适性和稳健性。

2. **自动化指标**  
   - 在Distinct、Entropy等多样性和创新性指标上，HOLLMWOOD同样表现更优，重复率低、文本丰富。

3. **消融实验发现**  
   - **反馈/修订机制**能显著提升角色和情节大纲的合理性、相关性和丰富度，且多轮反馈优于单轮。  
   - **角色扮演机制**极大增强了剧本中人物对话的自然性和互动性，使剧本更具可读性和戏剧张力。

4. **对开源模型适用性分析**  
   - 多数小参数开源模型（如Llama-2-7B等）难以长期保持格式规范和复杂任务连贯性，需更强能力的LLM才能完整复现该流程。

<p align=center>
	<img src="/images/papers/2024-hollmwood/hollmwood-3.png" width="100%">
</p>

<p align=center>
	<img src="/images/papers/2024-hollmwood/hollmwood-4.png" width="100%">
</p>

## 总结

本论文提出的**HOLLMWOOD**框架，创新性地将多角色协作与角色扮演机制引入大语言模型驱动的自动剧本写作任务，实现了从初步故事线到完整剧本的全流程自动化，显著提升了剧本的连贯性、趣味性和人物表现力。实验结果充分证明，模拟真实人类创作的多智能体分工与反馈-修订、角色扮演等机制，是释放大语言模型创意写作潜力的有效路径。

**局限性与展望：**  
当前自动剧本生成仍存在情节冗余、长距离一致性不足等问题，且某些题材（如犯罪、恐怖）因模型对不良内容的自我规避而受限。未来可在提高LLM长文本控制力、细化场景和主题适应性、跨语言迁移等方向深入研究。

