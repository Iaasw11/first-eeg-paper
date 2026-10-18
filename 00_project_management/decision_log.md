# Decision Log

用于记录重要科研决策及其原因，避免以后重复踩坑或忘记为什么改变路线。

## D001 — 第一篇论文优先选择 MI

**Status:** Adopted

### 决策
第一篇论文优先做 Motor Imagery（MI），而不是癫痫预测或 Future Vigilance Forecasting。

### 原因
- MI 的公开 Dataset 更成熟；
- Baseline 和评价协议更成熟；
- 更适合第一次完整跑通科研流程；
- 癫痫预测的临床协议、泄漏风险和事件级评价更复杂；
- Future Vigilance Forecasting 长期价值较高，但 Benchmark 和任务协议尚不够统一。

---

## D002 — 暂停“先定 Baseline 再找模块”的路线

**Status:** Adopted

### 原路线
先选一个 Baseline A，再不断尝试 a / b / c 模块。

### 调整原因
当前对 MI 全流程理解仍不足，直接魔改模型容易出现：
- 不清楚模块处于 Pipeline 哪一层；
- 不清楚不同 Task Protocol 下模块是否合法；
- 把预处理、目标域可见性、Backbone 和 Loss 混在一起；
- 即使涨点也无法解释为什么。

### 新路线
MI 全流程学习 → 论文流程拆解 → 组件库 → 兼容性矩阵 → 确定具体任务协议 → 再选最新强 Baseline / SOTA → 组合实验。

---

## D003 — EEG-DG 暂不作为第一版直接 Baseline

**Status:** Rejected for initial baseline

### 原因
静态代码审计发现：
- 公开入口有缺失模块与接口不一致；
- 条件分布损失实现存在梯度路径断开风险；
- 公开入口主要对应跨会话，而非目标跨被试协议；
- 使用目标测试集最高结果进行选择；
- 原始数据到输入特征的完整预处理链未闭合。

注意：以上针对当前公开仓库，不等于断言作者原始实验代码存在相同问题。

---

## D004 — SCLDGN 暂存为跨被试候选，不再立即定为最终 Baseline

**Status:** Candidate

### 优点
- 跨被试入口较完整；
- 源域有验证集；
- 模型选择流程比部分候选更规范；
- 核心代码相对完整。

### 风险
- 默认 Euclidean Alignment 依赖整批无标签目标会话统计量；
- 这更接近 offline / transductive setting，而不是“第一条数据就预测”的严格在线零校准；
- 仍需真实训练验证。

### 当前处理
保留为候选，等 Task Protocol 和组件库确定后重新评估。

---

## D005 — MIRepNet 保留为 Few-shot / Calibration Reduction 路线候选

**Status:** Candidate

### 优点
- 官方代码、预训练权重、许可较完整；
- 面向少量目标被试标注数据的快速适配；
- 适合研究 calibration reduction。

### 限制
- 与严格 target-free cross-subject 不是同一个任务协议；
- 当前更适合 few-shot supervised calibration；
- 完整预训练复现材料仍需继续核对。


---

## D006 — 阶段三改为“科研理解与实验审核”，不以编程能力为门槛

**Status:** Adopted（用户于 2026-10-18 同意）

### 决策

- 阶段三采用 25 课完整 MI Pipeline 学习框架，六个单元，具体见 [MI_Learning_Curriculum.md](MI_Learning_Curriculum.md)。
- 用户要理解任务协议、模块科学作用、实验的合法性、公平比较和论文证据，不要求独立编写 PyTorch。
- AI 主要负责代码实现、审计、实验脚本和自动化；是否真实复现必须基于实际运行日志和输出。
- 第 5–7 课已讲但用户难以回忆：标为待复习并重测；第 8 课 EEGNet 未验收；不以一次答题替代“掌握”。
- 后续阶段编号以用户定义的 0–10 为准：阶段 4 是 50 篇论文流程重构，阶段 5 才是组件库，阶段 6 是兼容矩阵，阶段 7 重新选 Baseline/SOTA。

### 原因

第一篇论文的关键产出是可验证的科学问题、合理的实验和可信的证据；代码是实施手段。把代码语法学习作为用户强制门槛既延迟进度，也不能代替科学审核能力。
