---
permalink: /
title: "About me"
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

<img src="/images/avatar-logo.jpg" alt="Junjie Wang avatar" style="float: left; width: 96px; margin: 0 16px 8px 0;">

**Junjie Wang (王军杰)** is currently a **postdoctoral researcher** at the [IIGROUP Lab](https://iigroup.github.io/), [Tsinghua University](https://www.tsinghua.edu.cn/en/), supervised by [**Prof. Yujiu Yang**](https://iigroup.github.io/about/).
His research focuses on **Verification-Driven Learning for Reliable Agents** (面向可靠智能体的验证驱动学习): how large language models and multimodal agents can continuously learn from verifiable feedback across document understanding, tool use, code execution, graphical user interfaces, and multimodal interaction. He received his Ph.D. in Engineering from [Waseda University](https://www.waseda.jp/top/en/), under the supervision of [**Prof. Tetsuya Sakai**](http://sakailab.com/tetsuya/).

<div style="clear: both;"></div>

Email: wangjunjie@sz.tsinghua.edu.cn (**Please state your purpose / 请您注明来意**)

📰 **News / 最近**

- [06/2026] 🏅 Selected as an ICML 2026 Golden Reviewer.
- [04/2026] 📜 1 paper is accepted to ICML 2026 !
- [04/2026] 📜 2 papers are accepted to ACL 2026 !
- [03/2026] 📜 1 paper is accepted to TMLR ! 获选CAAI-腾讯犀牛鸟研究计划 !
- [01/2026] 🎉 ROCO@AAAI2026 决赛冠军: [URL](https://wangjunjie-ai.github.io/portfolio/8-roco/)
- [01/2026] 📜 1 paper is accepted to ICLR 2026 !
- [11/2025] 📜 1 paper (Oral) is accepted to AAAI 2026 !

🌌 **Research Vision / 研究愿景**

### Verification-Driven Learning for Reliable Agents
### 面向可靠智能体的验证驱动学习

**From Benchmark-to-Model Feedback to Real-World Interaction**<br>
**从基准到模型反馈，再到真实世界交互**

My research studies how to build reliable agents through verification-driven learning. Different from evaluation that only reports final answers or static leaderboards, I treat benchmarks as model feedback systems: verifiable task environments should expose process-level failures in evidence use, tool calling, code execution, GUI operation, long-horizon planning, and safety constraints; these diagnoses should then be compiled into learning signals for data construction, post-training, preference learning, process rewards, and regression testing; finally, reliability gains should be validated in real-world interactive tasks.

我的研究关注如何构建可靠智能体，并将“验证驱动学习”作为核心路径。与传统只关注最终答案或静态排行榜的评测不同，我将 benchmark 视为模型反馈系统：通过设计可验证任务环境，暴露智能体在证据使用、工具调用、代码执行、GUI 操作、长程规划和安全约束中的过程性失败；再将这些失败诊断转化为模型可学习的信号，用于数据构造、后训练、偏好学习、过程奖励和回归测试；最终在真实交互任务中验证模型可靠性的持续提升。

**Core loop / 核心闭环**

Verifiable Tasks → Process-Level Diagnosis → Feedback Compilation → Model Post-Training → Reliable Agent Applications → Generalizable Principles ↺ Benchmark Redesign

可验证任务环境 → 过程级失败诊断 → 反馈信号编译 → 模型后训练与对齐 → 可靠智能体应用 → 基础规律抽象 ↺ 基准重新设计

🔎 **Core Methodology / 核心方法论**

My core methodology is **Benchmark-to-Model Feedback**: designing benchmarks not as static leaderboards, but as feedback systems that diagnose agent failures and convert them into model improvement signals.

我的核心方法论是 **Benchmark-to-Model Feedback**：不是将 benchmark 仅作为静态排行榜，而是将其作为反馈系统，用于诊断智能体失败并转化为模型改进信号。

- **Diagnostic evaluation / 诊断型评测**: expose concrete failures in evidence use, tool calling, code execution, GUI interaction, planning, and safety.
- **Feedback compilation / 反馈信号编译**: turn failures into supervision, preference pairs, process rewards, hard negatives, curricula, and regression tests.
- **Model improvement / 模型改进**: use these signals for post-training, alignment, error recovery, and reliable deployment in real interactive tasks.

🧭 **Research Areas / 研究方向**

1. **Verifiable multimodal and scientific document understanding / 可验证多模态与科学文档理解**<br>
   Evidence-grounded reading, long-context multimodal literature, chart understanding, and executable reproduction.

2. **Reliable tool, code, and GUI agents / 可靠工具、代码与 GUI 智能体**<br>
   Tool-use honesty, repository-level code execution and security, GUI state tracking, and long-horizon interactive workflows.

3. **Feedback learning and post-training / 反馈学习与后训练**<br>
   High-value supervision selection, process supervision, preference learning, process rewards, and regression-tested capability improvement.

4. **Real-world interactive intelligence / 真实世界交互智能**<br>
   Knowledge work, creation/editing, tool-using automation, multimodal navigation, embodied intelligence, and autonomous systems.

✒️ **Recent Professional Services / 最近的专业服务**

- Golden Reviewer: ICML 2026
- Area Chair: ACL ARR 2025 October (EACL); ACL ARR 2026 January (ACL); ACL ARR 2026 March (EMNLP).
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
