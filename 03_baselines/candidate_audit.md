# Baseline Candidate Audit

> 这里记录“高水平论文 + 开源实现”的可复现性审计。开源只代表有公开代码，不代表能直接复现。

## 当前候选概览

| Method | Primary task | Code status | Current decision |
|---|---|---|---|
| EEG-DG | Multi-source domain generalization | 公开代码存在缺失/接口/损失问题 | 暂不作为第一版 Baseline |
| SCLDGN | Cross-subject domain generalization | 核心训练链相对完整 | 保留为跨被试候选 |
| MSD-DDA | Multi-source unsupervised domain adaptation | 存在缺失对象、损失返回异常、输入流程缺口 | 暂缓 |
| MIRepNet | Few-shot / calibration reduction | 代码与预训练权重较完整 | 保留为 few-shot 候选 |

## EEG-DG

### 优点
- 高水平期刊；
- 作者公开仓库；
- 方法本身值得研究。

### 当前公开实现风险
- 入口依赖缺失文件；
- 网络接口与入口源域数量不一致；
- 条件分布损失的公开实现存在梯度路径断开风险；
- 公开入口主要执行跨会话实验；
- 数据预处理链未完整公开；
- 使用目标测试集最高结果进行报告。

**结论：** 方法可研究，当前仓库不适合作为“下载后直接跑”的第一版 Baseline。

## SCLDGN

### 优点
- 核心训练、数据、损失、采样与保存材料较完整；
- 公开入口确实留出目标被试；
- 源域内建立 Validation；
- 模型选择后再测试目标被试，实验结构相对清楚。

### 主要协议边界
默认 Euclidean Alignment 会使用整批目标无标签会话统计量。

因此必须区分：
- offline / transductive cross-subject；
- strict target-free DG；
- online / causal zero-calibration。

**结论：** 当前较值得继续，但等 Task Protocol 确定后再决定是否正式采用。

## MSD-DDA

### 当前公开实现风险
- 模型构造引用未定义对象；
- 训练入口调用缺失工具函数；
- 局部判别损失计算后未按命名进入返回值，实际训练项与变量名不一致；
- 原始 EEG → 50 维输入特征的完整过程缺失；
- 周期性读取目标测试标签并选择最高准确率。

**结论：** 暂不作为第一版底座。

## MIRepNet

### 优点
- 官方代码；
- 预训练权重；
- MIT License；
- 提供 fine-tuning 入口；
- 适合研究少样本 calibration reduction。

### 协议边界
- 使用目标被试少量标签进行微调；
- 与 strict target-free cross-subject 不是同一个任务；
- 默认流程仍需进一步核对评估集对齐统计量的使用方式；
- 完整预训练复现材料不等于微调材料。

**结论：** 如果最终任务是 few-shot personalization，优先级会明显上升。

## 以后审计 Baseline 必查

1. 论文与仓库是否一一对应；
2. Commit / release 固定；
3. License；
4. Environment 是否锁定；
5. 原始 Dataset 到模型输入是否完整；
6. Train / Validation / Test 是否清楚；
7. 是否使用目标域数据或标签；
8. Test 是否被用于模型选择；
9. Loss 是否真的产生梯度；
10. 论文结果是否可以在真实数据上复现。
