# Member 4 SVM — 修订版 Notebook

成员：Yao Haotian（G2603151K），MH6805 Group 30。

主文件：`Member4_SVM_Analysis_G2603151K_Revised.ipynb`。
全部分析代码都在 Notebook 内，不需要导入其他 `.py` 文件，也不需要运行额外测试脚本。

## 运行

1. 解压完整包，保持 Notebook 和 `data/` 的相对位置。若只下载 Notebook，请把标准 CSV 文件放入同目录下的 `data/` 或 `ML_data/`，也可以直接放在 Notebook 旁边：
   - `online_shoppers_train_fixed.csv`
   - `online_shoppers_test_fixed.csv`
2. 在所用 Jupyter kernel 的环境中安装依赖。已有环境可以先直接运行；缺少依赖时可在终端执行 `python -m pip install -r requirements.txt`。请确认该 Python 环境就是 Notebook 的 kernel。
3. 打开 Notebook，选择 **Kernel → Restart Kernel and Run All Cells**。
4. 检查最后一个代码单元输出 `Run complete`。结果写入 `results/member4_svm/<本次运行编号>/`，多次运行各自保留。

运行包含完整网格搜索、OOF 预测、校准，以及两组月份对照，耗时取决于 CPU 和内存。默认最多同时运行四个拟合任务，使用线程并行以避免 Windows 下子进程临时文件清理问题；内存不足时把 `N_JOBS` 改为 1。不要为了加速改变搜索范围或交叉验证设置，否则会形成不同实验。

**版本说明：**附带已执行结果使用 Python 3.13.15、scikit-learn 1.6.1；完整数值依赖版本见 `requirements-tested.txt` 和每次运行生成的 `environment.json`。1.6.1 是这次复现验证所用的版本，不是代码强制要求的唯一版本。`requirements.txt` 不固定为 1.6.1。使用其他版本时应重新 Run All 并核对实际结果；复现附带数值优先使用已验证版本。

## 对应 PDF 的六项修改

| PDF 项目 | Notebook 位置 | 实现 |
|---|---|---|
| 01 标准路径及数据校验 | 第 1 节 | 标准文件名；项目相对路径搜索；行数、正类数、列顺序、缺失值、重复及交叉重叠检查；SHA-256 比较 |
| 02 AP 命名 | 全文及导出文件 | `average_precision` 统一称 AP；保留原计算及 CV SD 定义 |
| 03 Training OOF margin 阈值 | 第 3、6 节 | 训练 OOF max F1；确定性并列规则；固定 test 只评价；默认阈值表单独保留 |
| 04 校准输出分离 | 第 4、7 节 | 保留 sigmoid、五折和原 ensemble 行为；原始 margin/校准概率逐行保存；两种 AP 分列 |
| 05 排除 Month 对照 | 第 5 节 | 原含 Month 实验保留为 `temporal_results`；新增 `month_excluded_results`；均只按 earlier-month CV 选参数/核 |
| 06 完整运行及归档 | 第 8–10 节及随附结果 | 表格、图、数据哈希、折分配、环境、完成状态、文件清单及计算结论自动保存 |

## 阅读结果时区分四个概念

- **主实验排序指标：**原始 SVM margin 的 AP 和 ROC-AUC。
- **原分类结果：**默认 margin=0，对应 `svm_default_margin_test_results.csv`。
- **新增分类结果：**训练 OOF 选出的 margin 阈值，对应 `svm_oof_margin_threshold.csv`。阈值改变 precision/recall/F1，不改变同一组 margin 的 AP/ROC-AUC。
- **校准结果：**`svm_calibration_results.csv` 中的 `Calibrated AP`、Brier、log loss、ECE。概率阈值 0.20–0.60 只展示预设情景，不从 test F1 反选阈值。

使用**非嵌套五折 CV**。OOF max F1 是训练内阈值选择依据，并非无偏泛化性能估计。Month holdout 是基于月份的分布变化诊断，不能声称为严格时间回测。固定 test 之前已经在项目中查看过；重新运行不构成全新的未见测试。

## 对原报告/PPT的影响

本包没有修改任何外部 report/PPT。原模型、预处理、搜索范围、固定数据、默认阈值评价和原含 Month 实验均保留，便于核对历史结果。若报告采用新的 OOF 阈值分类指标或新增 Month-excluded 实验，应相应更新该处方法说明和数值，不能把旧的默认阈值 recall/F1 当作新阈值结果。校准 AP 也不能替换原始 margin AP。

## 数据一致性与分享

默认核对随包标准 CSV 的 SHA-256。若提示哈希不一致，应先核对数据来源、文件内容和 CSV 换行/编码，不要直接绕过检查。

Notebook 源码及已保存输出不包含个人绝对路径、凭据或临时模型。PNG 以输出形式嵌入 Notebook；单独复制 Notebook 后仍可查看附带图像。运行产生的 CSV、PNG、JSON 均在结果目录。

## 本次交付的实际运行验证

- 已用全新 kernel 顺序执行所有 13 个代码单元，无错误输出；保存 6 张嵌入图片，完整运行耗时 16.2 分钟。
- 主实验原始 margin AP = 0.348299596，与原参考值一致；独立的 sigmoid ensemble AP = 0.351037490。
- 训练 OOF margin 阈值 = 0.318853831；固定 test precision / recall / F1 = 0.311653 / 0.602094 / 0.410714。
- 原含 Month 和新增不含 Month 两组实验均已实际执行并保留。
- 在本机 scikit-learn 1.9.0 另做了 500 个训练样本的 API 兼容性检查，未出现警告；这不是该版本下的完整结果复现。
- 独立检查了 36 组 OOF 阈值候选与并列情况，并核对逐行分数、指标和结果文件哈希。
- 详细信息见 `verification.json`；各实验结果见随附的 `results/`。
