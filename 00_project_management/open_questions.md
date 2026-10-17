# Open Questions

这里专门保存当前仍未解决、但会影响论文方向或实验公平性的问题。

## 当前未解决问题

1. 最终采用哪种 MI Task Protocol？
   - Subject-dependent
   - Cross-session
   - Cross-subject / LOSO
   - UDA
   - DG
   - Few-shot
   - Zero-calibration

2. 是否允许使用目标被试无标签数据进行预处理或对齐？

3. 如果允许，允许一次性使用整个目标 session，还是只能使用已经到达的数据？

4. Baseline 最终采用什么层级？
   - A0：经典可解释模型（如 EEGNet）
   - A1：现代强 Backbone
   - A2：当前具体协议下的最新强 SOTA

5. Euclidean Alignment（EA）应作为固定预处理还是候选组件？

6. 第一阶段 Dataset 是否只使用 BCIC-IV-2a，还是尽早加入 2b / OpenBMI？

7. Component Library 需要细到什么程度？
   - 模块级
   - 算子级
   - Loss 级
   - 数据处理级

8. 最终组合实验是否追求 architecture-agnostic：同一组件在 EEGNet / FBCNet / Conformer / SOTA 上都有效？

9. 如何定义“模块有效”？
   - 单次 Accuracy 提升不够
   - 应考虑多 seed、subject-level consistency、统计显著性、计算开销

10. 什么时候从 exploratory screening 切换到 final confirmatory experiment？
