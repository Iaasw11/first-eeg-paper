# Dataset Layer

本目录记录每个 MI 数据集从“原始文件”到“可用于实验的 trial”的完整过程。

## 每个数据集必须记录的字段

- Dataset 名称
- Subjects
- Sessions
- Classes
- Channels
- Sampling rate
- Trials per class / subject
- 原始文件格式
- Event / label 编码
- Trial 时间窗
- 官方 train/test 划分
- 常见论文划分
- 预处理差异
- 是否包含 EOG / artifact 标记
- License / 下载方式
- 可能的数据泄漏点

## 第一优先级

1. BCIC-IV-2a
2. BCIC-IV-2b
3. OpenBMI

当前先从 **BCIC-IV-2a** 做完整端到端学习，再横向比较其他数据集。

## 为什么 Dataset 要单独学习

不同论文即使使用相同模型，只要：
- trial 时间窗不同；
- session 选择不同；
- artifact trial 处理不同；
- train/test protocol 不同；

最终 Accuracy 就可能无法公平比较。

因此后续所有模型实验必须先锁定 Dataset + Task Protocol。
