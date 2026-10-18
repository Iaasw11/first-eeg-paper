# first-eeg-paper

这是我的第一篇 EEG / BCI 论文科研总仓库。

仓库不仅保存代码，还长期记录：**前置知识 → 文献 → Dataset → MI 全流程 → Baseline → 组件库 → 实验 → 结果 → Research Story → 论文写作**。

## 当前目标

- 优先完成一篇真实、规范、可投稿的 EEG / BCI 研究论文，当前首篇优先方向：**Motor Imagery（MI）**。
- 不急于锁死最终 Baseline；先建立 MI End-to-End Pipeline 的完整理解，再按协议选择强 Baseline / SOTA。
- 代码、实验配置、随机种子、日志、失败结果、科研决策与写作材料尽量可复现、可追踪。
- 同时保留对未来本科毕业论文和后续学术发展的复用价值，但当前优先级是首篇可投稿论文。

## 当前阶段

**阶段 3：MI 全流程学习**（规划 25 课；第 5–7 课需要复习，第 8 课 EEGNet 已讲第一遍但尚未验收）。

- [阶段三 25 课课程表与真实学习进度](00_project_management/MI_Learning_Curriculum.md)
- [研究项目阶段、下一步与当前证据](00_project_management/research_progress.md)
- [项目总路线（阶段 0–10）](00_project_management/roadmap.md)

**人机分工：**用户负责研究问题、任务协议、算法模块的科学作用、实验设计和结论审核；AI 主要负责代码实现、数据处理、静态审计及可用环境下的实验自动化。**不要求用户独立编写 PyTorch。** 代码写好不等于实验已运行，必须保留实际训练和评价证据。

## 零基础学习入口

从 [零基础前置知识](00_project_management/beginner_prerequisites.md) 和 [阶段三课程表](00_project_management/MI_Learning_Curriculum.md) 开始，遵循：

```text
零基础层 → MI 数据与信号层 → 算法与协议层 → 论文研究层
```

**先搞懂数据，再理解训练与评价，再理解模型及方法模块。**学习进度分为已接触、需要复习、随堂题通过和情景验收；听过不等于真正掌握。

已有辅助学习图：
- [EEG 数据层级图](00_project_management/assets/eeg_data_hierarchy.svg)
- [修正版 MI-EEG 数据处理流程图](00_project_management/assets/mi_eeg_pipeline_corrected.svg)

## 当前研究路线（阶段 0–10）

```text
阶段 0–2  方向选择 → MI 文献初筛 → Baseline 初步审计（已进行）
    ↓
阶段 3    MI 全流程理解与能力验收（当前）
    ↓
阶段 4    近年约 50 篇 MI 论文按 Pipeline 逐篇重构
    ↓
阶段 5    建立 Component Library
    ↓
阶段 6    建立组件兼容矩阵
    ↓
阶段 7    固定具体 Task Protocol，重新选择强 Baseline / SOTA
    ↓
阶段 8    仅在合法的 Validation 上筛选单模块
    ↓
阶段 9    A → A+a → A+b → A+a+b，消融、多 seed、多被试、多数据集
    ↓
阶段 10   根据可信实验现象形成论文、审核与投稿
```

任务协议从阶段三开始学习，在论文重构和组件分析中逐步明确，正式比较 Baseline 前必须固定。

## 项目原则

1. **先理解 Task Protocol，再比较 Accuracy。**
2. **先理解完整 Pipeline，再决定创新点。**
3. Train / Validation / Test 严格区分，防止 subject leakage 和测试集选优；Validation 用于模型选择，最终 Test 用于独立评价。
4. 模块比较可以单独调参，但须有透明且公平的调参预算；记录配置、随机种子、指标、日志与失败结果。
5. 开源不等于可复现；论文结果、静态代码审计和真正运行验证必须区分。
6. 创赛材料中的技术设想或数字不能直接当成科研证据；论文结论必须由可信实验支持。
7. 可从探索性实验发现现象，但解释需要额外实验核查，不能为涨点编造研究故事。
8. 重要科研决策记录“为什么”，不只保存最终结论。

## 当前候选 Baseline 审计

- `SCLDGN`：跨被试 / DG 候选，须明确默认 EA 可能使用整批目标会话无标签统计量；
- `MIRepNet`：Few-shot / calibration reduction 候选，不能与严格 target-free setting 混为一谈；
- `EEG-DG`、`MSD-DDA`：当前公开实现不适合未经修复直接作为首版底座。

详见 [决策日志](00_project_management/decision_log.md) 和 [候选 Baseline 审计](03_baselines/candidate_audit.md)。

## 目录

- `00_project_management/`：研究进度、课程、决策日志、前置知识、术语和学习流程图
- `01_literature/`：文献矩阵、核心论文、阅读笔记
- `02_dataset/`：数据集、事件/Trial、预处理、数据划分与记录（不提交大体积原始 EEG）
- `03_baselines/`：Baseline 候选、代码审计、复现记录
- `04_our_method/`：MI Pipeline Map、Component Library、后续方法设计
- `05_experiments/`：实验配置、日志、登记和失败实验
- `06_results/`：结果表、统计分析
- `07_figures/`：论文图表与生成脚本
- `08_paper/`：论文大纲、草稿、修改记录
- `09_thesis_reuse/`：本科毕业论文可复用内容

## 建议阅读顺序

1. [阶段三课程表](00_project_management/MI_Learning_Curriculum.md)
2. [零基础前置知识](00_project_management/beginner_prerequisites.md)
3. [研究进度](00_project_management/research_progress.md)
4. [阶段路线](00_project_management/roadmap.md)
5. [研究术语](00_project_management/research_glossary.md)
6. [MI 全流程地图](04_our_method/mi_pipeline_map.md)
7. [组件库框架](04_our_method/component_library.md)
8. [研究决策日志](00_project_management/decision_log.md)
9. [Baseline 审计](03_baselines/candidate_audit.md)

## GitHub 知识沉淀规则

遇到论文必需的前置知识时，**AI 先提出入库建议 → 用户审阅并同意 → 更新对应文件**。不要因课堂出现某个术语就无提示地新增知识文档；理解更新时优先修改原文，不制造重复或未经核查的结论。

详见 [知识管理规则](00_project_management/knowledge_management_rules.md)。
