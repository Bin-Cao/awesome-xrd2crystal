<div align="center">

# Awesome XRD to Crystal

**PXRD による結晶同定、生成、分解、精密化のためのキュレーション知識マップ。**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/Bin-Cao/awesome-xrd2crystal?style=flat&logo=github&label=Stars)](https://github.com/Bin-Cao/awesome-xrd2crystal/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/Bin-Cao/awesome-xrd2crystal?style=flat&logo=github&label=Forks)](https://github.com/Bin-Cao/awesome-xrd2crystal/forks)
[![Issues](https://img.shields.io/github/issues/Bin-Cao/awesome-xrd2crystal?style=flat&logo=github&label=Issues)](https://github.com/Bin-Cao/awesome-xrd2crystal/issues)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

[English](README.md) · [中文](README.zh-CN.md) · **日本語** · [한국어](README.ko.md) · [Español](README.es.md) · [Deutsch](README.de.md)

</div>

---

## 概要

このリポジトリは、**XRD/PXRD から結晶構造へ** という研究領域に関する論文、コード、データセット、ベンチマーク、ツールを時系列で整理したキュレーションリストです。相同定、結晶系・空間群・格子予測、多相分解、Rietveld 自動化、生成モデルによる構造決定、in-situ/自律実験解析を対象とします。

PXRD から構造を推定する問題は不適切設定の逆問題であり、複数の候補構造が類似した一次元回折パターンを与える可能性があります。実験パターンには装置由来の広がり、サイズ効果、配向、バックグラウンド、不純物相、ピーク重なりも含まれます。

| 方向 | 典型的な目的 |
|---|---|
| 相同定 | PXRD パターンから既知相を検索または分類する |
| 対称性・格子予測 | 結晶系、空間群、消滅則、格子定数を予測する |
| 多相分解 | 混合パターンを分離し、相分率を推定する |
| Rietveld 自動化 | 精密化、パラメータ推定、全局最適化を高速化する |
| 生成的構造決定 | PXRD から 3D 結晶、原子座標、格子、CIF を生成する |
| 自律・in-situ 解析 | リアルタイム回折データを解析し、実験ループを閉じる |

引用、リンク、年代順を一貫して保つため、完全な論文リストは英語版で管理しています: [README.md](README.md#contents)。

## クイックリンク

- [完全な目次](README.md#contents)
- [End-to-End PXRD to Crystal Structure](README.md#end-to-end-pxrd--crystal-structure-generative)
- [XRD による相同定](README.md#phase-identification-from-xrd)
- [結晶系 / 空間群 / 格子予測](README.md#crystal-system--space-group--lattice-prediction-from-xrd)
- [多相分解と Rietveld 精密化](README.md#multi-phase-decomposition--rietveld-refinement)
- [データセットとベンチマーク](README.md#datasets--benchmarks)
- [コントリビューションガイド](CONTRIBUTING.md)

