<div align="center">

# Awesome XRD to Crystal

**Un mapa curado de conocimiento para identificación, generación, descomposición y refinamiento de cristales a partir de PXRD.**

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/Bin-Cao/awesome-xrd2crystal?style=flat&logo=github&label=Stars)](https://github.com/Bin-Cao/awesome-xrd2crystal/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/Bin-Cao/awesome-xrd2crystal?style=flat&logo=github&label=Forks)](https://github.com/Bin-Cao/awesome-xrd2crystal/forks)
[![Issues](https://img.shields.io/github/issues/Bin-Cao/awesome-xrd2crystal?style=flat&logo=github&label=Issues)](https://github.com/Bin-Cao/awesome-xrd2crystal/issues)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

[English](README.md) · [中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · **Español** · [Deutsch](README.de.md)

</div>

---

## Descripción General

Este repositorio reúne, en orden cronológico, artículos, código, conjuntos de datos, benchmarks y herramientas sobre **XRD/PXRD a estructura cristalina**. Cubre identificación de fases, predicción de simetría y red cristalina, descomposición multifase, automatización de Rietveld, generación ab-initio de estructuras e interpretación autónoma o in-situ.

El problema PXRD a estructura es un problema inverso mal condicionado: varias estructuras pueden producir patrones 1D similares, y los perfiles experimentales pueden incluir ensanchamiento instrumental, efectos de tamaño, orientación preferente, fondo, impurezas y solapamiento de picos.

| Dirección | Objetivo típico |
|---|---|
| Identificación de fases | Buscar o clasificar fases conocidas desde patrones PXRD |
| Predicción de simetría y red | Predecir sistema cristalino, grupo espacial o parámetros de red |
| Descomposición multifase | Separar patrones mixtos y estimar fracciones de fase |
| Automatización de Rietveld | Acelerar refinamiento, estimación de parámetros y optimización global |
| Solución generativa de estructuras | Generar cristales 3D, coordenadas atómicas, red o CIF desde PXRD |
| Análisis autónomo/in-situ | Analizar datos de difracción en vivo y cerrar ciclos experimentales |

Para mantener citas, enlaces y cronología consistentes, la lista completa se mantiene en el archivo principal en inglés: [README.md](README.md#contents).

## Accesos Rápidos

- [Índice completo](README.md#contents)
- [End-to-End PXRD to Crystal Structure](README.md#end-to-end-pxrd--crystal-structure-generative)
- [Identificación de fases desde XRD](README.md#phase-identification-from-xrd)
- [Predicción de sistema cristalino / grupo espacial / red](README.md#crystal-system--space-group--lattice-prediction-from-xrd)
- [Descomposición multifase y refinamiento Rietveld](README.md#multi-phase-decomposition--rietveld-refinement)
- [Datasets y benchmarks](README.md#datasets--benchmarks)
- [Guía de contribución](CONTRIBUTING.md)

