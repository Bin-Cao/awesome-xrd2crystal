<div align="center">

# Awesome XRD to Crystal

**PXRD 기반 결정 식별, 생성, 분해, 정련을 위한 큐레이션 지식 맵.**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/Bin-Cao/awesome-xrd2crystal?style=flat&logo=github&label=Stars)](https://github.com/Bin-Cao/awesome-xrd2crystal/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/Bin-Cao/awesome-xrd2crystal?style=flat&logo=github&label=Forks)](https://github.com/Bin-Cao/awesome-xrd2crystal/forks)
[![Issues](https://img.shields.io/github/issues/Bin-Cao/awesome-xrd2crystal?style=flat&logo=github&label=Issues)](https://github.com/Bin-Cao/awesome-xrd2crystal/issues)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

[English](README.md) · [中文](README.zh-CN.md) · [日本語](README.ja.md) · **한국어** · [Español](README.es.md) · [Deutsch](README.de.md)

</div>

---

## 개요

이 저장소는 **XRD/PXRD에서 결정 구조로** 이어지는 연구 주제의 논문, 코드, 데이터셋, 벤치마크, 도구를 시간순으로 정리한 큐레이션 목록입니다. 상 식별, 결정계/공간군/격자 예측, 다상 분해, Rietveld 자동화, 생성 모델 기반 구조 결정, in-situ 및 자율 실험 분석을 포함합니다.

PXRD로부터 구조를 추정하는 문제는 ill-posed inverse problem입니다. 서로 다른 구조가 유사한 1D 회절 패턴을 만들 수 있고, 실험 데이터에는 장비 broadening, 크기 효과, 배향, 배경, 불순물 상, peak overlap 등이 포함될 수 있습니다.

| 방향 | 일반적인 목표 |
|---|---|
| 상 식별 | PXRD 패턴에서 알려진 상을 검색하거나 분류 |
| 대칭성 및 격자 예측 | 결정계, 공간군, 소광군, 격자 파라미터 예측 |
| 다상 분해 | 혼합 패턴을 분리하고 상 분율 추정 |
| Rietveld 자동화 | 정련, 파라미터 추정, 전역 최적화 가속 |
| 생성형 구조 결정 | PXRD에서 3D 결정, 원자 좌표, 격자, CIF 생성 |
| 자율/in-situ 분석 | 실시간 회절 스트림 분석 및 실험 피드백 루프 구성 |

인용, 링크, 시간순 정렬을 일관되게 유지하기 위해 전체 논문 목록은 영어 기본 파일에서 관리합니다: [README.md](README.md#contents).

## 빠른 링크

- [전체 목차](README.md#contents)
- [End-to-End PXRD to Crystal Structure](README.md#end-to-end-pxrd--crystal-structure-generative)
- [XRD 기반 상 식별](README.md#phase-identification-from-xrd)
- [결정계 / 공간군 / 격자 예측](README.md#crystal-system--space-group--lattice-prediction-from-xrd)
- [다상 분해 및 Rietveld 정련](README.md#multi-phase-decomposition--rietveld-refinement)
- [데이터셋 및 벤치마크](README.md#datasets--benchmarks)
- [기여 가이드](CONTRIBUTING.md)

