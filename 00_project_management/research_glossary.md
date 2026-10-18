# Research Glossary

这是第一篇 EEG / BCI 论文必须掌握的科研词典。优先记录会直接影响实验公平性、Baseline 选择和论文写作的概念。

## Baseline

**直观解释：** 用来证明“我们的改动到底有没有价值”的参照方法。

Baseline 可以分层：
- `A0`：经典、简单、稳定，例如 EEGNet / CSP-LDA；
- `A1`：现代强 Backbone，例如 FBCNet / Conformer；
- `A2`：当前具体任务协议下最新强方法 / SOTA。

**常见误区：**
- Baseline 不等于“随便找一个弱模型”。
- 不能故意不给 Baseline 调参，而给自己的模型精调。

---

## SOTA — State of the Art

**直观解释：** 某个明确任务协议和评估条件下，当前公开结果中最强或最有竞争力的方法。

**关键点：**
不存在“整个 MI 领域唯一 SOTA”。

例如：
- BCIC-IV-2a subject-dependent SOTA
- BCIC-IV-2a LOSO SOTA
- UDA SOTA
- Few-shot SOTA

它们不能直接混为一谈。

---

## Task Protocol — 任务协议

**直观解释：** 一项实验的“规则书”。它规定模型训练和测试时到底允许看什么数据。

核心问题：
- 谁用于训练？
- 谁是目标被试？
- 目标被试 EEG 能不能在训练/预处理阶段看到？
- 目标标签能不能看到？
- Validation 从哪里来？
- Test 什么时候第一次被使用？

### 常见协议

#### Subject-dependent
同一个人的部分数据训练，剩余数据测试。

#### Cross-session
例如 Session 1 训练，同一人的 Session 2 测试。

#### Cross-subject / LOSO
其他被试训练，完整留出一个新被试测试。

#### UDA — Unsupervised Domain Adaptation
源域有标签，训练阶段允许看到目标域无标签数据。

#### DG — Domain Generalization
训练阶段完全看不到目标域，测试时才出现新被试。

#### Few-shot
允许目标被试提供少量有标签样本做适配。

#### Zero-calibration
不使用目标被试任务标签进行校准。注意仍要继续说明是否允许使用无标签目标数据或静息态数据。

---

## LOSO — Leave-One-Subject-Out

有 N 名被试时，每次留出 1 名作为目标测试被试，其余 N-1 名用于训练/验证，轮流执行 N 次。

LOSO 是跨被试评价的一种常见方式，但仍需继续说明：
- 是否使用目标无标签数据；
- 是否对目标整段 session 做 EA 等统计对齐；
- 模型选择是否只基于源域验证集。

---

## Train / Validation / Test

### Train
用于更新模型参数。

### Validation
用于选择超参数、模块、epoch、checkpoint。

### Test
用于最终一次性评价泛化能力。

**核心原则：** 如果不断根据 Test 结果换模型、换模块、选 epoch，那么 Test 已经变成了 Validation。

---

## Data Leakage — 数据泄漏

训练流程利用了理论上测试时不应获得的信息，从而让结果虚高。

MI 常见风险：
- 同一 trial 或高度重叠窗口同时出现在 train/test；
- 使用整个数据集计算 normalization，再切 train/test；
- 使用目标测试标签选择最佳 epoch；
- Subject leakage：同一个人的样本随机分到 train/test，却声称做跨被试泛化。

**注意：** 使用目标无标签统计量不一定是“泄漏”，但必须符合任务协议并明确披露。例如整批目标 session EA 属于 transductive/offline 信息利用，而不是严格 target-free DG。

---

## Ablation Study — 消融实验

用于回答：最终模型中的每一个组件到底有没有贡献。

理想形式：

| Model | a | b | c |
|---|---|---|---|
| Baseline A | × | × | × |
| A+a | ✓ | × | × |
| A+b | × | ✓ | × |
| A+a+b | ✓ | ✓ | × |
| A+a+b+c | ✓ | ✓ | ✓ |

除了 Accuracy，还应观察：
- 多被试一致性；
- 多 seed 稳定性；
- 参数量 / MACs / latency；
- 与假设对应的机制指标。

---

## Exploratory vs Confirmatory Experiment

### Exploratory
用于找有希望的模块组合，可以快速试错，但只能在 Train/Validation 上决策。

### Confirmatory
结构冻结后，用独立 Test、多随机种子、多数据集验证结论。

这一区分允许“先通过实验发现有效模块”，同时避免最终结论被反复试错污染。

---

## Research Gap

不是“别人没用过我的模块”。

更合理的定义：已有方法在某个明确、可验证条件下仍存在稳定不足，而这个不足值得解决。

首篇论文优先寻找：
**成熟 Benchmark + 小而真实的问题 + 可验证的机制改进。**

---

## Backbone

模型中承担主要特征提取/表示学习的骨干网络。例如：
- CNN：EEGNet、FBCNet、ShallowConvNet
- Transformer：EEG Conformer
- Graph：GCN/GAT
- Sequence：TCN/Mamba

Backbone 与 Alignment、Augmentation、Loss、Domain Adaptation 模块应尽量分开描述。
