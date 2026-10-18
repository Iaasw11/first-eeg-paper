# 零基础论文阅读模板（MI 专用，可复制）

> 规则：第一遍先懂问题、流程、输入输出；不要在未理解变量含义时强行推公式。
>
> 证据纪律：标记 [原文] / [我的理解] / [待核对]，不可将猜测当作作者结论。

## 1. 论文名和来源

- Title：
- Authors / Year / Venue：
- DOI / Official link：
- Paper type：综述 / 实验方法论文 / 数据集论文 / 其他
- 阅读日期：
- 阅读状态：未读 / 第一遍 / 精读 / 已复核

## 2. 一句话回答：这篇论文想解决什么？

- **作者明确写的研究问题 [原文]**：
- **我的大白话翻译 [我的理解]**：
- **什么还不懂 [待核对]**：

## 3. 把论文放进 MI 总流程

| 流程阶段 | 论文在这里做了什么 | 输入 | 输出 | 作者证据（章节/表/图） | 我的疑问 |
|---|---|---|---|---|---|
| Task / Protocol | | | | | |
| Dataset / Acquisition | | | | | |
| Event / Epoch / Split | | | | | |
| Preprocessing | | | | | |
| Normalization / Alignment | | | | | |
| Representation | | | | | |
| Augmentation | | | | | |
| Backbone | | | | | |
| Adaptation / Loss | | | | | |
| Classification Head | | | | | |
| Validation / Test / Metrics | | | | | |

> 注：以上是**项目统一比较坐标系**，不是声称每篇论文都必须有上述全部模块。综述尤其可能不提供单一实验实现。

## 4. 模型分类

- Backbone family：传统机器学习 / CNN / TCN-RNN / Transformer / GCN / Riemannian / Mamba / Foundation / 不适用
- 真正改动的位置：
- 是新增模块、改变数据流、引入新 Loss，还是改变实验协议？

## 5. 任务协议与可见性

- Train Subjects / Sessions：
- Validation 来源：
- Target EEG 训练时是否可见：是 / 否 / 不确定
- Target labels 训练时是否可见：是 / 否 / 不确定
- 目标域完整无标签 session 是否参与预处理：是 / 否 / 不确定
- Test 是否被用于选 epoch：是 / 否 / 不确定
- 是否存在需要进一步核查的泄漏风险：

## 6. 组件拆解卡

- 组件名：
- 流程位置：
- 要解决的小问题：
- 输入形状/数据类型：
- 输出形状/数据类型：
- 是否需要标签：
- 是否需要无标签目标数据：
- 所属协议：SD / Cross-session / DG / UDA / Few-shot / 其他
- 是否可以独立替换：
- 与其他模块的重叠或冲突：
- 代码来源/可复现性：
- 是否值得进入组件池：待用户审阅

## 7. 实验与证据

- Datasets：
- Metrics：
- Strong baselines：
- Ablation：
- Main results（仅记录论文实际报告）：
- 是否有代码/权重：
- 我们是否实际运行过：否 / 是（附实验 ID）
- 证据缺口：

## 8. 阅读输出

- 我用一句话说清楚这篇论文：
- 我真正学会的 3 个概念：
- 我现在解释不清楚的 2 个概念：
- 可能复用的 1 个流程组件：
- 是否加入正式组件库：待用户决定
