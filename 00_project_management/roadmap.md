# Roadmap

## 总目标

完成第一篇真实、规范、可投稿的 EEG / BCI 论文，并在过程中建立能够复用到后续科研的 MI 方法论、代码和知识体系。

## Phase 0 — 方向选择 ✅

- 比较 MI、癫痫预测、精神疲劳/警觉度
- 选择 MI 作为首篇论文训练场

## Phase 1 — 文献地图 ✅ / 持续更新

- 近两年高水平 MI 论文扫描
- 记录 Dataset、Split、Preprocessing、Input、Backbone、Loss、Augmentation、Metric、Ablation、Gap
- 识别主要研究线：跨被试、跨会话、少校准、轻量化、数据增强、Riemannian、预训练等

## Phase 2 — Baseline 审计 ✅ / 暂停定型

已审计代表候选：
- EEG-DG
- SCLDGN
- MSD-DDA
- MIRepNet

结论：仅“顶刊 + GitHub”不足以确定 Baseline，需要先理解完整 Pipeline 与 Task Protocol。

## Phase 3 — MI 全流程学习 ← 当前阶段

从 BCIC-IV-2a 开始，掌握：

Raw EEG → Event → Trial → Split → Preprocessing → Alignment → Representation → Augmentation → Backbone → Adaptation/Loss → Head → Model Selection → Metric

要求：不仅知道“怎么做”，还要知道：
- 为什么需要这一步；
- 输入是什么；
- 输出是什么；
- 有哪些替代方案；
- 哪些方案使用了目标数据/标签；
- 哪些组合可能冲突。

## Phase 4 — Component Library

对近年论文做“横向拆解”，而非整篇照搬。

构建：
- Preprocessing components
- Alignment components
- Input representations
- Augmentation components
- Backbone families
- Feature enhancement modules
- Cross-subject/adaptation modules
- Loss functions
- Heads
- Evaluation protocols

每个组件记录接口与协议依赖。

## Phase 5 — Compatibility Matrix

把组件分成：
- 可直接组合
- 功能重叠
- 协议互斥
- 需要额外目标数据
- 需要目标标签

## Phase 6 — 确定具体 Task Protocol

先明确实验规则，再找 SOTA。

例如：
- Strict LOSO / DG
- Offline cross-subject with unlabeled target statistics
- UDA
- Few-shot calibration
- Cross-session

## Phase 7 — 重新选择 Baseline / SOTA

建立三级 Baseline：
- A0：经典、简单、方便插模块
- A1：现代强 Backbone
- A2：当前 Task Protocol 下最新强 SOTA

## Phase 8 — Exploratory Module Screening

固定训练/验证/测试规则，仅在 Validation 上快速筛：

A → A+a_i → A+a+b_j → 必要时 A+a+b+c

失败模块也登记，不只保留成功结果。

## Phase 9 — Confirmatory Experiments

冻结结构后：
- 多随机种子
- 多被试
- 多数据集
- 公平调参预算
- Ablation
- Sensitivity
- Efficiency
- Statistical testing

## Phase 10 — Research Story

顺序：

发现稳定现象 → 提出机制解释 → 设计额外实验验证解释 → 形成 Research Problem / Gap / Contribution

不是为了涨点事后编造无法验证的故事。

## Phase 11 — Writing & Submission

完成：
- Introduction
- Related Work
- Method
- Experiments
- Results
- Discussion / Limitation
- Figures / Tables
- Reproducibility materials
