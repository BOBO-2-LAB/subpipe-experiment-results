# 管道与 SUIM 实际实验数据

本目录对应原始图像、逐像素标注、实际实验缓存和划分文件。大文件存放在本仓库 GitHub Releases，可以直接下载。

[下载本次全部数据包](https://github.com/BOBO-2-LAB/subpipe-experiment-results/releases/tag/datasets-20261120-v1)

|数据包|实际内容|
|---|---|
|[管道数据](https://github.com/BOBO-2-LAB/subpipe-experiment-results/releases/download/datasets-20261120-v1/subpipe_experiment_dataset.zip)|647 对原图和标注，历史 518/129 划分，原 288×512 缓存，五个连续时间留出块及 2 秒隔离索引。|
|[SUIM 原始数据](https://github.com/BOBO-2-LAB/subpipe-experiment-results/releases/download/datasets-20261120-v1/suim_local_source_dataset.zip)|本地 train_val 的 1,522 对图像与 RGB 标注、1,369/153 实验划分，以及现有 TEST 文件和原 INFO.txt。|
|[SUIM 实验缓存及索引标注](https://github.com/BOBO-2-LAB/subpipe-experiment-results/releases/download/datasets-20261120-v1/suim_experiment_cache_and_labels.zip)|全部训练与验证图像/标签缓存、原版八类索引标注、质检记录及预处理脚本。|

## 使用与校验

解压后的 `file_manifest.json` 记录每个原始文件的路径、字节数和 SHA-256。每个包都已逐文件读取归档内容并与本地源文件校验。仓库中的 [datasets_manifest.json](datasets_manifest.json) 和 [SHA256SUMS.txt](SHA256SUMS.txt) 给出整个 ZIP 的校验值。

管道包中的 `subpipe/train` 和 `subpipe/val` 为原图及 `_label.png` 标注，图像同时有 JPEG 和 PNG 格式。`split.json` 中的本机源目录已替换为可移植路径，其余划分保留。`fivefold_splits.json` 对应论文五折使用的 647 帧及隔离规则。该包仅包含本项目使用的分割子集，不包含完整 SubPipe 的其他传感器序列。

SUIM 原始 RGB 颜色标注与质检后的八类索引分别保存。实验缓存为 384×512 的 uint8 数组，图像为 NHWC、标签为 NHW；验证时中心裁剪到 384×384。类别索引依次为 BW、HD、PF、WR、RO、RI、FV、SR，其中鱼类 FV=6。缓存 `meta.json` 保留准确样本顺序。

SUIM 实验包采用 B0/B1/B2 匹配消融使用的原版缓存和标签，85 张非标准颜色标注按最近标准色处理；未混入后续 37 张裁剪对齐修订。

本地 TEST 只有 108 张图像、110 张顶层 RGB 标注，另有分类别标注，与原 INFO.txt 所述 110 张测试图像不一致。此处完整保留本地可用文件，不补造缺图，不声称为完整官方测试集。该 TEST 未参与本项目已有训练或评分。

## 数据来源

管道图像来自 [SubPipe/SubPipeMini](https://zenodo.org/records/12666132)，原作者项目为 [remaro-network/SubPipe-dataset](https://github.com/remaro-network/SubPipe-dataset)。

生物数据来自 [SUIM 作者实验室](https://irvlab.cs.umn.edu/image-segmentation/suim)，对应 [IROS 2020 论文](https://arxiv.org/abs/2004.01241) 和 [作者代码仓库](https://github.com/IRVLab/SUIM)。

本次发布是实际本地实验输入的副本，保留原数据作者归属及原有使用条款，不对第三方图像或标注另授统一许可证。包内 `SOURCES.txt` 与 SUIM `INFO.txt` 保留来源说明。
