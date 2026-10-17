# Component Library

目标：把论文中的方法拆成**可独立理解、可独立插拔、可验证接口**的最小组件，而不是整篇论文照搬。

## 组件卡片模板

```text
Name:
Category:
Pipeline Position:
Input Shape:
Output Shape:
Needs Label?:
Needs Target Data?:
Needs Target Label?:
Train-only or Train+Inference?:
Main Purpose:
Expected Benefit:
Computation Cost:
Main Hyperparameters:
Compatible With:
Potential Conflict:
Source Paper(s):
Evidence Status:
Our Status: Learning / Reviewed / Adopted / Rejected
```

## 组件分类

### 1. Preprocessing
- Band-pass
- Filter Bank
- Surface Laplacian
- CAR
- ICA
- Resampling

### 2. Normalization / Alignment
- Z-score
- Min-Max
- Euclidean Alignment
- Riemannian Alignment
- Whitening

### 3. Input Representation
- Raw EEG
- CSP
- Filter-bank representation
- SPD / covariance
- PSD / STFT / Wavelet
- Graph
- Topology

### 4. Augmentation
- Gaussian noise
- Channel dropout
- Time/Frequency mask
- Mixup
- CutMix
- Segment recombination
- GAN/WGAN-GP
- Diffusion

### 5. Backbone
- EEGNet
- FBCNet
- Shallow/DeepConvNet
- TCN
- Transformer / Conformer
- GCN / GAT
- Mamba
- Foundation model

### 6. Feature Enhancement
- Residual
- SE
- ECA
- CBAM
- Multi-scale
- Second-order pooling
- Local-global fusion

### 7. Cross-domain / Cross-subject
- MMD
- CORAL
- Wasserstein
- Adversarial discriminator
- Prototype alignment
- Source weighting
- Pseudo-label selection

### 8. Representation Learning Loss
- SupCon
- Triplet
- Center Loss
- Prototype Loss
- KD Loss
- Reconstruction Loss

### 9. Classifier Head
- Linear
- MLP
- Cosine
- Prototype
- MDM

## 兼容性分类

以后每一对组件至少标记为以下一种：

### ✅ 可直接组合
解决不同位置/不同问题，接口天然兼容。

例：
`SincConv → TCN → SupCon`

### ⚠️ 功能部分重叠
可能可以组合，但必须证明不是重复堆叠。

例：
`MMD + CORAL + Wasserstein`

都属于分布对齐，不能因为都能涨点就全部塞进去。

### ❌ 协议冲突
不是代码能不能接的问题，而是实验规则互斥。

例：
- strict DG：训练阶段目标域不可见；
- UDA 模块：训练阶段必须使用目标无标签数据。

### 🔬 需要实验确认
理论上可组合，但张量维度、训练稳定性或信息流可能冲突。

## 最小可行组件的审阅标准

一个组件进入正式组合池前，至少回答：

1. 它解决什么局部问题？
2. 输入/输出接口清楚吗？
3. 是否改变 Task Protocol？
4. 是否额外使用目标数据或标签？
5. 是否能单独打开/关闭做 Ablation？
6. 是否需要大量额外超参数？
7. 计算成本是否可接受？
8. 是否与已有组件功能重复？
9. 至少有一篇论文或可靠实现证明它能工作吗？
10. 我们能否设计机制实验验证“为什么有效”？

## 组合实验原则

不做暴力笛卡尔积。

采用层级筛选：

```text
固定 Dataset + Protocol + Backbone
        ↓
筛 Representation
        ↓
筛 Feature Module
        ↓
筛 Adaptation / Loss
        ↓
检查协同
        ↓
冻结结构
        ↓
最终确认实验
```

探索阶段可以快速试错；最终论文阶段必须冻结规则并公平复现。
