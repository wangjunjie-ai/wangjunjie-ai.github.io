---
title: "💭🚩 OneLatent: Single-Token Compression for Visual Latent Reasoning"
collection: publications
category: arxiv
permalink: /publication/2026-02-14-onelatent
excerpt: 'Latent Reasoning, Chain-of-Thought Compression, Visual Supervision, DeepSeek-OCR, Minimum Description Length, Reasoning Efficiency'
date: 2026-02-14
venue: 'Arxiv'
paperurl: 'https://arxiv.org/abs/2602.13738'
bibtexurl: # empty
citation: # empyty
slidesurl: # empyty
---

Arxiv地址：[https://arxiv.org/abs/2602.13738](https://arxiv.org/abs/2602.13738)

## 1. 关键词 (Keywords)

* Latent Reasoning / 隐空间推理
* Chain-of-Thought Compression / 思维链压缩
* Single Latent Token / 单隐变量 token
* Visual Supervision / 视觉监督
* DeepSeek-OCR Hidden States / DeepSeek-OCR 隐状态
* Minimum Description Length / 最小描述长度
* Output Token Contribution / 输出 token 贡献率
* Reasoning Efficiency / 推理效率

## 2. 背景与动机 (Background & Motivation)

### 显式思维链的能力收益与部署成本

显式 Chain-of-Thought（CoT）能够提升多步推理，但模型必须逐 token 解码完整过程，输出长度、时延和 KV cache 都随推理链增长。更关键的是，长推理文本并不等于高密度计算：其中可能混有模板化表达、重复解释，甚至与模型真实内部计算不一致的事后叙述。

已有 iCoT、COCONUT 等方法尝试把推理迁移到连续隐状态，却通常需要多个 latent token，并可能在强压缩下损失准确率。OneLatent 追问一个更激进的问题：**能否把可变长度的显式 CoT 压进一个固定的连续 token，同时保留足以生成答案的信息？**

<p align=center>
  <img src="/images/papers/2026-onelatent/figure-1.jpg" width="100%">
</p>

Figure 1 将 No-CoT、文本 CoT、iCoT、COCONUT 与 OneLatent 放在同一接口视角下。OneLatent 的目标不是在测试时读取一张 CoT 图片，而是只在问题与答案之间保留一个 latent slot；视觉通道只负责训练监督。图中的低输出长度与较高 OTC 说明它把主要计算从可见文本移入隐藏状态，但并不直接证明隐藏推理更忠实或更可解释。

### 以最小描述长度约束推理接口

论文借用 Minimum Description Length（MDL）的直觉：当不同中间解释都能得到正确答案时，更短且充分的表示可以减少冗余支架，并形成更强的归纳偏置。OneLatent 并未直接优化 MDL，而是通过固定的单 token 接口施加严格信息预算，再用准确率与输出长度的折中检验“压缩约束下的泛化”。

## 3. OneLatent 方法 (Core Methodology)

### 3.1 从显式 CoT 到单 token 的三阶段课程

<p align=center>
  <img src="/images/papers/2026-onelatent/figure-2.jpg" width="100%">
</p>

Figure 2 展示了方法的核心递进关系。Stage 1 用显式 CoT 与答案做 next-token prediction，先建立可见推理能力；Stage 2 删除可见 CoT，插入一个 latent token，同时用答案损失与视觉隐状态的 MSE 对齐来压缩推理；Stage 3 去掉 MSE，只保留 answer-only 微调，使模型适应最终短输出接口。这个课程把“学会推理”“压缩推理”和“稳定作答”分开，避免一次性从长 CoT 跳到单 token。

在 Stage 2 中，总损失为答案 token 的自回归损失与 latent alignment loss 之和，默认权重 $\lambda=1$。对齐目标不是图片 patch，而是冻结 DeepSeek-OCR 视觉编码器和 LLM 主干处理渲染图后，最后一个视觉位置的隐藏状态。

### 3.2 单 latent segment 与连续填充

模型在问题与答案之间加入 `<|begin-latent|> <|latent|> <|end-latent|>`。所有报告实验都固定 $N=1$；在 latent 位置，其输入 embedding 被前一位置的隐藏状态覆盖，即 $e_{\ell}\leftarrow h_{\ell-1}$，从而让一次连续隐状态更新承担中间推理。

推理阶段复用完全相同的接口，只生成最终答案。若答案长度为 $T$、显式 CoT 长度为 $R$，则论文将解码开销概括为 OneLatent 的 $O(T+1)$ 对显式 CoT 的 $O(T+R)$。固定长度使 batching、KV cache 和运行时预算可预测，但也意味着模型无法按问题难度动态增加隐空间计算。

### 3.3 把 CoT 渲染为可审计的高密度监督

<p align=center>
  <img src="/images/papers/2026-onelatent/figure-3.jpg" width="100%">
</p>

Figure 3 对应离线数据准备链路：先把每条 CoT 以黑字白底、等宽字体渲染到固定画布，再交给冻结的 SAM-ViT-B 与 CLIP-L 视觉编码器；拼接、投影并通过 LLM 层后，抽取一个 $v\in\mathbb{R}^{d}$ 向量作为 Stage 2 监督。训练和推理本身始终只接收文本，因此视觉模型的额外开销发生在离线目标生成，而不是在线解码。

标准配置使用 $1024\times1024$ 画布、20 像素边距与 100 DPI。渲染器按画布约束搜索最大可用字号，必要时用 DeepSeek-OCR 检查可读性并调整 DPI 或边距。这个确定性过程使监督目标可以缓存和复核，也把方法性能绑定到 CoT 质量、字体布局、分辨率与 OCR 编码器。

## 4. 实验设计 (Experimental Design)

### 数据、模型与评价协议

训练使用约 **38.5 万条** GSM8K-Aug-NL 样本。标准评测覆盖 GSM8K、GSM8K-Hard、SVAMP、ProntoQA 和 ProsQA；长链测试另构造 ProntoQA Enhanced（290 条）与 ProsQA Enhanced（500 条），由 LLM 扩展 CoT 后再通过 LLM-as-Judge 校验正确性和推理深度。

基础模型采用 DeepSeek-OCR LLM，每个阶段训练 15 个 epoch，学习率为 $2\times10^{-5}$，以 8 张 GPU 做分布式训练，单卡 batch size 为 1。主指标是归一化 exact-match accuracy、平均输出 token 数，以及论文提出的 Output Token Contribution：$\mathrm{OTC}=\mathrm{Acc}/\mathrm{AvgOut}$。OTC 衡量每个已生成 token 对准确率的贡献，但不是 wall-clock latency、吞吐量或能耗的替代指标。

## 5. 结果与分析 (Results & Analysis)

### 5.1 五个标准推理数据集

<p align=center>
  <img src="/images/papers/2026-onelatent/table-1.jpg" width="100%">
</p>

Table 1 中，OneLatent 的平均准确率为 **52.7%**，与文本 CoT 的 **54.9%** 相差约 **2.21 个百分点**；平均输出从 **74.62** 个 token 降到 **6.78** 个，约为原来的 $1/11$。它在 ProntoQA 与 ProsQA 上达到 **99.80% / 97.80%**，但在 GSM8K、GSM8K-Hard、SVAMP 上分别只有 **24.8% / 4.58% / 36.5%**，均低于文本 CoT 的 **40.5% / 11.3% / 52.0%**。因此，最强证据是长链逻辑任务上的压缩，而不是“单 token 已普遍替代显式 CoT”。

与使用 6 个 latent token 的 COCONUT 相比，OneLatent 的平均输出更短（**6.78 vs. 12.6**），平均准确率略高（**52.7% vs. 51.8%**）；与 iCoT 相比，它在五个数据集上的准确率均更高。论文摘要报告相对文本 CoT 的 OTC 提升为 **6.8×**，而 Table 1 的平均行给出 OneLatent **7.77**、CoT **0.74**；两种汇总口径并未在表格附近充分解释，跨方法比较时应同时保留准确率与长度原值。

### 5.2 增强长链任务的压缩极限

<p align=center>
  <img src="/images/papers/2026-onelatent/table-2.jpg" width="100%">
</p>

Table 2 将约 800-token 的扩展 CoT 压缩到不足 10 个输出 token：ProntoQA Enhanced 从 **784.50** 降到 **8.98**，压缩 **87.4×**，准确率从 **99.80%** 到 **99.90%**；ProsQA Enhanced 从 **804.84** 降到 **9.98**，压缩 **80.6×**，准确率从 **97.80%** 到 **98.10%**。这些结果说明固定单 token 在结构清晰的逻辑/程序推理链上能够承载高度压缩的监督，但增强集来自 LLM 扩写与 judge 过滤，不能直接代表自然分布中的任意长推理。

### 5.3 三阶段训练是否各自必要

<p align=center>
  <img src="/images/papers/2026-onelatent/table-3.jpg" width="100%">
</p>

Table 3 显示 Stage 2 首先完成主要压缩：相对 Stage 1，GSM8K、ProntoQA、ProsQA 的输出长度分别减少 **78.3% / 91.8% / 73.5%**，OTC 分别提高 **4.8× / 23.5× / 6.9×**。Stage 3 在几乎不改变输出长度的情况下继续提升准确率：三项任务分别从 **20.39% / 93.20% / 89.80%** 提高到 **24.79% / 99.80% / 97.80%**。这支持“对齐负责压缩、答案微调负责恢复可用性”的设计，但该表是阶段轨迹，并没有提供去除每个阶段后重新训练的完整因果消融。

## 6. 总结与贡献 (Conclusion & Contribution)

OneLatent 的核心贡献是把“视觉压缩”从输入上下文压缩转成隐空间推理监督：显式 CoT 被确定性渲染并编码成一个训练目标，模型随后只用一个连续 token 在纯文本接口中完成推理。这一设计把运行时推理预算固定下来，同时以三阶段课程缓解从长文本到单向量的优化断层。

在 ProntoQA / ProsQA 及其增强长链版本上，单 token 可以把数百个 CoT token 的输出压缩 **80.6–87.4×**，并保持接近饱和的准确率；跨五个标准任务，平均输出压缩约 **11×**，准确率只下降约 **2.21 个百分点**。与此同时，算术任务退化、有限评测规模以及缺少端到端系统测量，限定了当前结果的外推范围。

OneLatent 更像一种**固定预算的 reasoning bottleneck**，而不是对显式 CoT 的普遍替代。它说明高密度跨模态监督可以帮助模型内化一部分推理轨迹，下一步更关键的问题是：能否让 latent budget 随难度自适应、在保持短输出的同时恢复可诊断性，并在更大模型和更开放任务上验证真实的时延与泛化收益。
