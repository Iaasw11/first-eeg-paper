# first-eeg-paper

这是我的第一篇 EEG / BCI 论文科研总仓库。

目标不是只保存代码，而是完整记录：**前置知识 → 文献 → Dataset → MI 全流程 → Baseline → 组件库 → 实验 → 结果 → Research Story → 论文写作**。

## 当前目标

- 优先完成一篇真实、规范、可投稿的 EEG / BCI 研究论文。
- 第一篇论文当前优先方向：**Motor Imagery（MI）**。
- 当前不急于锁死最终 Baseline；先建立对 MI End-to-End Pipeline 的完整理解。
- 代码、实验、结果、失败记录和科研决策尽量做到可复现、可追踪。
- 同时保留未来本科毕业论文复用价值，但当前优先级仍是首篇可投稿论文。

## 当前研究策略

```text
理解 MI 全流程
      ↓
按流程拆解近年论文
      ↓
建立 Component Library
      ↓
建立组件兼容性矩阵
      ↓
确定具体 Task Protocol
      ↓
重新选择该协议下的强 Baseline / SOTA
      ↓
A → A+a → A+a+b → 必要时 A+a+b+c
      ↓
严格 Ablation / 多 seed / 多被试 / 多数据集
      ↓
根据稳定实验现象形成可验证的 Research Story
      ↓
论文
```

## 项目原则

1. **先理解 Task Protocol，再比较 Accuracy。**
2. **先理解完整 Pipeline，再决定创新点。**
3. 训练 / 验证 / 测试严格分离，防止 subject leakage 和 test-set overfitting。
4. 模块筛选只根据 Validation 决策；最终 Test 用于确认，不用于反复试错。
5. 不同模型可以有不同最优参数，但必须获得公平的调参预算。
6. 开源 ≠ 可复现；Baseline 必须做代码、数据、协议和结果审计。
7. 允许探索性地先发现有效组合，但最终论文解释必须有额外实验验证，不能事后编造无法验证的故事。
8. 所有重要科研决策记录“为什么”，不仅记录“最后选了什么”。

## 当前阶段

**Phase 3：MI 全流程学习与组件化建模。**

当前优先完成：

- BCIC-IV-2a 从原始数据到最终评价的端到端流程；
- MI 模型分类；
- 近年论文按 Pipeline 位置重新拆解；
- Component Library 与 Compatibility Matrix。

暂存候选：
- `SCLDGN`：跨被试 / DG 候选；
- `MIRepNet`：Few-shot / calibration reduction 候选。

暂不作为第一版直接底座：
- `EEG-DG`；
- `MSD-DDA`。

详见 `00_project_management/decision_log.md` 与 `03_baselines/candidate_audit.md`。

## 目录

- `00_project_management/`：Roadmap、进度、决策日志、未解决问题、科研词典、知识管理规则
- `01_literature/`：文献矩阵、核心论文、阅读笔记
- `02_dataset/`：Dataset 说明、下载方式、事件/Trial、预处理与划分记录
- `03_baselines/`：Baseline 候选、代码审计、复现结果
- `04_our_method/`：MI Pipeline Map、Component Library、后续方法设计
- `05_experiments/`：实验配置、日志、实验登记、失败实验
- `06_results/`：结果表、统计分析
- `07_figures/`：论文图表与生成脚本
- `08_paper/`：论文大纲、草稿、修改记录
- `09_thesis_reuse/`：未来本科毕业论文可复用内容与系统扩展设想

## 建议阅读顺序

第一次进入仓库时：

1. `00_project_management/research_progress.md`
2. `00_project_management/roadmap.md`
3. `00_project_management/research_glossary.md`
4. `04_our_method/mi_pipeline_map.md`
5. `04_our_method/component_library.md`
6. `00_project_management/decision_log.md`
7. `03_baselines/candidate_audit.md`

## GitHub 知识沉淀规则

以后出现“输出论文必须掌握的前置知识”时，不直接无限堆文档：

1. ChatGPT 提醒该知识建议入库；
2. 我人工审阅是否值得保存；
3. 同意后归类到对应文件；
4. 后续理解更新时修改原文，避免重复和知识垃圾。

详细规则见 `00_project_management/knowledge_management_rules.md`。
