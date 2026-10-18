# MI 全流程入门综述 #01 — Singh et al. (2021)

> 阅读状态：待精读（已建立阅读地图）；知识级别：L0–L1 零科研基础；目的：理解 MI 系统如何从脑电采集走到分类/反馈。此文不是“2026 年最新 SOTA”榜单。

## 论文信息（已核对）

- **Title**: A Comprehensive Review on Critical Issues and Possible Solutions of Motor Imagery Based Electroencephalography Brain-Computer Interface
- **Authors**: Amardeep Singh, Ali Abdul Hussain, Sunil Lal, Hans W. Guesgen
- **Journal**: Sensors, 2021, 21(6), 2173
- **DOI**: https://doi.org/10.3390/s21062173
- **全文（开放获取）**: https://pmc.ncbi.nlm.nih.gov/articles/PMC8003721/
- **出版社**: https://www.mdpi.com/1424-8220/21/6/2173
- **建议先看**: Figure 2（完整 MI-BCI 系统框图），然后 Section 2

## 先修词典：不需要公式的六个概念

| 词 | 零基础解释 | 易混淆点 |
|---|---|---|
| EEG（脑电图） | 多路电极随时间记录的电位差数据 | 原始 EEG 不是标签 |
| MI（运动想象） | 想象做某个动作，不要求真的动 | 想象动作≠真实运动 |
| BCI（脑机接口） | 将脑信号加工、识别成控制指令的系统 | 算法分类只是系统一部分 |
| Trial（试次） | 实验中一次按指定规则完成的任务 | 试次和采样点是不同单位 |
| Feature（特征） | 有助于区分任务的信号信息/数字表示 | 特征不一定是手工计算的 |
| Classifier（分类器） | 根据特征判断类别或控制指令 | 预测结果≠真实标签 |

## 这篇论文本身的总架构（以 Section 2 和 Figure 2 为准）

论文将 MI-BCI 分为 **calibration phase（校准/学习）**、**translation/online phase（在线转换）**以及 **feedback（反馈）**。Section 2.1–2.8 对应以下系统功能：

| 原文小节 | 论文流程环节 | 初学者先掌握什么 | 今日掌握状态 |
|---|---|---|---|
| 2.1 | Data Acquisition | 电极如何将 EEG 采集、放大、数字化 | [ ] |
| 2.2 | MI Training | 被试如何按照提示学习运动想象/校准系统 | [ ] |
| 2.3 | Pre-processing and Artifacts Removal | 眼动、肌电、工频等干扰如何减小 | [ ] |
| 2.4 | Feature Extraction | 从 EEG 中提取能区分类别的信息 | [ ] |
| 2.5 | Channel Selection | 选哪些电极（非每篇必需） | [ ] |
| 2.6 | Feature Selection / Dimensionality Reduction | 选哪些特征、减少维度（非每篇必需） | [ ] |
| 2.7 | Classification | 根据特征输出类别/控制指令 | [ ] |
| 2.8 | Performance Evaluation | 准确率等评价以及系统效能 | [ ] |

**第一遍阅读目标**：能用自己的话解释每一行“输入 → 操作 → 输出”，而不是背算法或推导公式。

### 特别注意：论文中的两个层次

1. **实际 BCI 系统**：校准学习 → 利用学到的映射做在线预测 → 给被试反馈。这是本综述 Figure 2 的重点。
2. **我们未来的科研评测流程**：数据集 → 训练/验证/测试划分 → 训练 → 模型选择 → 最终评测。这个是为后续实验补充的规范化视角，**不是把综述 Figure 2 原样抄成 train/val/test 图**。

另外，Figure 2 黄框的 channel selection、feature selection、dimensionality reduction 是 **可选** 步骤，不能写成所有模型都必须做。

## 第一课：Figure 2 的白话版

1. 用户按提示想象左手/右手等运动。
2. EEG 电极采集信号；预处理尝试降低干扰。
3. 识别系统寻找 EEG 中与 MI 任务相关的特征。
4. 分类器把特征转化为类别/控制指令。
5. 在校准阶段建立映射；在线阶段使用已学到的映射并将结果反馈给用户。

**举例（教学示例，不是该综述公布的实验结果）**：想象左手 → 采到一段多通道 EEG → 滤波 → 提取特征 → 分类器预测“左手” → 控制一个图标向左移动。

## 建议阅读顺序（20–40 分钟首遍）

1. 读 Abstract + Section 1，只找 BCI / EEG / MI 三个词的含义。
2. 重点看 Figure 2，指出框图中哪部分对应“学习”，哪部分对应“实际使用”。
3. 略读 Section 2.1–2.3，试着回答“信号从哪来？为什么有噪声？”。
4. 略读 Section 2.4 和 2.7，回答“特征和分类结果是什么关系？”。
5. 略读 Section 2.8，不深究全部评价指标。
6. Section 3 暂时只看标题：它讨论仍有哪些应用问题，不需要一次吃透。

## 阅读作业（无需数学基础）

- Q1：EEG、MI、BCI 分别是什么？能否各用一句话解释？
- Q2：人在想象左手时，**模型输入**是什么？**理想输出**是什么？
- Q3：预处理、特征提取和分类器，谁先谁后？每个解决什么问题？
- Q4：这篇综述为什么既有 calibration phase，又有 translation/online phase？
- Q5：Channel Selection 是不是每一个 MI 模型都必须执行？为什么？

## 不懂时的统一提问模板

> 我在 Singh 2021 的第 __ 节看到术语 __。请按“所在流程 → 目的 → 输入 → 输出 → 例子 → 常见误解”解释，尽量不使用未定义的新术语。

## 阅读笔记（由用户逐步填写）

| 流程位置 | 我的白话理解 | 原文提到的方法 | 还没理解的术语 | 需要进一步核对 |
|---|---|---|---|---|
| Acquisition | 待填写 | 待填写 | 待填写 | 待填写 |
| MI Training | 待填写 | 待填写 | 待填写 | 待填写 |
| Preprocessing | 待填写 | 待填写 | 待填写 | 待填写 |
| Feature Extraction | 待填写 | 待填写 | 待填写 | 待填写 |
| Channel Selection | 待填写 | 待填写 | 待填写 | 待填写 |
| Feature Selection | 待填写 | 待填写 | 待填写 | 待填写 |
| Classification | 待填写 | 待填写 | 待填写 | 待填写 |
| Evaluation | 待填写 | 待填写 | 待填写 | 待填写 |

## 本文的适用边界

- 这是一篇 2021 年 **综述**，适合建立 MI-BCI 的传统端到端系统地图；不应用它替代 2025–2026 年最新算法检索。
- 它不是“从 BCIC-IV-2a 原始 GDF 到 PyTorch 训练代码”的逐行实作教程。
- 本文的通用系统流程不等于某个具体深度学习模型的固定流程；深度学习可将表示学习和分类联合优化。
- 本阅读卡把“论文原文涵盖的内容”和“我们用于科研训练的补充规则”有意区分，后续引用时保持此边界。

## 下一篇配套实践

先学 Dataset / Trial / Channel / Time Point / Label / Batch 等零基础概念，再用 BCIC-IV-2a 演示“从连续记录到一个可分类试次”，之后读 EEGNet / SCLDGN 等方法。
