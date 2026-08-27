---
title: "💭🚩 Simple-OPD: Demystifying Warm-up for On-policy Distillation"
collection: publications
category: arxiv
permalink: /publication/2026-08-07-simple-opd
excerpt: 'On-Policy Distillation, Warm-up, Chain-of-Thought, Teacher Compatibility, LoRA, Reasoning Models'
date: 2026-08-07
venue: 'Arxiv'
paperurl: 'https://arxiv.org/abs/2608.06802'
bibtexurl: # empty
citation: # empyty
slidesurl: # empyty
---

Arxiv地址：[https://arxiv.org/abs/2608.06802](https://arxiv.org/abs/2608.06802)

GitHub：[https://github.com/Utaotao/Simple-OPD](https://github.com/Utaotao/Simple-OPD)

## 1. 关键词 (Keywords)

* On-Policy Distillation (OPD) / 在策略蒸馏
* Warm-up Initialization / 预热初始化
* Chain-of-Thought (CoT) / 思维链
* Teacher Compatibility / 教师兼容性
* Low-Rank Adaptation (LoRA) / 低秩适配
* In-Domain Adaptation / 域内适配
* Out-of-Domain Generalization / 域外泛化
* Reasoning Model Distillation / 推理模型蒸馏

## 2. 背景与动机 (Background & Motivation)

### OPD 的优势与初始化难题

On-policy distillation（OPD）让学生模型先对训练提示自行采样，再由固定教师在这些学生生成的上下文上提供 token-level 监督。与只学习静态教师回答的 off-policy 蒸馏相比，这种训练信号更贴近学生当前真正会访问的状态；但当学生的早期 rollout 很少落入教师熟悉的生成空间时，教师给出的分布也可能偏置甚至有害。

常见缓解方式是在 OPD 前先做一段监督微调，把学生拉到更适合接受教师信号的位置。问题在于，既有工作通常把这段 warm-up 当作固定的工程步骤，尚未充分回答三个直接影响训练效果的问题：warm-up 是否必须包含 CoT、应该由谁生成、以及轨迹答案是否必须正确。即使数据选对了，full-parameter SFT、LoRA 与训练时长也可能在域内适配和域外能力之间产生完全不同的取舍。

<p align=center>
  <img src="/images/papers/2026-simple-opd/figure-1.jpg" width="80%">
</p>

Figure 1 将论文的改动边界画得很清楚：Vanilla OPD 直接从基础学生开始蒸馏；Simple-OPD 先用 OPD 教师生成的 CoT 对学生进行 LoRA warm-up，再进入完全标准的 OPD。它不修改 OPD 的目标函数，而是改变学生进入 OPD 时的初始化位置，因此是一种可插拔的训练 recipe，而不是新的蒸馏损失。

### 论文要验证的核心假设

论文把 warm-up 拆成“数据”和“训练”两个维度，并提出一个比“先把答案做对”更细的假设：有效预热的主要作用，可能是让学生获得与下游教师兼容的思考模式，而不只是记住正确答案。围绕这一点，作者依次比较有无 CoT、OPD 教师与更强外部模型生成的 CoT、正确与错误教师 rollout，以及 full SFT 与不同 rank、不同训练时长的 LoRA。

## 3. Simple-OPD 方法 (Core Methodology)

### 3.1 先确定 warm-up 数据：CoT 比最终答案更关键

主分析使用 Qwen3-1.7B-Base 作为学生，使用在 DAPO-Math-17K 上训练的 Qwen3-8B-Base 作为教师；warm-up prompt 与后续 OPD prompt 都来自 DAPO-Math-17K。作者从同一 prompt 分布构造不同监督版本，并让每个 warm-up checkpoint 继续训练 75 个 OPD steps，从而比较的不是单独 SFT 结果，而是它能否提供更好的 OPD 起点。

<p align=center>
  <img src="/images/papers/2026-simple-opd/figure-2.jpg" width="80%">
</p>

Figure 2 显示，在相同 SFT step 下，保留 CoT 的 checkpoint 始终强于只保留最终答案的版本，而且这种优势会延续到后续 OPD。到 SFT step 100，CoT warm-up 的平均分约为 **31.3**，75 步 OPD 后为 **31.4**；无 CoT 版本则从约 **15.5** 恢复到 **23.6**。附录给出的逐 benchmark 结果同样明显：两者在后续 OPD 后的 AIME24 / AIME25 / MATH-500 分别为 **12.7 / 8.5 / 73.7** 与 **5.8 / 3.5 / 61.4**。这说明 OPD 能修复一部分弱初始化，却不能稳定补回缺失的推理过程监督。

### 3.2 CoT 来源：下游教师的一致性高于外部模型的独立强度

论文在相同 prompt 上比较 OPD 教师和 GPT-5.5 生成的 CoT。这里的关键控制变量是：后续 OPD 始终由同一个 Qwen3-8B 教师提供信号，只改变 warm-up 轨迹的来源。

<p align=center>
  <img src="/images/papers/2026-simple-opd/figure-3.jpg" width="80%">
</p>

Figure 3 中，OPD 教师生成的 CoT 随 warm-up 持续提高学生表现，而 GPT-5.5 CoT 虽来自更强外部模型，却让学生基本停留在初始水平。到 SFT step 100，教师 CoT 的 SFT / 后续 OPD 平均分约为 **31.3 / 31.4**，GPT-5.5 CoT 则约为 **17.5 / 26.7**。更准确的结论不是“更强教师无用”，而是当前对照表明：**warm-up 教师与下游 token-level 教师之间的生成兼容性，比 warm-up 教师的独立能力更重要**。

### 3.3 Rollout 正确性：思考骨架可以与局部答案错误分离

为了避免把“来源不同”与“正确率不同”混在一起，作者从同一个 OPD 教师、同一批 prompt 中配对采样正确和错误 CoT，并在这一消融中加入 AMC23，与 AIME24、AIME25、MATH-500 一起取平均。

<p align=center>
  <img src="/images/papers/2026-simple-opd/figure-4.jpg" width="80%">
</p>

Figure 4 显示，两种 warm-up 的 SFT 曲线多数 checkpoint 相差不到 1 分；完成后续 OPD 后，两组最终平均分都落在 **35.2–36.5** 的窄区间，且没有一组持续占优。附录案例说明，一条错误轨迹仍可能保留与正确轨迹相同的问题分解、中间计算和自检结构，只因局部算术错误得到错误答案。因此，这里的“错误 rollout 也有效”应理解为**教师兼容的推理结构对初始化很重要**，而不能外推成任意错误、噪声或低质量 CoT 都适合训练。

### 3.4 再确定训练方式：LoRA 约束更新范围

full-parameter SFT 能快速提高域内数学表现，但也可能重写过多预训练能力。论文将 direct OPD、full SFT warm-up 与 LoRA rank 16 / 32 / 64 放在同一 OPD 训练轨迹中比较；域内指标取 AMC23、MATH-500、AIME24、AIME25 的平均，域外指标取 IFEval、GPQA-Diamond、HumanEval 和 MMLU-Pro 的 Chemistry / Physics / History 子集平均。

<p align=center>
  <img src="/images/papers/2026-simple-opd/figure-5.jpg" width="100%">
</p>

Figure 5 展示了明显的 Pareto 取舍：direct OPD 的域内能力提升较慢，域外表现则早早达到峰值后下降；full SFT 在进入 OPD 前已有较高域内分数，却造成持续且难以恢复的 OOD 损失。三种 LoRA rank 最终得到接近的域内表现，但 OOD 明显强于 full SFT，其中 rank 16 的域外轨迹最好。因而 LoRA 在这里不只是节省参数，也像一个限制 warm-up 干扰范围的结构性正则。

### 3.5 训练到接近饱和，而不是越久越好

作者固定 LoRA rank 为 32，比较 40、100、150 与 175 个 warm-up steps。短预热不足以建立明显优势；较长预热同时改善域内收敛与域外保持，但收益不随时长单调增加。

<p align=center>
  <img src="/images/papers/2026-simple-opd/figure-6.jpg" width="100%">
</p>

Figure 6 中，**150 steps** 提供最好的 ID–OOD 平衡，**175 steps** 略偏向更高 ID 表现。充分 warm-up 的模型约在 100 个 OPD steps 后接近稳定域内水平，而 direct OPD 要到约 200 steps 仍在改善。论文据此推荐“低 rank、训练到接近饱和”的 LoRA，而不是简单最大化训练时长。

### 3.6 最终 recipe 与实现细节

Simple-OPD 的最终流程可以压缩为三步：从下游 OPD prompt 分布抽样；让同一个 OPD 教师生成带 CoT 的回答；用较低 rank 的 LoRA 将学生训练到接近饱和，再接标准 OPD。warm-up 阶段仍使用普通 token-level SFT 交叉熵，OPD 阶段在学生自己采样的 context 上最小化 student-to-teacher reverse KL。

论文的主配置中，SFT batch size 为 16，full fine-tuning 与 LoRA learning rate 分别为 `5e-6` 和 `5e-5`；OPD global / mini batch size 均为 128，每个 prompt 采样 1 条 rollout，最大 prompt / response 长度为 2,048 / 8,192，temperature 与 top-p 均为 1.0，learning rate 为 `1e-6`，额外 KL coefficient 为 0。训练实验基于 verl 与 vLLM，并在 8 张 GPU 上运行。

## 4. 实验设计 (Experimental Design)

### 模型与任务设置

论文没有只在单一师生对上报告结果，而是覆盖四类设定：

* **主 warm-up 分析**：Qwen3-1.7B-Base 学生与 DAPO-Math-17K 后训练的 Qwen3-8B-Base 教师；
* **不同 OPD 目标**：vanilla OPD、G-OPD 与 PowerOPD，使用 non-thinking Qwen3-1.7B / Qwen3-4B 师生组合；
* **thinking 模型**：Qwen3-0.6B thinking 学生与 Qwen3-4B-Thinking-2507 教师；
* **同规模能力整合**：DeepSeek-R1-Distill-Qwen-1.5B 学生与 RL 后训练的 JustRL-DeepSeek-1.5B 教师。

域内评测主要覆盖 MATH-500、AMC23、AIME24 与 AIME25；域外评测覆盖 IFEval、GPQA-Diamond、HumanEval 以及 MMLU-Pro 的物理、化学、历史子集。主数据消融对 MATH-500 使用 `avg@4`，对 AIME24 / AIME25 使用 `avg@16`。这种设计同时观察“数学能力是否转移”和“预训练通用能力是否被破坏”，比只报告一个域内终点分数更能支持 warm-up recipe 的选择。

### 评测边界

不同扩展实验使用的 ID / OOD 聚合项并不完全相同。例如 Table 1 的 ID 只平均 AIME24 与 AIME25，OOD 不含 HumanEval；Table 2 的 ID 则包含四个数学集合。因此，表内的 Simple-OPD 对比是可解释的，但不应直接横向比较不同表的平均分大小。

## 5. 实验结果与分析 (Results & Analysis)

### 5.1 对不同 OPD objective 的兼容性

<p align=center>
  <img src="/images/papers/2026-simple-opd/table-1.jpg" width="100%">
</p>

Table 1 中，Simple-OPD 将 vanilla OPD 的 ID 平均分从 **38.34** 提高到 **39.69**，OOD 从 **47.43** 提高到 **48.96**；G-OPD 的 ID 从 **41.56** 提高到 **43.13**，OOD 从 **44.71** 略降到 **44.61**；PowerOPD 的 ID 从 **39.06** 提高到 **40.01**，OOD 从 **46.80** 提高到 **47.63**。这支持“初始化收益不依赖某一种 OPD loss”，但也显示收益不是每个 benchmark 都同向，尤其 G-OPD 的 OOD 只能说基本持平。

### 5.2 Thinking 模型上的结果

<p align=center>
  <img src="/images/papers/2026-simple-opd/table-2.jpg" width="100%">
</p>

Table 2 中，direct OPD 已将学生的 ID 平均分从 **37.94** 提高到 **42.36**，Simple-OPD 进一步达到 **43.81**；OOD 平均分也由 OPD 的 **35.43** 提高到 **36.28**。提升主要来自 AMC23（**54.37 → 57.19**）、MATH-500（**78.80 → 81.80**）、AIME25（**22.08 → 23.33**）、IFEval（**29.76 → 30.87**）与 GPQA（**24.24 → 26.77**）；AIME24 和 MMLU-Pro Chemistry 则下降。这比只写“thinking setting 一致提升”更准确：聚合分提高成立，但单任务并非全部受益。

### 5.3 同规模教师与训练动态

在 1.5B 同规模能力整合中，direct OPD 将 ID 平均分从 **49.59** 提高到 **62.72**，Simple-OPD 再提高到 **64.34**；OOD 则从 OPD 的 **32.35** 小幅降到 **31.93**。这表明方法不要求教师参数量更大，但“基本保持 OOD”仍包含 **-0.42** 的实际代价。

训练动态提供了另一个侧面的证据：full SFT 与 LoRA warm-up 都以更高 reward 开始，response length 更早稳定，并减少训练早期 student / teacher top-32 token 集合 overlap ratio 的大幅波动；充分训练后，不同初始化逐渐进入相近区间。由此更稳妥的解释是 warm-up **加快并稳定早期 OPD**，而不是让最终可达上限无限提高。

MATH-500 案例中，教师与 warm-up 模型都会显式复核中间结果或重新计算，而无 warm-up 模型虽然推导路径看似合理，却因缺少复核保留了局部计数或算术错误。这与“迁移教师式验证行为”的假设一致，但案例是质性证据，不能单独证明所有性能提升都由自检行为造成。

## 6. 总结与贡献 (Conclusion & Contribution)

Simple-OPD 最重要的贡献不是增加一个复杂模块，而是把 OPD warm-up 从经验性的“先做点 SFT”整理成一组有诊断性的设计原则：使用下游教师生成的 CoT，让学生先接近教师的思考分布；用低 rank LoRA 限制对预训练能力的干扰；训练到接近饱和，并在 ID–OOD Pareto 前沿选择 checkpoint；随后保持 OPD objective 不变。

实验证据中，最有解释力的不是单个最高分，而是三组相互衔接的消融：有 CoT 明显优于只有答案；同一个 OPD 教师优于更强但不一致的外部 CoT 来源；同一教师的错误与正确 rollout 在当前设置下效果接近。它们共同把 warm-up 的作用从“灌入正确答案”推进到“建立可被后续教师有效监督的生成轨迹”。

我的判断是，这篇工作更像一份可操作的 OPD 初始化研究，而不是一个已经封闭的理论解释。它给出了简单、公开且跨多种 OPD 设置可复用的 recipe，也明确暴露了下一步值得研究的问题：如何在训练前量化师生轨迹兼容性、如何自动选择 near-saturation checkpoint，以及错误 CoT 的有效范围何时从结构迁移转变为错误放大。
