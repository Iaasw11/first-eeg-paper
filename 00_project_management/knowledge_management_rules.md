# Knowledge Management Rules

这个仓库不仅保存代码，也保存第一篇 EEG / BCI 论文从“不会”到“完成投稿”过程中必须掌握的知识、决策、实验和失败经验。

## 1. 什么内容应该进入仓库

分为三类：

### A. 必须掌握的前置知识
例如：
- Baseline / SOTA
- Task Protocol（任务协议）
- Train / Validation / Test
- Subject-dependent / Cross-session / Cross-subject
- LOSO / UDA / DG / Few-shot / Zero-calibration
- Data leakage / Subject leakage
- Ablation study
- Accuracy / Kappa / F1 / Balanced Accuracy

这类知识应长期保留，要求做到“以后看到论文时能自己识别”。

### B. 对当前论文直接有用的领域知识
例如：
- BCIC-IV-2a/2b/OpenBMI 的数据结构
- EEG 预处理、EA、CSP、Riemannian、Filter Bank
- CNN / TCN / Transformer / GCN / Mamba 等模型类别
- Domain Adaptation / Contrastive / Prototype 等跨被试组件

这类内容主要进入 MI Pipeline 和 Component Library。

### C. 项目过程信息
例如：
- 为什么选择 MI 而不是癫痫预测 / 疲劳预测作为首篇论文
- 为什么暂停某个 Baseline
- 当前阶段、下一步、未解决问题
- 哪些想法被否决以及原因

必须记录“为什么”，不能只记录最终答案。

## 2. 什么内容暂时不进入仓库

- 尚未核实的论文数字
- 只出现一次、与当前项目无关的超参数
- 无法确认来源的 SOTA 声称
- 纯聊天式猜测

## 3. 知识状态

建议对重要条目标记：
- `Learning`：刚接触，还不能独立解释
- `Reviewed`：已经人工审阅，理解基本正确
- `Adopted`：已经进入实验或论文方案
- `Rejected`：曾考虑但已明确不用，并记录原因

## 4. 入库流程

后续当出现“论文产出必须掌握的前置知识”时：
1. ChatGPT 先提示这是建议入库内容；
2. 用户审阅是否值得保存；
3. 用户同意后，再整理为长期文档；
4. 若后续理解变化，更新原文，不堆重复文件。

## 5. 证据原则

- 文献中的事实必须区分“论文明确报告”和“我们的推断”。
- 复现结论必须区分“静态代码审计”和“真实运行验证”。
- 开源 ≠ 可复现；不开源 ≠ 一定有问题。
- 任何最终论文结果必须来自公平、可追踪的实验协议。

## 6. 阶段三教学与人机分工（2026-10-18 用户同意）

- **用户学习目标是科学理解、方法审阅、实验设计与证据判断，不是独立写 PyTorch 或重做代码工程。**
- AI 主要承担文献辅助、实现/审计代码、组织数据、构建可复现实验、脚本自动化、辅助统计与图表、起草文稿；真实运行依赖可用环境/算力，绝不能将未执行的程序或推测结果写成已复现。
- 第 5–7 课虽然讲过，用户明确表示回忆不牢；统一标记 **Revisit**，不得虚报“完全掌握”。第 8 课为已讲未验收。
- 学习进度区分 `Introduced`（已讲）、`Revisit`（需复习）、`Quiz-passed`（单题答对）、`Reviewed`（通过新的综合案例验收）。
- 课程计划和项目状态可以在用户批准后统一纳入项目管理文档；具体技术知识卡仍须逐项提示价值，用户批准后再入库。
- 课程计划：[MI_Learning_Curriculum.md](MI_Learning_Curriculum.md)。
