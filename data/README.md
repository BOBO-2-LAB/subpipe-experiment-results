# 实验数据下载

[实验总报告](../README.md) · [逐运行索引](../实验档案索引.md) · [文件清单与 SHA-256](manifest.json)

本目录收录 **4,993 份数据文件**，未压缩文件与压缩文件合计 **87.8 MiB**。其中包括 4,584 份 JSON、350 份原始表格副本、52 份完整逐帧压缩日志、一份逐帧汇总和6份分割预测数组。

|数据|入口|
|---|---|
|历史训练结构与种子|[打开数据](mono/runs_ablation)|
|管道五折均值、标准差和四组对照|[打开数据](mono/runs_review/plain_standard_fivefold_20261031_v1/combined_mean_std.csv)|
|A0、A1-D、A3 逐折数据|[打开数据](mono/runs_review/m13_fivefold_20261030_v1/fold_metrics.csv)|
|A1-S 逐折数据|[打开数据](mono/runs_review/plain_standard_fivefold_20261031_v1/fold_metrics.csv)|
|生物小波消融与推理计时|[打开数据](mono/runs_review/m13_biology_ablation_20261027_v1/evaluation.json)|
|独立与共享编码器指标和预测诊断|[打开数据](mono/runs_review/encoder_sharing_20261117_v1/results.json)|
|独立与共享编码器训练曲线|[打开数据](mono/runs_review/encoder_sharing_20261117_v1/train_log.csv)|
|DeepCamo 补训与保留门槛|[打开数据](mono/runs_fish/deepcamo_20261023_seed42/results.json)|
|Retinex 亮度 MSR 的 SUIM 配对实验|[打开数据](mono/runs_review/retinex_threeway_20261023_suim_only_v2)|
|Haar 与原图图像质量指标|[打开数据](mono/runs_review/wavelet_rgb_review_20261030_v1/per_image_quality.csv)|
|人工评分的匿名逐题数据|[打开数据](mono/runs_review/wavelet_rgb_human_scores_20261031_v1/resolved_scores.csv)|
|最终52回合评分|[打开数据](mono/runs_review/a1_unified_tuning_20261031_v1/course_allocation_v5/final_matrix/metrics.csv)|
|最终52回合完整逐帧日志|[打开数据](mono/runs_review/a1_unified_tuning_20261031_v1/course_allocation_v5/final_matrix/closed_loop)|
|最终逐帧轨迹和计分|[27,980 帧](final_closed_loop_frames.csv)|
|历史双目结果|[打开数据](stereo/runs_stereo)|

## 文件口径

- 训练日志中的每行对应原实验日志中的轮次和组别。原始分割比例通常为0–1，来源中带 `percent` 或 `%` 的字段沿用百分数。
- 同一场景在不同配置及不同版本中可能重复。验收汇总以各自实验的 `task_completed` 字段为准。
- `final_closed_loop_frames.csv` 中的位置单位是米，速度单位是米/秒。`t` 是仿真逻辑时间，`inference_wall_s` 是实际推理墙钟时间。完整嵌套诊断保存在同场景的 `trajectory.json.gz`。
- 五折预测数组 `oof_predictions_*.npz` 的 `masks` 键按共647帧的原缓存索引排序。共享编码器实验的数组按第0折 `test_indices` 排序，共129帧。掩码值0为背景，1为管道。
- 公开副本保留实验数值与失败记录。工作区路径转成相对路径，外部本地路径替换为不透明引用。人工评分保留逐题数值和匿名选择，去掉评分人及自由文本备注。原日志中的非有限值以 JSON `null` 表示。
- 仓库范围为结果数据。原始训练素材、真实视频、模型权重、历史大体积逐帧调试日志和中断轨迹按本地原档留存。

按 `manifest.json` 的 `files` 查找源实验路径、公开文件路径、行数或数组形状及公开副本的哈希。
