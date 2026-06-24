<div align="center">

# Awesome XRD to Crystal

**面向 PXRD 驱动晶体识别、生成、分解与精修的精选知识图谱。**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/Bin-Cao/awesome-xrd2crystal?style=flat&logo=github&label=Stars)](https://github.com/Bin-Cao/awesome-xrd2crystal/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/Bin-Cao/awesome-xrd2crystal?style=flat&logo=github&label=Forks)](https://github.com/Bin-Cao/awesome-xrd2crystal/forks)
[![Issues](https://img.shields.io/github/issues/Bin-Cao/awesome-xrd2crystal?style=flat&logo=github&label=Issues)](https://github.com/Bin-Cao/awesome-xrd2crystal/issues)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

[English](README.md) · **中文** · [日本語](README.ja.md) · [한국어](README.ko.md) · [Español](README.es.md) · [Deutsch](README.de.md)

</div>

---

## 项目概览

本仓库系统整理 **XRD/PXRD 到晶体结构** 相关的论文、代码、数据集、基准和工具，覆盖物相识别、晶系/空间群/晶格预测、多相分解、Rietveld 自动化、端到端晶体结构生成以及原位/自主实验分析等方向。

PXRD 到结构是典型的病态反问题：不同结构可能产生相似的一维衍射图谱，而实验数据还会受到仪器展宽、晶粒尺寸、择优取向、背景、杂相和峰重叠等因素影响。

| 方向 | 典型目标 |
|---|---|
| 物相识别 | 从 PXRD 图谱中检索或分类已知物相 |
| 对称性与晶格预测 | 预测晶系、空间群、消光群或晶格参数 |
| 多相分解 | 分离混合图谱并估计相含量 |
| Rietveld 自动化 | 加速精修、参数估计和全局优化 |
| 生成式结构解析 | 从 PXRD 生成三维晶体、原子坐标、晶格或 CIF |
| 自主/原位分析 | 解析实时衍射数据流并闭环指导实验 |

完整论文清单目前维护在英文主文件中，以保证引用、链接和时间顺序一致：请查看 [README.md](README.md#contents)。

## 快速入口

- [完整目录](README.md#contents)
- [端到端 PXRD 到晶体结构生成](README.md#end-to-end-pxrd--crystal-structure-generative)
- [XRD 物相识别](README.md#phase-identification-from-xrd)
- [晶系 / 空间群 / 晶格预测](README.md#crystal-system--space-group--lattice-prediction-from-xrd)
- [多相分解与 Rietveld 精修](README.md#multi-phase-decomposition--rietveld-refinement)
- [数据集与基准](README.md#datasets--benchmarks)
- [贡献指南](CONTRIBUTING.md)

