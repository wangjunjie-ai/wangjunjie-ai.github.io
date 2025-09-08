---
permalink: /
title: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

<img src="/images/avatar-logo.jpg" width="10%">

**Junjie Wang (王军杰)** is currently a **postdoctoral researcher** at the [IIGROUP Lab](https://sites.google.com/view/iigroup-thu), [Tsinghua University](https://www.tsinghua.edu.cn/en/), supervised by **Prof. Yujiu Yang**. 
His research interests include natural language processing, multimodal reasoning, and embodied intelligence. He received his Ph.D. in Engineering from [Waseda University](https://www.waseda.jp/top/en/), under the supervision of **Prof. Tetsuya Sakai**.

Email: wangjunjie@sz.tsinghua.edu.cn (**Please state your purpose / 请您注明来意**)

🌌 **Long-term Goal / 长期目标**

To create AI systems that emulate the principles of human reasoning and learning, allowing them to interact with the world and assist humanity in a safe, transparent, and beneficial manner.

创造能够模拟人类推理与学习原理的 AI 系统，使其能与世界交互，并以安全、透明和有益的方式协助人类。

🔎 **Research Interests / 研究兴趣**

1. Grounding in Reality: The Foundation of Understanding / 扎根现实：理解的基础
   - Embodied and Multimodal Learning / 具身与多模态学习
2. Human-like Cognition: The Core of Reasoning / 类人认知：推理的核心
  - Cognitive-inspired Reasoning and Language / 认知启发的推理与语言
  - Controllable and Explainable Generation / 可控与可解释生成
3. Alignment with Humanity: The Ethical Framework / 对齐人类：伦理的框架
  - Value Alignment and Social Norms / 价值观对齐与社会规范

## Publications

Details in [Publications Page](https://wangjunjie-ai.github.io/publications/)

<p>Total Publications: {{ site.publications | size }}</p>

- ⭐: Co-first Author
- 🚩: Corresponding Author
- 💭: Under Review

<ul>{% for post in site.publications reversed %}
  {% include archive-single-cv.html %}
{% endfor %}</ul>