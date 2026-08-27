---
title: "AutoResearch：从 Idea 到 Paper-Ready Evidence 的 AI/ML 研究智能体"
excerpt: "<img src='https://img.shields.io/github/stars/EvoMap/AutoResearch?style=social' alt='GitHub stars'> 将研究想法生成、实验执行与独立验证组织为可追踪、可恢复的自主科研闭环。<br/><img src='/images/projects/autoresearch/figure-1.jpg' width='60%'>"
collection: portfolio
order: 10
---

<img src='https://img.shields.io/github/stars/EvoMap/AutoResearch?style=social' alt='GitHub stars'> 项目地址：[https://github.com/EvoMap/AutoResearch](https://github.com/EvoMap/AutoResearch)

论文地址：[https://arxiv.org/abs/2608.17906](https://arxiv.org/abs/2608.17906)

## 项目概述

AutoResearch 是一个面向 AI/ML 研究的自主智能体系统，将研究信号、领域知识、实验规划、代码执行、结果分析与独立验证组织为可追踪、可恢复的端到端工作流。它既可以从一个已有研究想法开始，也可以从近期论文、开发者社区和开源趋势中发现候选方向。

项目的目标不是让智能体更快地产生“像论文的文本”，而是生成可供研究者复核的 **paper-ready evidence**：研究计划、代码、运行日志、指标、失败原因、critic report 与 blind review 都被持久化保存，使实验可以中断恢复，也允许研究者随时接管或停止。

<p align=center>
  <img src="/images/projects/autoresearch/figure-1.jpg" width="100%">
</p>

## 我的角色与贡献

**角色：核心贡献者、项目负责人、通讯作者。**

我参与了整体研究框架与系统设计，重点推动从研究想法生成、实验执行到独立验证的闭环，以及多模型交叉评审、过程诊断与证据留存机制，提升自主研究过程的可靠性并降低幻觉风险。

其中，我特别关注研究系统中的两类 grounding：在 Idea Generation 阶段，让候选想法能够回溯到外部研究信号、领域知识和可检验机制；在 Idea Execution 阶段，让结论能够回溯到真实环境输出、实验工件和独立审查，而不是依赖生成智能体自己的完成声明。

## 核心流程

- **Idea Generation**：聚合并筛选外部研究信号，与本地域知识相交后生成候选想法和实验计划。
- **多模型交叉评审**：由至少三个不同底层模型独立生成并交叉审查，降低单一模型自我确认带来的偏差。
- **有状态实验执行**：持久化计划、代码、队列、日志和结论，通过 pilot 先验证可行性，再决定扩展、修改或停止。
- **独立证据验证**：由 reviewer、critic 和 blind review 检查实现、指标与结论之间是否存在真实证据链。
- **负结果保留**：当假设失败或证据不足时，允许以可追踪的负结果结束，而不是把每条实验路线包装成成功。

<p align=center>
  <img src="/images/projects/autoresearch/figure-2.jpg" width="100%">
</p>

<p align=center>
  <img src="/images/projects/autoresearch/figure-3.jpg" width="100%">
</p>

## 项目价值

AutoResearch 将自主科研的重点从“自动完成多少步骤”转向“研究判断是否有依据”。多智能体编排负责扩大搜索与执行能力，而可恢复状态、真实实验工件和独立 evidence gate 决定一个结论能否被接受。

这套系统不能保证每个研究结论都正确，但它保留了研究者复核所需的来源、状态和证据，使研究过程中的失败、修正与停止同样能够成为可审计的科研产物。
