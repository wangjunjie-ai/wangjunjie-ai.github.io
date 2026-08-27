---
title: "💭🚩 AutoResearch: Insight In, Hallucination Out"
collection: publications
category: arxiv
permalink: /publication/2026-08-18-autoresearch
excerpt: 'Autonomous Research, Multi-Agent Systems, Idea Generation, Evidence-Grounded Execution, Independent Verification, Scientific Discovery'
date: 2026-08-18
venue: 'Arxiv'
paperurl: 'https://arxiv.org/abs/2608.17906'
bibtexurl: # empty
citation: # empyty
slidesurl: # empyty
---

Arxiv地址：[https://arxiv.org/abs/2608.17906](https://arxiv.org/abs/2608.17906)

GitHub：[https://github.com/EvoMap/AutoResearch](https://github.com/EvoMap/AutoResearch)

## 1. 关键词 (Keywords)

* Autonomous Research / 自主科研
* Multi-Agent Research System / 多智能体科研系统
* Idea Generation / 研究想法生成
* Mechanism Transfer / 机制迁移
* Evidence-Grounded Execution / 证据驱动执行
* Independent Verification / 独立验证
* Stateful Workflow / 有状态工作流
* Negative Results / 负结果保留

## 2. 背景与动机 (Background & Motivation)

### 从“自动完成更多步骤”转向“做出有依据的研究判断”

自主科研系统已经可以把目标拆成假设、代码、实验与报告，但流程更长、人工介入更少，并不自动意味着研究更可靠。一个实现错误、测量口径错误或结果解释偏差，只要被后续智能体当作既定事实，就可能沿长链条逐步固化，最后形成叙述完整却缺乏实验支持的结论。论文把这种现象称为系统层面的 hallucination。

AutoResearch 因此不把“端到端自动化率”作为唯一目标，而是追问两个互补的问题：一个研究想法为什么值得测试，以及一个实验结论为什么值得接受。前者要求想法能回溯到新出现的研究信号、领域知识与可迁移机制；后者要求结论能回溯到真实环境输出、持久化工件和独立审查。

### Idea Generation 与 Idea Execution 的双重 grounding

已有系统常从用户给定的想法、任务或实验上下文开始，重点优化规划和执行。AutoResearch 把上游的研究发现也纳入系统边界：持续整合外部信号与本地域知识，经多模型生成、交叉审查与新颖性核验后，形成可证伪的研究计划；计划进入执行阶段后，再通过有状态任务图、实验诊断和证据门控决定继续、修改、扩展或停止。

“Insight In, Hallucination Out”并不是声称系统可以消灭模型幻觉，而是一条过程约束：**研究承诺之前先验证 insight 是否有机制依据，接受结论之前再验证 evidence 是否足以支撑 claim**。

## 3. AutoResearch 系统设计 (System Design)

### 3.1 两阶段闭环：从研究语境到可核验结论

论文把时刻 $t$ 的研究语境写成 $C_t=(K_t,S_t)$：$K_t$ 是累积的领域知识，$S_t$ 是新出现的研究信号。Idea Generation 将研究语境与目标领域映射为假设 $h$ 和可执行计划 $p$；Idea Execution 则以 $(h,p)$ 初始化持久状态，在每一步执行动作、读取真实环境输出，并把计划、代码、观察、评论与证据更新到统一研究状态中。

<p align=center>
  <img src="/images/papers/2026-autoresearch/figure-1.jpg" width="80%">
</p>

Figure 1 的关键不是把多个 agent 串起来，而是显示了两道不同的质量门。上游从 signal collectors 经过去重、质量筛选和 Idea Forge，结合 domain knowledge base 形成研究计划；下游由 planner、coder、runner、reviewer/critic 和 closure 推进实验。Monitoring dashboard 只读取执行状态，不参与研究判断，避免可视化层反向成为新的决策源。

### 3.2 Idea Generation：寻找可迁移机制，而不是拼接热门术语

外部信号来自论文、代码仓库、研究社区和技术媒体，也包括 X、小红书等变化较快的平台。系统先利用来源质量先验、标准化、去重与模型筛选保留具有实质技术内容的信号，再把它们与本地域知识库相交。这里的目标不是直接复述热点，而是抽取能够脱离原场景、在目标领域重新检验的 mechanistic insight。

对每个研究 seed，多个生成器独立判断它是否能解决目标领域中的未解问题；若不存在实质机制迁移，可以显式返回 no-match。当前实现由 3 个前沿模型独立生成候选，再由 3 个 reviewer 交叉评审，至少获得 2 个正向意见才能继续。存活想法还要经过 freshness check 与 domain-consistency check，最终被压缩成“可证伪假设 + 首轮可执行实验计划”。

### 3.3 Idea Execution：任务图、持久状态与可恢复执行

执行阶段将计划表示为带依赖关系的任务图，只调度前置任务已完成的节点，并在依赖允许时并行运行。每个动作都必须产生真实环境观察或工件，例如日志、评测记录、checkpoint 或结果文件；这些信息写入持久状态，使中断后的项目从已验证进度恢复，而不是依赖一段不透明的长对话重新推断上下文。

当搜索空间适合并行探索时，执行层可以扩展为 swarm-style coordination：不同 agent 认领任务、交换中间结果并交叉验证关键输出。但并发只是搜索和执行手段，是否接受结果仍由后续证据门决定。

### 3.4 独立评审：把“产出结果”和“证明结果”分开

Reviewer 检查实现和实验协议是否仍忠实于原假设，critic 判断已有证据是否足以支撑结论。关键设计是 fresh-context evaluation：审查 agent 不继承生产者的推理轨迹，只接收假设、计划、实验工件与评价标准等必要材料，以降低对早期叙事的锚定。

评审输出为 `PASS`、`PARTIAL` 或 `FAIL`。只要不是 `PASS`，系统就进入 `DIAGNOSE`、`REVISE` 或 `RERUN`，而不是把异常结果解释掉后继续写结论。一个证据项由“执行动作、环境输出、持久工件”组成；claim 只有在相关证据子集通过独立验证后才可接受。

### 3.5 Evidence-conditioned closure：负结果也可以是完成态

AutoResearch 把实验输出视为观察，把审查通过的输出视为证据。依据当前证据，系统可以 `Continue`、`Revise`、`Scale` 或 `Stop`；停止时允许记录假设被支持、被证伪或证据不足。这样，负结果和不确定结果不必被强行包装成成功，而一个未经验证的正结果也不能因为生成它的 agent 自认完成就进入最终结论。

官方仓库将 Idea Generation、研究运行时、知识库、配置、日志和测试拆成可检查目录，并公开研究计划、代码、运行日志、指标、失败原因、critic report 与 blind review 的落盘路径。Idea Forge 要求至少 3 个不同底层模型参与独立生成与交叉审查；具体模型由用户配置，论文结论不应被理解为绑定某个固定模型组合。

## 4. 实验设计与结果 (Evaluation & Results)

### 4.1 三类场景与对比协议

论文用三类研究场景分别检验系统链路：RSICD 双向图文检索考察“想法能否转成可测进展”；矩阵乘法优化考察“能否拒绝不可靠的漂亮结果并修正测量”；3 个 Kaggle 任务考察“能否根据证据决定扩展、修改或停止”。在需要横向比较的场景中，AutoResearch 与 The AI Scientist、Agent Laboratory、R&D-Agent、AutoResearchClaw 接收相同研究目标和任务级实验契约。

评价不只看最终任务分数，还审计各系统生成的研究工件并统计确认后的 issue events。这比引用系统自己的完成声明更严格，但 issue 数量仍依赖审计定义、系统配置与单次运行轨迹，不能直接当作跨任务通用可靠率。

### 4.2 RSICD：生成想法能否带来可分解、可复核的增益

<p align=center>
  <img src="/images/papers/2026-autoresearch/figure-2.jpg" width="100%">
</p>

Figure 2(a) 对一个由 Idea Forge 生成并交叉验证的图文检索想法做逐阶段实验：baseline 的 mR 为 **32.84**；加入更强的全局图文对齐后达到 **33.89**，再加入文本引导的局部特征聚合后达到 **34.04**，最后加入显式实体—位置关联后达到 **34.69**，累计提升 **+1.85 mR**。同一协议下的单调增益说明候选想法可以拆成可检验组件，但它只验证这一想法在 RSICD 上的实例化，不等价于该机制已经跨数据集泛化。

Figure 2(b) 报告 AutoResearch 有 **5** 个 audit-confirmed issue events，少于 R&D-Agent 的 **11**、AutoResearchClaw 的 **15**、Agent Laboratory 的 **18** 和 The AI Scientist 的 **27**。它把最终性能与过程可靠性放在一起观察，支持“较好结果不是只靠最终数字包装出来”的判断；但论文未用大规模重复运行给出 issue rate 的统计置信区间，因此更适合作为受控案例证据，而不是系统排名的终局结论。

### 4.3 矩阵乘法：能否发现测量错误并拒绝过早结论

矩阵乘法实验先定义明确契约：$1024\times1024$ 的 FP32 乘法耗时低于 **200 ms**，相对两个数值参考的误差不超过 **$10^{-5}$**，并且 10 次 wall-clock 运行的变异系数低于 **20%**。这使“快、正确、稳定”都能被单独验证。

<p align=center>
  <img src="/images/papers/2026-autoresearch/figure-3.jpg" width="100%">
</p>

Figure 3(a) 中，初始 pilot 已满足速度和数值精度，却因稳定性 gate 失败而没有被接受。诊断发现，多线程 BLAS 环境下 CPU time 被误当成 elapsed wall-clock time；修正计时口径并重跑后，系统建立了可复现的 **3.4 ms** baseline，对应 **626 GFLOPS**，约有目标阈值 **58 倍**的速度余量。最有价值的不是 3.4 ms 本身，而是系统没有把第一次出现的漂亮数字直接升级为科研结论。

Figure 3(b) 中，AutoResearch 记录 **4** 个确认问题；R&D-Agent 与 Agent Laboratory 均为 **5**，AutoResearchClaw 为 **7**，The AI Scientist 为 **8**。这里的领先幅度小于 RSICD，稳妥结论是 AutoResearch 在该案例中成功发现并修复了自己流程内的关键测量错误，同时保持较少的审计问题，而不是已经证明它在所有系统优化任务上都更可靠。

### 4.4 Kaggle：何时扩展、何时修改、何时停止

<p align=center>
  <img src="/images/papers/2026-autoresearch/figure-4.jpg" width="100%">
</p>

Figure 4 展示三种不同 closure。Titanic 的五折交叉验证准确率从 **0.822** 提升到 **0.843**，超过 **0.830** 目标，因而进入 scale-up；House Prices 的 RMSLE 从 **0.2008** 降到 **0.1251**，接近但未达到 **0.120**，结论是继续 revise；Disaster Tweets 的 F1 从 **0.763** 升到 **0.805**，仍低于 **0.835**，且后期收益趋于停滞，因此停止并保留负结果。该实验验证的是 evidence-conditioned decision，而不是三个数据集上的最高分竞争。

### 4.5 运行规模与筛选漏斗

论文还报告了一个连续一周的运行点：在双 Intel Xeon Platinum 8563C（98 核 / 196 线程）、8 张 NVIDIA L20 和 944 GiB 内存的单服务器上，系统约生成 **2,584** 个候选想法；经多模型审查后约 **355** 个进入实验队列，约 **22** 个被自动执行，最终约 **14** 个得到实证验证。

这些数字说明系统通过多级筛选把宽搜索压缩成少量实验承诺，也暴露了成本与吞吐边界：它们来自一个具体硬件、模型服务和任务分布下的 operating point，并非标准化效率 benchmark。论文提出把每轮已验证证据回写到知识状态的更新式，但持续自我更新的闭环仍属于未来工作，而不是当前实验已经证明的能力。

## 5. 总结与贡献 (Conclusion & Contribution)

AutoResearch 的核心贡献是把自主科研重新表述为两次 grounding：先用演化研究信号、领域知识、机制迁移和多模型交叉审查约束“做什么研究”，再用真实环境工件、独立验证和显式 closure 约束“什么结论可以成立”。任务图、持久状态与多 agent 协作是执行基础，而 evidence gate 才是连接系统设计与论文主张的关键。

三组实验分别给出互补证据：RSICD 展示生成想法可以转成逐步可测的 **+1.85 mR**；矩阵乘法案例展示系统能拒绝不稳定结果并纠正计时错误；Kaggle 轨迹展示达到目标、接近目标与收益停滞时可以产生不同后续决策。它们说明负结果、修正和停止都能成为有证据的科研产物，而不必把每条路线续写成成功故事。

我的判断是，这篇工作最重要的价值不在“AI 已经可以独立做科研”的宏大结论，而在提出了一套可落盘、可恢复、可独立复查的 research runtime。它把科研 agent 的评价重点从最终文本和最高分移向**研究承诺是否有机制依据、实验结论是否有可追溯证据**。后续更值得关注的是：如何标准化 issue audit、量化 critic 的独立性与漏检率、在不同预算下比较发现效率，以及让已验证证据安全地回流到下一轮知识状态。
