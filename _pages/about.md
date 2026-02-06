---
permalink: /
title: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

<img src="/images/avatar-logo.jpg" width="10%">

**Junjie Wang (王军杰)** is currently a **postdoctoral researcher** at the [IIGROUP Lab](https://iigroup.github.io/), [Tsinghua University](https://www.tsinghua.edu.cn/en/), supervised by [**Prof. Yujiu Yang**](https://iigroup.github.io/about/). 
His research interests include natural language processing, multimodal reasoning, and embodied intelligence. He received his Ph.D. in Engineering from [Waseda University](https://www.waseda.jp/top/en/), under the supervision of [**Prof. Tetsuya Sakai**](http://sakailab.com/tetsuya/).

Email: wangjunjie@sz.tsinghua.edu.cn (**Please state your purpose / 请您注明来意**)


📰 **News / 最近**

- [01/2026] 🎉 ROCO@AAAI2026 决赛冠军: [URL](https://wangjunjie-ai.github.io/portfolio/8-roco/)
- [01/2026] 📜 1 paper are accepted to ICLR 2026 !
- [11/2025] 📜 1 paper (Oral) are accepted to AAAI 2026 !

🌌 **Long-term Goal / 长期目标**

-> Practical Epistemology / 实践认识论 🧠

My long-term goal is to engineer (self-evolving) AGI as a form of Practical Epistemology: turning “knowing” into an operational, testable process. Concretely, I formalize cognition into structured representations, shape executable behaviors via post-training signal engineering, and make reasoning–action–creation verifiable through evidence, traces, and executable artifacts. “Self-evolving” means a reproducible closed loop—verification signals → training signals and data/task redesign → regression-tested capability gains—rather than unconstrained self-modification.

我的长期目标是将（自进化的）通用智能工程化为一种“实践认识论”：把“知道/理解”变成可操作、可检验、可复现的过程。具体而言，我将认知形式化为结构化表示，通过后训练的信号工程塑形可执行行为，并以证据链、过程轨迹与可执行产物对推理—行动—创造进行过程级验收。“自进化”指可复现闭环：验收信号 → 训练信号与数据/任务重构 → 回归测试下的能力累积，而不是无约束自我改写。

🔎 **Research Interests / 研究兴趣**

1. Structured Cognition / 结构化认知
2. Post-Training Behavior Shaping / 后训练行为塑形
3. Process Verification & Diagnosis / 过程验收与诊断
4. Self-Evolution Flywheel / 自进化飞轮

🌱 Derived Verticals / 落地方向 (AI for X)
- AI for Creation（创造/编辑）
- AI for Knowledge Work（知识/科学知识工作流）
- AI for Tool-Using Automation（工具/GUI/代码自动化）
- AI for Robots（机器人） 

✒️ **Recent Professional Services / 最近的专业服务**

- Area Chair: ACL ARR 2025 October (EACL 2026)
- Senior PC member: WSDM 2026
- Workshop Organiser: [SIGIR-AP 2025 BREV-RAG Workshop](https://dl.acm.org/doi/10.1145/3767695.3769523)

## Publications

Details in [Publications Page](https://wangjunjie-ai.github.io/publications/)

<p>Total Publications: {{ site.publications | size }}</p>

- ⭐: Co-first Author
- 🚩: Corresponding Author
- 💭: Under Review

<ul>{% for post in site.publications reversed %}
  {% include archive-single-cv.html %}
{% endfor %}</ul>


**Research Interests / 研究兴趣** 展开说明

1. Structured Cognition / 结构化认知
  - Task/interface unification: compositional formulations for reasoning, extraction, and selection
  - 任务/接口统一：将推理、抽取与选择统一为可组合表述
  - Multimodal interaction representations: structured grounding and cross-modal interaction modeling
  - 多模态交互表征：结构化 grounding 与跨模态交互建模
  - Reasoning primitives: multi-paradigm and cooperative reasoning as reusable cognitive mechanisms
  - 推理原语：多范式与协作推理的可复用认知机制
2. Post-Training Behavior Shaping / 后训练行为塑形
  - Supervision signal engineering: mining, selection, and reweighting of high-value learning signals
  - 监督信号工程：高价值学习信号的挖掘、筛选与重加权
  - Tool/retrieval alignment: learning transferable tool-using and decision behaviors under data constraints
  - 工具/检索对齐：在数据效率约束下学习可迁移的工具使用与决策行为
  - Capability injection & transfer: behaviors that generalize across substrates (text/code/GUI/tools)
  - 能力注入与迁移：跨载体（文本/代码/GUI/工具）的可泛化稳定行为
3. Process Verification & Diagnosis / 过程验收与诊断
  - Process-centric evaluation: stage-wise acceptance criteria beyond outcome-only scores
  - 过程导向评测：以分阶段验收标准替代单一结果分数
  - Executable verification interfaces: chart-to-code, long-horizon GUI traces, repository-level code tasks
  - 可执行验证接口：chart-to-code、GUI 长链轨迹、仓库级代码任务
  - Diagnostic taxonomies: structured failure modes for localization and regression testing
  - 诊断分类体系：结构化失败模式以支持定位与回归测试
4. Self-Evolution Flywheel / 自进化飞轮
  - Verification → training transformation: converting diagnostics into objectives, curricula, and data/task redesign
  - 验收信号→训练信号：将诊断转化为训练目标、课程与数据/任务重构
  - Loop stability & milestones: measurable stages and regression suites for cumulative generalization
  - 闭环稳定性与里程碑：用阶段性指标与回归测试集保障能力累积
  - Infrastructure for evolution: datasets/benchmarks/systems enabling reproducible iteration
  - 演化基础设施：数据/基准/系统资产支撑可复现迭代
