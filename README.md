English | [中文](zh/README.md)

# 一天搞定 Diffusion Models · One-Day Trip to Diffusion Models

A systematic, engineering-oriented technical documentation series on Diffusion Transformers — from the DDPM foundations to DiT, adaLN-Zero, conditional diffusion, efficiency, and video/multimodal extensions. Available in Chinese and English.

一份系统、可核对、面向工程的 Diffusion Transformer 技术文档 —— 从 DDPM 的数学地基一路讲到 DiT、adaLN-Zero、条件扩散、效率优化与视频/多模态扩展。**中英双语。**

Documentation: [中文版目录](zh/README.md) ｜ [English Contents](en/README.md)

> **共 9 章（第 0–8 章）· 4,249 行 · 54,235 汉字 · 237 个编号小节 · 两版小节编号一一对应，内部链接全部校验通过。**

---

## 选择语言 · Choose your language

| | 中文 | English |
|:---:|---|---|
| **目录与阅读指南** | [**📖 中文版目录**](zh/README.md) | [**📖 English Contents**](en/README.md) |
| **规模** | 4,249 行 · 54,235 汉字 · 143,886 字符 | ~4,243 lines · 300,174 characters |
| **适合** | 中文母语 / 快速通读 | English readers / citation & terminology reference |

**直达各章 · Jump straight to a chapter**

| # | 中文 | English |
|:---:|---|---|
| 0 | [全局速览：一张技术演进图](zh/00-overview.md) | [Overview: One Diagram of the Evolution](en/00-overview.md) |
| 1 | [基础扩散模型（DDPM 谱系）](zh/01-diffusion-basics.md) | [Diffusion Basics (the DDPM Lineage)](en/01-diffusion-basics.md) |
| 2 | [从 U-Net 到 Diffusion Transformer](zh/02-dit-architecture.md) | [From U-Net to Diffusion Transformer](en/02-dit-architecture.md) |
| 3 | [AdaLN-Zero：自适应层归一化零初始化](zh/03-adaln-zero.md) | [AdaLN-Zero: Adaptive Layer Norm, Zero-Init](en/03-adaln-zero.md) |
| 4 | [条件扩散模型：从类别条件到文本到图像](zh/04-conditional-diffusion.md) | [Conditional Diffusion: from Class Labels to Text-to-Image](en/04-conditional-diffusion.md) |
| 5 | [效率优先的 Transformer 扩散主干](zh/05-efficient-backbones.md) | [Efficiency-First Transformer Backbones](en/05-efficient-backbones.md) |
| 6 | [训练与调参实践](zh/06-training-and-tuning.md) | [Training and Tuning in Practice](en/06-training-and-tuning.md) |
| 7 | [扩展到视频、多模态与自回归](zh/07-video-and-multimodal.md) | [Scaling to Video, Multimodal and Autoregressive](en/07-video-and-multimodal.md) |
| 8 | [附录：符号表 / 公式速查 / 术语对照](zh/08-appendix.md) | [Appendix: Notation, Formula Sheet, Glossary](en/08-appendix.md) |

---

## 这份文档讲什么 · What this documentation covers

**技术主线 · The through-line**

```
扩散模型（把生成变成逐步去噪的回归问题）
  → Diffusion Transformer（用通用可扩展主干替换 U-Net）
    → adaLN-Zero（把条件高效注入 Transformer，且不破坏训练稳定性）
      → MMDiT + 整流流（多模态条件 + 更直、更少步的采样路径）
        → 效率优化与训练/调参实践
          → 视频、多模态、可控编辑的扩展
```

**每节固定结构 · Every section follows the same shape**

```
本节回答的问题 / What question this section answers
  机制拆解 + 逐项读公式 / mechanism breakdown + term-by-term formula reading
  对比表 / comparison tables
  工程提示 ／ 常见错误 / engineering notes and common pitfalls
  小结 / summary
```

**三条数字纪律 · Three rules for every number**

1. **能推导的就给推导** — derivations you can re-compute, not just results;
2. **凡具体数值都标口径** — pixel space vs latent space, FLOPs vs parameters, MACs vs FLOPs;
3. **区分"解析推导"与"论文报告值"** — analytic derivations are marked as such and separated from reported results.

---

## 仓库结构 · Repository layout

```
diffusion_models_day_trip/
├── README.md                     # 本文件（语言入口）· this file (language entry)
├── zh/                           # 中文版
│   ├── README.md                 #   中文目录与阅读指南
│   ├── 00-overview.md … 08-appendix.md
│   └── assets/alpha-bar-schedules.svg
└── en/                           # English edition
    ├── README.md                 #   contents & reading guide
    ├── 00-overview.md … 08-appendix.md
    └── assets/alpha-bar-schedules.svg
```

两个语言版本**章节划分、小节编号、公式与代码完全一致**，因此可以逐节对照阅读：
The two editions share **identical chapter structure, section numbering, formulas and code**, so they can be read side by side:

| 中文 | English | 说明 / Note |
|---|---|---|
| `zh/01-diffusion-basics.md#13-…` | `en/01-diffusion-basics.md#13-…` | 小节号一致，锚点可用节号定位 / same section numbers |
| 公式 `$x_t=\sqrt{\bar\alpha_t}x_0+\sqrt{1-\bar\alpha_t}\epsilon$` | 同一公式 / identical | 数学不翻译 / math is not translated |
| Python 代码块 | 同一代码 / identical | 代码与变量名保持不变 / code and identifiers unchanged |

---

## 部署到 Hugo / GitHub

**GitHub**：直接推送即可。根 `README.md` 作为语言入口，`zh/` 与 `en/` 各自有 README 与章末导航。

**Hugo**：整目录放入 `content/docs/`，两种语言可分别作为独立内容目录（也可接 Hugo 的多语言 `content/docs.zh/`、`content/docs.en/` 机制）。注意：

- 加 front matter 后**不要**把正文标题提为 `#`，否则与页面标题重复；
- 公式使用 `$…$` / `$$…$$`，需在主题中启用 MathJax 或 KaTeX（Hugo 常用 `passthrough` 扩展 + math 渲染钩子）；
- `assets/*.svg` 走相对路径引用，Hugo 下建议移到 `static/` 或页面 bundle 并相应调整路径。

各语言版 README 内有更详细的部署说明。
Each edition's README contains the detailed deployment notes.

---

## 引用与致谢 · References

核心文献见附录（中英各一份）：
Key papers are listed in the appendix of each edition:

| 工作 / Work | 论文 / Paper |
|---|---|
| DDPM | [Denoising Diffusion Probabilistic Models](https://arxiv.org/abs/2006.11239) |
| DDIM | [Denoising Diffusion Implicit Models](https://arxiv.org/abs/2010.02502) |
| Score SDE | [Score-Based Generative Modeling through SDEs](https://arxiv.org/abs/2011.13456) |
| CFG | [Classifier-Free Diffusion Guidance](https://arxiv.org/abs/2207.12598) |
| LDM | [High-Resolution Image Synthesis with Latent Diffusion Models](https://arxiv.org/abs/2112.10752) |
| DiT | [Scalable Diffusion Models with Transformers](https://arxiv.org/abs/2212.09748) |
| SD3 / MMDiT | [Scaling Rectified Flow Transformers for High-Resolution Image Synthesis](https://arxiv.org/abs/2403.03206) |
| REPA | [Representation Alignment for Generation](https://arxiv.org/abs/2410.06940) |

---

## 反馈 · Feedback

发现公式错误、口径不一致、译文不准，欢迎提 Issue / PR。文档中每个可核对的数字都标注了推导口径，便于逐项复核。
Found a formula error, a wording issue, or an inaccurate translation? Issues and PRs are welcome. Every number that can be verified carries its derivation basis, so it can be checked term by term.
