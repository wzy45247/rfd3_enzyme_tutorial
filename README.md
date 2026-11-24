# RFD3 酶设计流程复现

本项目复现基于 RFD3、LigandMPNN 和 RF3 的酶活性位点约束设计流程。以酵母 Ulp1 蛋白酶结构 `1euv_lig.pdb` 为输入，保留配体及催化相关残基的空间约束，生成候选骨架、设计序列，并通过 RF3 回折叠评价设计结构与目标骨架的一致性。

## 工作流程

1. 读取带配体的 1EUV 输入结构。
2. 设置配体、催化残基、设计长度和溶剂可及性约束。
3. 使用 RFD3 生成候选蛋白骨架。
4. 根据结构质量指标筛选候选骨架。
5. 使用 LigandMPNN 为候选骨架设计序列。
6. 使用 RF3 对设计序列进行结构预测。
7. 计算主链 RMSD 等指标，并导出 PyMOL 比较文件。

## 目录结构

```text
rfd3_enzyme_tutorial/
├── README.md
├── enzyme.ipynb
├── inputs/
│   └── 1euv_lig.pdb
└── complete_outputs/
    ├── rfd3/             # RFD3 候选骨架和元数据
    ├── mpnn/             # LigandMPNN 设计结构
    ├── pymol/            # 最终候选及可视化文件
    └── rf3_all_results.csv
```

## 主要结果

- RFD3 共生成 8 个候选骨架。
- `complete_outputs/rf3_all_results.csv` 汇总了 RF3 回折叠结果。
- `complete_outputs/pymol/` 保存筛选候选的目标结构、预测结构和 PyMOL 比较文件。

## 使用说明

主要分析和运行步骤记录在 `enzyme.ipynb` 中。运行前需要配置 Foundry/RFD3、LigandMPNN、RF3 及其模型权重。模型权重、软件环境和大型临时输出不纳入本仓库。

输入、参数、筛选过程和关键结果均保留在 Notebook 与输出目录中，以便复查和复现。
