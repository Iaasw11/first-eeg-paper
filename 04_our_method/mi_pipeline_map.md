# MI End-to-End Pipeline Map

这是当前项目最重要的学习地图。后续读任何论文，都要把它的改动放回这条链路，而不是只看模型名字。

```text
Dataset / Task Protocol
        ↓
Raw EEG + Event / Label
        ↓
Trial Extraction
        ↓
Train / Validation / Test Split
        ↓
Preprocessing
        ↓
Normalization / Alignment
        ↓
Input Representation
        ↓
Data Augmentation
        ↓
Backbone
        ↓
Feature Enhancement / Fusion
        ↓
Cross-subject / Adaptation Module
        ↓
Loss
        ↓
Classification Head
        ↓
Model Selection
        ↓
Evaluation / Statistics / Efficiency
```

## 0. Dataset / Task Protocol

先回答：
- 什么数据集？
- 做 subject-dependent、cross-session、LOSO、UDA、DG 还是 few-shot？
- 目标被试数据/标签在什么时候可见？

这是后续所有结果解释的前提。

## 1. Raw EEG / Event / Label

输入通常包含：
- 多通道 EEG；
- 采样率；
- event marker；
- class label；
- session / subject ID；
- 可能包含 EOG、artifact 标记。

## 2. Trial Extraction

关键变量：
- cue 相对时间；
- epoch 起止；
- 是否保留 artifact trial；
- baseline interval 是否参与。

不同 trial 窗口会改变最终任务，不能忽略。

## 3. Data Split

必须先 Split，再决定哪些统计量可以计算。

常见：
- 官方 session split；
- within-subject train/test；
- LOSO；
- source-train/source-validation/target-test；
- few-shot target calibration/test。

## 4. Preprocessing

候选组件：
- Band-pass
- Notch
- Filter Bank
- Resampling
- CAR
- Surface Laplacian
- ICA / artifact rejection
- Baseline correction

## 5. Normalization / Alignment

候选组件：
- Z-score
- Min-Max
- Euclidean Alignment (EA)
- Riemannian Alignment
- Whitening

每个组件必须注明：统计量来自 Train、Source、Target-unlabeled 还是整段 Test session。

## 6. Input Representation

常见类别：
- Raw EEG `[B, C, T]`
- Filter-bank multi-band input
- CSP projected signals/features
- Covariance / SPD matrices
- PSD / STFT / Wavelet
- Graph representation
- Topological representation

## 7. Data Augmentation

候选：
- Gaussian noise
- Channel dropout
- Time/Frequency masking
- Mixup / CutMix
- Segment/channel recombination
- GAN / WGAN-GP
- Diffusion

必须记录增强发生在 raw、feature 还是 embedding 层。

## 8. Backbone Families

### CNN
- EEGNet
- ShallowConvNet
- DeepConvNet
- FBCNet
- Multi-scale CNN

### Temporal / Sequence
- TCN
- LSTM / GRU
- Mamba

### Transformer
- EEG Conformer
- EEG-TransNet
- 其他时空/频带 Transformer

### Graph
- GCN
- GAT
- Dynamic Graph

### Geometric
- Riemannian Network
- SPDNet

### Pretrained / Foundation
- MIRepNet
- LaBraM
- CBraMod
- EEGPT

## 9. Feature Enhancement / Fusion

常见可插拔组件：
- Residual
- SE / ECA / CBAM
- Multi-scale branch
- Local-global fusion
- Second-order pooling
- Cross-stitch
- Frequency attention

## 10. Cross-subject / Adaptation

必须与 Task Protocol 匹配。

### Distribution alignment
- MMD
- CORAL
- Wasserstein
- Covariance alignment

### Adversarial
- Domain discriminator / DANN

### Prototype / Metric
- Class prototype
- Triplet
- Center loss

### Contrastive
- SupCon
- Domain contrastive
- Prototype contrastive

### Source handling
- Source selection
- Similarity weighting

### Few-shot
- Fine-tuning
- Meta-learning
- Metric learning

## 11. Loss

- Cross Entropy
- MMD / CORAL / Wasserstein
- SupCon
- Triplet
- Center Loss
- Prototype Loss
- KD Loss
- Reconstruction Loss

Loss 是独立实验组件，不应全部归到 Backbone。

## 12. Classification Head

- Linear
- MLP
- Cosine classifier
- Prototype classifier
- MDM / Riemannian classifier

## 13. Model Selection

优先：
- Source validation / independent validation
- Early stopping / fixed epoch

高风险：
- 每个 epoch 看 target test，然后报告最高 test accuracy。

## 14. Evaluation

### Performance
- Accuracy
- Balanced Accuracy
- Kappa
- F1
- AUC（按任务）

### Stability
- mean ± std
- multiple seeds
- subject-level result
- paired statistical test

### Efficiency
- Params
- FLOPs / MACs
- Latency
- Memory

## 后续读论文时的核心问题

1. 论文到底改了 Pipeline 哪一层？
2. 其他层是否也悄悄改变？
3. 增益可能来自模型，还是来自预处理/划分/目标数据可见性？
4. 该组件是否能从原论文中拆出来单独插拔？
5. 与我们的目标 Task Protocol 是否兼容？
