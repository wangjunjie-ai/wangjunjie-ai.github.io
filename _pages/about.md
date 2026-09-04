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
His research focuses on **Learning to Reason for Self-Evolving Agents**: enabling agents to learn from knowledge, digital interaction, and physical-world consequences, and ultimately to improve not only their capabilities but also the mechanisms by which they improve. He received his Ph.D. in Engineering from [Waseda University](https://www.waseda.jp/top/en/), under the supervision of [**Prof. Tetsuya Sakai**](http://sakailab.com/tetsuya/).

<div style="clear: both;"></div>

Email: wangjunjie@sz.tsinghua.edu.cn (**Please state your purpose / 请您注明来意**)

📰 **News / 最近**

- [08/2026] 📜 8 papers are accepted to EMNLP 2026 !
- [06/2026] 🏅 Selected as an ICML 2026 Golden Reviewer.
- [04/2026] 📜 1 paper is accepted to ICML 2026 !
- [04/2026] 📜 2 papers are accepted to ACL 2026 !
- [03/2026] 📜 1 paper is accepted to TMLR ! 获选CAAI-腾讯犀牛鸟研究计划 !
- [01/2026] 🎉 ROCO@AAAI2026 决赛冠军: [URL](https://wangjunjie-ai.github.io/portfolio/8-roco/)
- [01/2026] 📜 1 paper is accepted to ICLR 2026 !
- [11/2025] 📜 1 paper (Oral) is accepted to AAAI 2026 !

🌌 **Research Vision / 研究愿景**

Learning to Reason: Toward Reasoning-Centric Recursive Self-Improvement

学会推理：迈向以推理为中心的递归自我改进

My central question is: **How can reasoning become a continually improving capability?** I study how agents learn to reason from knowledge, digital interaction, and physical-world consequences as human predefinition decreases and agent autonomy increases.

我的核心问题是：**如何让推理成为一种能够持续改进的能力？** 我关注智能体如何从知识、数字交互和物理世界后果中学习推理，并随着人类预定义减少而逐步提升自主性。

<p align="center">
  <img src="/images/intro.jpg" alt="Three stages from knowledge-grounded reasoning to interaction-grounded and physical-world reasoning" style="display: block; width: 80%; height: auto; margin: 1rem auto 0.5rem;">
</p>

<p align="center"><em>From human-defined knowledge to interaction feedback and real-world consequences.<br>从人类预定义知识，走向交互反馈与真实世界后果。</em></p>

🧭 **Three Reasoning Layers / 三层推理**

1. **Knowledge-Grounded Reasoning / 知识驱动推理** — Learn representations and explicit reasoning structures from human-curated data, evidence, and tasks.<br>
   从人类定义的数据、证据与任务中学习表征和显式推理结构。

2. **Interaction-Grounded Reasoning / 交互驱动推理** — Diagnose trajectories in tools, code, and GUIs, then convert verified feedback into capability updates.<br>
   诊断工具、代码与 GUI 中的交互轨迹，并将可验证反馈转化为能力更新。

3. **Physical-World Reasoning / 物理世界推理** — Reason about dynamics, actions, consequences, and safety in robotics and autonomous driving.<br>
   在机器人与自动驾驶中理解动力学、行动、后果与安全约束。

🔄 **Toward Reasoning-Centric RSI / 迈向以推理为中心的 RSI**

**Interaction → Verification → Attribution → Internalization → Capability Improvement ↺**

My long-term goal is **Reasoning-Centric Recursive Self-Improvement (RSI)**: agents that can verify which experiences are trustworthy, attribute success and failure, internalize high-value lessons, and eventually improve the mechanisms by which they improve.

我的长期目标是构建**以推理为中心的递归自我改进（Reasoning-Centric RSI）**：让智能体能够验证经验、归因成败、内化高价值反馈，并最终改进其自身的改进机制。

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
