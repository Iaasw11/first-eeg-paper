# Research Progress

## 当前阶段

**Phase 3：MI 全流程学习与组件化建模。**

当前目标不是立刻追求 SOTA，也不是马上确定最终 Baseline，而是先建立从原始 EEG 到最终评价指标的完整 MI 心智模型，再把近年论文拆成可复用组件。

## 已完成

- [x] 比较 MI、癫痫预测、疲劳/警觉度预测三条路线
- [x] 确定 MI 更适合作为第一篇论文的训练场：Benchmark、Dataset、Baseline、Metric 更成熟
- [x] 初步检索约 50 篇近两年 MI 高水平期刊论文
- [x] 提取研究问题、Dataset、Split、Preprocessing、Input、Backbone、Loss、Augmentation、Metric、Ablation、Research Gap 等字段
- [x] 初筛 EEG-DG、SCLDGN、MSD-DDA、MIRepNet 等开源候选
- [x] 完成上述候选的第一轮代码审计
- [x] 发现“先定 Baseline 再盲拆模块”对当前阶段过早
- [x] 调整策略为“先学全流程 → 再做组件库 → 最后重新选 Baseline/SOTA”

## 当前进行

- [x] 为 MI 零基础全流程阅读选定首篇开放获取综述（Singh et al., 2021）并创建阅读卡与笔记模板
- [ ] 读懂该综述 Figure 2（校准 → 在线转换 → 反馈）并回答入门问题
- [ ] 建立 MI End-to-End Pipeline Map
- [ ] 从 BCIC-IV-2a 开始理解原始数据、事件、trial、预处理、划分、输入表示、模型、评价
- [ ] 按流程位置重构近年论文，而不是按论文标题堆列表
- [ ] 建立模型分类体系：CNN / TCN-RNN / Transformer / GCN / Riemannian / Mamba / Foundation
- [ ] 建立 Component Library
- [ ] 建立组件兼容性矩阵

## 下一阶段

- [ ] 明确具体 Task Protocol
- [ ] 为该协议重新检索最新强 Baseline / SOTA
- [ ] 建立三级 Baseline：经典 A0、现代强 Backbone A1、协议下强 SOTA A2
- [ ] 在 Validation 上做模块筛选
- [ ] 形成 A → A+a → A+a+b → A+a+b+c 的增量实验
- [ ] 多随机种子、多被试、多数据集验证
- [ ] Ablation / Sensitivity / Efficiency / Statistical test
- [ ] 根据实验现象形成可验证的 Research Story
- [ ] 完成论文写作与投稿

## 当前最重要的原则

1. 先理解任务协议，再比较 Accuracy。
2. 先理解完整 Pipeline，再决定模型创新点。
3. 模块筛选只看 Validation，不反复偷看最终 Test。
4. 不同模型可以有不同最优超参数，但必须获得公平的调参预算。
5. 先发现有效现象，再提出解释，再用额外实验验证解释；不能为了涨点倒推虚假故事。
