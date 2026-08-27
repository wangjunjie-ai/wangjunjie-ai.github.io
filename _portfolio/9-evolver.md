---
title: "Evolver：基于 GEP 的智能体自进化引擎"
excerpt: "<img src='https://img.shields.io/github/stars/EvoMap/evolver?style=social' alt='GitHub stars'> 将智能体经验沉淀为可复用、可验证、可审计的 Gene、Capsule 与 Evolution Event。<br/><img src='/images/projects/evolver/figure-1.jpg' width='60%'>"
collection: portfolio
order: 9
---

<img src='https://img.shields.io/github/stars/EvoMap/evolver?style=social' alt='GitHub stars'> 项目地址：[https://github.com/EvoMap/evolver](https://github.com/EvoMap/evolver)

研究论文：[From Procedural Skills to Strategy Genes: Towards Experience-Driven Test-Time Evolution](https://arxiv.org/abs/2604.15097)

## 项目概述

Evolver 是一个由 **GEP（Genome Evolution Protocol）**驱动的智能体自进化引擎。它关注的不是让智能体在一次会话中“临时表现得更好”，而是把运行日志、失败模式与有效策略转化为可积累的演化资产，使后续智能体能够复用、验证和继续改进已有经验。

项目围绕三类核心对象组织演化过程：**Gene** 表达可复用的策略单元，**Capsule** 承载经过组合与验证的经验资产，**Evolution Event** 记录每次选择、变异和结果。它们共同把零散的 prompt 调整转化为具有来源、验证条件与审计轨迹的持续演化过程。

<p align=center>
  <img src="/images/projects/evolver/figure-1.jpg" width="100%">
</p>

## 我的角色与贡献

**角色：核心贡献者、创始贡献者。**

我参与了项目早期建设以及核心演化框架的设计与持续演进，重点围绕 Gene、Capsule 与 Event 建立经验积累、复用和验证机制，推动智能体从一次性交互走向可追踪、可审计的持续自进化。

我的工作关注两个问题：一是如何把运行过程中的有效经验压缩为可迁移资产，避免每次任务都从零开始；二是如何通过协议约束、验证命令和事件记录，让演化结果能够被复查、回滚和继续迭代，而不是退化为不可解释的自动改写。

## 核心机制

- **经验信号提取**：从 memory、历史记录和错误模式中识别值得复用或修复的信号。
- **Gene / Capsule 选择**：根据当前任务与运行信号匹配已有演化资产，减少无约束的自由生成。
- **协议化演化**：生成受 GEP 约束的演化提示，并通过 validation 与 solidify 流程检验结果。
- **事件留痕**：将演化过程写入 Evolution Event，保留选择依据、结果与后续可追踪状态。
- **跨智能体共享**：可通过 EvoMap 网络发布和获取演化资产，让局部经验进入协作式演化网络。

<p align=center>
  <img src="/images/projects/evolver/figure-2.jpg" width="100%">
</p>

## 项目价值与影响

Evolver 将“自进化”从宽泛的能力描述落实为一套可运行的资产协议：经验被结构化、验证并留下审计记录，既可以在本地离线使用，也可以接入 EvoMap 进行跨智能体协作。截至本页创建时，项目 GitHub Stars 已超过 **9K**，顶部徽章会随仓库数据动态更新。

需要特别说明的是，Evolver 本身主要负责提取信号、选择演化资产、生成协议化提示并记录事件；具体修改仍由宿主智能体或人工审查流程执行。这一边界使它更接近可审计的演化控制层，而不是无约束地自行修改代码的黑盒代理。
