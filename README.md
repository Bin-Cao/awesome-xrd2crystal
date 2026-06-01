# Awesome XRD → Crystal [![Awesome](https://awesome.re/badge.svg)](https://awesome.re) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> A curated, chronologically organized collection of papers, code, and datasets on **(powder) X-ray diffraction (XRD/PXRD) → crystal structure** — identification, symmetry classification, ab-initio structure determination, generative modeling, multi-phase decomposition, refinement, and related machine-learning topics.

The PXRD → structure problem is an ill-posed inverse problem: many candidate structures can produce similar 1D patterns, and experimental profiles contain instrumental broadening, finite-size effects, texture/preferred orientation, background, impurity phases, and peak overlap. Work in this space spans (1) phase identification and search-match, (2) symmetry / lattice / space-group prediction, (3) multi-phase decomposition and Rietveld automation, (4) autonomous/in-situ analysis, and (5) end-to-end generative ab-initio structure solution.

Within every section, entries are listed **chronologically (oldest → newest)** in a standardized format.

> 📢 **Contributions, corrections, and translations are warmly welcomed — 欢迎补充、纠正与翻译！**
> If a paper is missing, a link is broken, or an author/affiliation is wrong, please [open an issue](https://github.com/Bin-Cao/awesome-xrd2crystal/issues/new) or send a PR. See [CONTRIBUTING.md](CONTRIBUTING.md). All contributors are credited in the [Contributors](#contributors) section at the bottom.

## Maintainers 

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/Bin-Cao">
        <img src="https://github.com/Bin-Cao.png?size=120" width="96" alt="Bin Cao"/><br/>
        <sub><b>Bin Cao</b></sub>
      </a><br/>
      <sub>@Bin-Cao</sub>
    </td>
    <td align="center">
      <a href="https://github.com/OPilgrim">
        <img src="https://github.com/OPilgrim.png?size=120" width="96" alt="Yunyue Su"/><br/>
        <sub><b>Yunyue Su</b></sub>
      </a><br/>
      <sub>@OPilgrim</sub>
    </td>
    <td align="center">
      <a href="https://github.com/komusama0930">
        <img src="https://github.com/komusama0930.png?size=120" width="96" alt="Shuchen Pu"/><br/>
        <sub><b>Shuchen Pu</b></sub>
      </a><br/>
      <sub>@komusama0930</sub>
    </td>
  </tr>
</table>

This list is jointly curated by the maintainers above. For paper additions, please open an issue or PR; for scope or organizational questions, feel free to tag any maintainer directly.

---

## Classification vs. Generation — quick guide

Two complementary problem formulations recur throughout this list. Pick the section that matches your task:

| Task | Input | Output | Sections |
|---|---|---|---|
| **Phase / structure identification** (classification, retrieval) | PXRD pattern | Index of a known phase, crystal system, or space group | [Phase Identification](#phase-identification-from-xrd) · [Crystal System / Space Group / Lattice](#crystal-system--space-group--lattice-prediction-from-xrd) |
| **Multi-phase decomposition** | Mixed PXRD pattern | Per-phase weight fractions and component patterns | [Multi-phase Decomposition & Rietveld](#multi-phase-decomposition--rietveld-refinement) |
| **Ab-initio structure generation** | PXRD pattern (± composition / cell) | Full 3D crystal (atom species + fractional coordinates + lattice / CIF) | [End-to-End PXRD → Crystal Structure (Generative)](#end-to-end-pxrd--crystal-structure-generative) |
| **Autonomous / in-situ analysis** | Live PXRD stream from beamline / lab | Phase calls, next-measurement policy, synthesis decisions | [Autonomous / In-situ XRD](#autonomous--in-situ-xrd-analysis) |

Classification models are typically lighter, require no symmetry equivariance, and degrade gracefully on out-of-distribution patterns; generative models target atomic-resolution structure but rely on stronger physical priors and are still constrained by training-set coverage.

---

## Contents

- [Maintainers · 维护者](#maintainers--维护者)
- [End-to-End PXRD → Crystal Structure (Generative)](#end-to-end-pxrd--crystal-structure-generative)
- [Phase Identification from XRD](#phase-identification-from-xrd)
- [Crystal System / Space Group / Lattice Prediction from XRD](#crystal-system--space-group--lattice-prediction-from-xrd)
- [Multi-phase Decomposition & Rietveld Refinement](#multi-phase-decomposition--rietveld-refinement)
- [Autonomous / In-situ XRD Analysis](#autonomous--in-situ-xrd-analysis)
- [Datasets & Benchmarks](#datasets--benchmarks)
- [Simulation, Refinement, and Utility Tools](#simulation-refinement-and-utility-tools)
- [Reviews & Surveys](#reviews--surveys)
- [Related Curated Lists](#related-curated-lists)
- [Contributing](#contributing)
- [Contributors](#contributors)

### Standard entry format

```
### YYYY · ShortName — One-sentence tagline
- **Title:** <full paper title>
- **Authors:** <first author> (<affiliation>), ..., <senior author> (<affiliation>)
- **Venue:** <journal vol, pp (year)>; arXiv:<id>
- **Paper:** <https://...>
- **Code:** <https://...>     (omit if none)
- **Data:** <https://...>     (omit if none)
- **TL;DR:** <1–3 sentences>
```

---

## End-to-End PXRD → Crystal Structure (Generative)

Methods that take a PXRD pattern (optionally + composition / lattice) and output a full 3D crystal structure (atomic positions + lattice, typically as CIF or coordinates).

### 2024 · CrystalNet — Coordinate-based VAE for electron density from PXRD

- **Title:** Towards end-to-end structure determination from X-ray diffraction data using deep learning
- **Authors:** Gabe Guo, Judah Goldfeder, Ling Lan, et al.; senior: Hod Lipson (Columbia University)
- **Venue:** *npj Computational Materials* 10, 209 (2024); arXiv:2312.15136
- **Paper:** <https://www.nature.com/articles/s41524-024-01401-8> · <https://arxiv.org/abs/2312.15136>
- **Code:** <https://github.com/gabeguo/deep-crystallography-public>
- **TL;DR:** Conditional implicit neural representation predicts a Cartesian-mapped electron-density field from PXRD + composition; up to 93.4% SSIM on cubic test cases, 74.1% average on trigonal.

### 2024 · XtalNet — Contrastive PXRD-crystal pretraining + conditional equivariant diffusion

- **Title:** End-to-End Crystal Structure Prediction from Powder X-Ray Diffraction
- **Authors:** Qingsi Lai, Fanjie Xu, Lin Yao, Zhifeng Gao, et al.; senior: Guolin Ke (DP Technology, Beijing) — collab. Peking Univ., Xiamen Univ., AI for Science Institute
- **Venue:** *Advanced Science* (2025); arXiv:2401.03862 (Jan 2024)
- **Paper:** <https://arxiv.org/abs/2401.03862> · <https://onlinelibrary.wiley.com/doi/10.1002/advs.202410722>
- **Code:** <https://github.com/dptech-corp/XtalNet>
- **Data:** <https://zenodo.org/records/13629658>
- **TL;DR:** Two-module pipeline — Contrastive PXRD-Crystal Pretraining (CPCP) + Conditional Crystal Structure Generation (CCSG) — that scales PXRD-conditioned CSP up to MOFs with 400 atoms/cell (90.2%/79% Top-10 match on hMOF-100/400).

### 2024 · Crystalyze — XRD encoder + CDVAE diffusion

- **Title:** Crystal Structure Determination from Powder Diffraction Patterns with Generative Machine Learning
- **Authors:** Eric A. Riesel (MIT), Tsach Mackey (Yale), et al.; seniors: Danna E. Freedman (MIT), Jure Leskovec (Stanford)
- **Venue:** *J. Am. Chem. Soc.* 146, 30340–30348 (2024)
- **Paper:** <https://pubs.acs.org/doi/10.1021/jacs.4c10244>
- **Code:** <https://github.com/ML-PXRD/Crystalyze>
- **TL;DR:** Pretrained XRD encoder feeding CDVAE; ~42% match rate on experimental and ~67% on simulated patterns; solved previously-unsolved Powder Diffraction File entries.

### 2025 · PXRDnet — SE(3)-equivariant score-based diffusion for nanocrystalline PXRD

- **Title:** Ab initio structure solutions from nanocrystalline powder diffraction data via diffusion models
- **Authors:** Gabe Guo (Columbia), Tristan Saidi (Columbia), Maxwell Terban (MPI Solid State Research), Michele Liu (Columbia), Hamed Salimian (Columbia), Simon J. L. Billinge (Columbia/BNL); senior: Hod Lipson (Columbia)
- **Venue:** *Nature Materials* 24, 1726–1734 (2025); arXiv:2406.10796
- **Paper:** <https://www.nature.com/articles/s41563-025-02220-y> · <https://arxiv.org/abs/2406.10796>
- **Code:** <https://github.com/gabeguo/cdvae_xrd>
- **TL;DR:** Score-based diffusion conditioned on finite-size-broadened PXRD + formula; works on simulated nanocrystals as small as 10 Å and on real experimental patterns spanning all seven crystal systems; median RMSD ≤ 0.11 Å on MP-20-PXRD.

### 2025 · PXRDGen — Contrastive XRD encoder + flow/diffusion + automated Rietveld

- **Title:** Powder diffraction crystal structure determination using generative models
- **Authors:** Qi Li (IoP, CAS), Rui Jiao (Tsinghua), Liang Wu, Tao Zhu, et al.; seniors: Wenbing Huang (Renmin Univ.), Shifeng Jin (IoP, CAS)
- **Venue:** *Nature Communications* 16, 7428 (2025); arXiv:2409.04727
- **Paper:** <https://www.nature.com/articles/s41467-025-62708-8> · <https://arxiv.org/abs/2409.04727>
- **Code:** <https://codeocean.com/capsule/2196660/> (DOI: 10.24433/CO.6347299.v1)
- **TL;DR:** Contrastive-pretrained XRD encoder + DiffCSP-style diffusion/flow generator + integrated Rietveld refinement; 82% valid compounds from a single sample on MP-20, 96% within 20.

### 2025 · deCIFer — Autoregressive transformer over CIF tokens conditioned on PXRD

- **Title:** deCIFer: Crystal Structure Prediction from Powder Diffraction Data using Autoregressive Language Models
- **Authors:** Frederik Lizak Johansen, Ulrik Friis-Jensen, Erik Bjørnager Dam, Kirsten M. Ø. Jensen, Rocío Mercado, Raghavendra Selvan — University of Copenhagen (DIKU & Department of Chemistry)
- **Venue:** TMLR / OpenReview 2025; arXiv:2502.02189
- **Paper:** <https://arxiv.org/abs/2502.02189> · <https://openreview.net/forum?id=LftFQ35l47>
- **Code:** <https://github.com/FrederikLizakJohansen/deCIFer>
- **TL;DR:** Decoder-only transformer that emits CIF text token-by-token conditioned on PXRD embeddings; ~94% structure match in the author setting on NOMA1/CHILI-100K-derived data.

### 2025 · DiffractGPT / AtomGPT — Generative pretrained transformer for XRD → structure

- **Title:** DiffractGPT: Atomic Structure Determination from X-ray Diffraction Patterns Using a Generative Pretrained Transformer
- **Authors:** Kamal Choudhary — NIST, Material Measurement Laboratory (also Johns Hopkins University)
- **Venue:** *J. Phys. Chem. Lett.* (2025); arXiv:2508.08349
- **Paper:** <https://pubs.acs.org/doi/10.1021/acs.jpclett.4c03137> · <https://arxiv.org/abs/2508.08349>
- **Code:** <https://github.com/usnistgov/atomgpt> · <https://github.com/usnistgov/diffractgpt>
- **TL;DR:** Mistral-style LLM fine-tuned on JARVIS-DFT simulated PXRD to emit CIF-like crystal descriptions; lattice MAE ~0.17–0.27 Å for a/b/c (DGPT-formula).

### 2025 · Uni-3DAR — Unified 3D autoregressive generation on compressed spatial tokens

- **Title:** Uni-3DAR: Unified 3D Generation and Understanding via Autoregression on Compressed Spatial Tokens
- **Authors:** Shuqi Lu, Haowei Lin, Lin Yao, Zhifeng Gao, Xiaohong Ji, Weinan E, Linfeng Zhang, Guolin Ke — DP Technology / Peking Univ. / AISI
- **Venue:** arXiv:2503.16278 (Mar 2025)
- **Paper:** <https://arxiv.org/abs/2503.16278> · project: <https://uni-3dar.github.io/>
- **Code:** <https://github.com/dptech-corp/Uni-3DAR> · weights: <https://huggingface.co/dptech/Uni-3DAR>
- **TL;DR:** Octree-based hierarchical tokenization + autoregressive 3D modeling; on PXRD-conditioned CSP MP-20 reaches 75.08% match rate, RMSE 0.0276.

### 2025 · CrystaLLM-π — Property- and PXRD-conditioned CIF language model

- **Title:** CrystaLLM-π: Property- and PXRD-Conditioned Generation of Crystal Structures with a CIF Language Model
- **Authors:** C-Bone-UCL group (University College London); builds on CrystaLLM (Antunes et al., Univ. of Reading)
- **Venue:** preprint / open-source release (2025)
- **Code:** <https://github.com/C-Bone-UCL/CrystaLLM-2.0> · weights: `CrystaLLM-pi_COD-XRD`, `CrystaLLM-pi_Mattergen-XRD` on Hugging Face
- **Base model:** <https://arxiv.org/abs/2307.04340> · <https://github.com/lantunes/CrystaLLM>
- **TL;DR:** Adds bandgap, density, photovoltaic efficiency and PXRD conditioning streams to the CrystaLLM CIF autoregressive language model. The base model is **CrystaLLM** (Antunes et al., *Nat. Commun.* 15, 10570, 2024) — a GPT-style decoder-only language model trained on millions of CIF files that emits crystal structures as CIF text token by token.

### 2026 · XRDSol — Equivariant diffusion solver for inorganic PXRD

- **Title:** Equivariant diffusion solution for inorganic crystal structure determination from powder X-ray diffraction data
- **Authors:** Dongfang Yu, Zhewen Zhu (Zhejiang Univ. / Westlake Univ.), Fucheng Leng (Univ. College Cork); senior: Yizhou Zhu (Westlake Univ.)
- **Venue:** *Nature Communications* 17, 3274 (2026)
- **Paper:** <https://www.nature.com/articles/s41467-026-70035-9>
- **Code:** <https://github.com/ai4mat-zhu/XRDSol>
- **TL;DR:** EGNN-based denoising diffusion conditioned on stoichiometry + unit cell + PXRD; ~82.3% success on MP-20, 81.6% on ICDD-20 experimental benchmark; ~0.6 s per solution on one GPU.

### 2026 · RealPXRD-Solver — Flow-matching solver with experimental augmentation

- **Title:** Experimental Powder X-ray Diffraction Crystal Structure Determination with RealPXRD-Solver
- **Authors:** Qi Li et al. — Institute of Physics, CAS (with DP Technology, Tsinghua, Renmin Univ., SJTU, AISI)
- **Venue:** arXiv:2603.00965 (Mar 2026)
- **Paper:** <https://arxiv.org/abs/2603.00965>
- **Code:** <https://github.com/liqi-529/RealPXRD-Solver>
- **TL;DR:** Universal encoder of d-spacing–intensity fingerprints trained on 6,250,238 theoretical structures with experiment-mimicking augmentations; lattice-conditioned and lattice-free modes; 77.9%/91.9% Top-1/Top-20 on CNRS, 78.8%/92.9% on RRUFF; solved 39 previously-unreported PDF entries.

### 2026 · Hybrid Ab-initio PXRD Solver — Discrete search + continuous optimization

- **Title:** Ab-initio Crystal Structure Determination from Powder X-Ray Diffraction
- **Authors:** Kaixiang Su, Osman Goni Ridwan, Hongfei Xue; senior: Qiang Zhu — UNC Charlotte
- **Venue:** arXiv:2605.24594 (May 2026)
- **Paper:** <https://arxiv.org/abs/2605.24594>
- **TL;DR:** Hierarchical pipeline: (1) discrete search over space group / unit cell / Wyckoff combinations, (2) continuous coordinate optimization with AI-based peak profile analysis, density estimation, and physics-informed energy constraints.

---

## Phase Identification from XRD

Methods that, given a PXRD pattern, predict which known phase(s) it corresponds to (classification / multi-label / one-to-one ID).

### 2017 · Iwasaki et al. — Dissimilarity measures for clustering combinatorial XRD

- **Title:** Comparison of dissimilarity measures for cluster analysis of X-ray diffraction data from combinatorial libraries
- **Authors:** Yuma Iwasaki (NIMS), A. Gilad Kusne (NIST/UMD), Ichiro Takeuchi (UMD)
- **Venue:** *npj Computational Materials* 3, 4 (2017)
- **Paper:** <https://www.nature.com/articles/s41524-017-0006-2>
- **TL;DR:** Systematic comparison of cosine, Pearson, JSD, NCDTW and other dissimilarity measures for grouping XRD patterns of Fe–Co–Ni composition spreads; foundation for downstream unsupervised phase mapping.

### 2019 · Oviedo et al. — Fast and interpretable XRD classification

- **Title:** Fast and interpretable classification of small X-ray diffraction datasets using data augmentation and deep neural networks
- **Authors:** Felipe Oviedo (MIT Photovoltaics Research Lab), et al.; senior: Tonio Buonassisi (MIT) — collab. NIST
- **Venue:** *npj Computational Materials* 5, 60 (2019)
- **Paper:** <https://www.nature.com/articles/s41524-019-0196-x>
- **Code:** <https://github.com/PV-Lab/autoXRD>
- **TL;DR:** Physics-informed augmentation lets 1D a-CNNs train from small experimental XRD sets; introduces CAM-based interpretability for crystal-system / dimensionality / space-group classification of thin films.

### 2020 · Lee et al. — Deep CNN for multiphase inorganic phase ID

- **Title:** A deep-learning technique for phase identification in multiphase inorganic compounds using synthetic XRD powder patterns
- **Authors:** Jin-Woong Lee, Woon Bae Park, Jin Hee Lee, Satendra Pal Singh; senior: Kee-Sun Sohn — Sejong University
- **Venue:** *Nature Communications* 11, 86 (2020)
- **Paper:** <https://www.nature.com/articles/s41467-019-13749-3>
- **TL;DR:** CNN trained on ~1.78 M simulated PXRD patterns across the Sr-Li-Al-O quaternary; near-perfect identification on experimental multi-phase compounds.

### 2020 · Wang et al. — Interpretable CNN for one-to-one MOF XRD ID

- **Title:** Rapid Identification of X-ray Diffraction Patterns Based on Very Limited Data by Interpretable Convolutional Neural Networks
- **Authors:** Hong Wang, Yunchao Xie, Dawei Li, Heng Deng, Yunxin Zhao, Ming Xin; senior: Jian Lin — University of Missouri
- **Venue:** *J. Chem. Inf. Model.* 60, 2004–2011 (2020); arXiv:1912.07750
- **Paper:** <https://pubs.acs.org/doi/10.1021/acs.jcim.0c00020> · <https://arxiv.org/abs/1912.07750>
- **TL;DR:** CNN trained on theoretical MOF XRD patterns augmented with noise from limited experiments; 96.7% Top-5 identification accuracy with class-activation interpretation.

### 2021 · Lee et al. — Phase ID + quantitative phase-fraction prediction

- **Title:** A data-driven XRD analysis protocol for phase identification and phase-fraction prediction of multiphase inorganic compounds
- **Authors:** Jin-Woong Lee, Woon Bae Park, Minseuk Kim, Satendra Pal Singh, Myoungho Pyo; senior: Kee-Sun Sohn — Sejong University
- **Venue:** *Inorganic Chemistry Frontiers* 8, 2492 (2021)
- **Paper:** <https://pubs.rsc.org/en/content/articlelanding/2021/qi/d0qi01513j>
- **TL;DR:** Extends Lee 2020 to the Li-La-Zr-O quaternary; 96.47% test phase-ID accuracy and R² ≈ 0.97 phase-fraction regression on simulated data (91.11% / 0.96 on experimental).

### 2023 · NeuralXRD — Synthetic + real ML for transition-metal phase ID

- **Title:** Machine Learning-Assisted Close-Set X-ray Diffraction Phase Identification of Transition Metals
- **Authors:** Maksim Eremeev et al.
- **Venue:** ICLR 2023 ML4Materials Workshop
- **Code:** <https://github.com/maxnygma/NeuralXRD>
- **TL;DR:** Combines synthetic phase generation, peak integration, and post-hoc calibration to identify transition-metal phases from XRD; ships demo notebooks operating on COD-derived patterns.

### 2024 · CPICANN — Convolutional self-attention phase identifier

- **Title:** Crystallographic phase identifier of a convolutional self-attention neural network (CPICANN) on powder diffraction patterns
- **Authors:** Shouyang Zhang, Bin Cao; senior: Tong-Yi Zhang — HKUST(GZ)
- **Venue:** *IUCrJ* 11, 634 (2024)
- **Paper:** <https://journals.iucr.org/m/issues/2024/04/00/lt5076/>
- **Code:** <https://github.com/WPEM/CPICANN>
- **Data:** <https://huggingface.co/datasets/caobin/datasetCPICANN>
- **TL;DR:** Self-attention–augmented CNN performing whole-pattern phase identification across four benchmarks of varying background and noise level.

### 2024 · MLstructureMining — ML structure ID from atomic PDFs

- **Title:** MLstructureMining: a machine learning tool for structure identification from X-ray pair distribution functions
- **Authors:** Emil T. S. Kjær, Andy S. Anker, Andrea Kirsch, et al.; seniors: Simon J. L. Billinge (Columbia), Kirsten M. Ø. Jensen (Copenhagen)
- **Venue:** *Digital Discovery* (2024); DOI 10.1039/D4DD00001C
- **Paper:** <https://pubs.rsc.org/en/content/articlehtml/2024/dd/d4dd00001c>
- **TL;DR:** Tree-ensemble classifier trained on simulated PDFs to identify candidate structures for in-situ / operando experiments; complements direct PXRD methods on the PDF side.

### 2025 · XQueryer — 1.03 B-parameter transformer crystal identifier

- **Title:** XQueryer: an intelligent crystal structure identifier for powder X-ray diffraction
- **Authors:** Bin Cao, Zinan Zheng, Yang Liu, Longhan Zhang, Lawrence W. Y. Wong, Lu-Tao Weng, Jia Li, Haoxiang Li, Tong-Yi Zhang — HKUST(GZ) / HKUST
- **Venue:** *National Science Review* 12(12), nwaf421 (2025); DOI 10.1093/nsr/nwaf421
- **Paper:** <https://doi.org/10.1093/nsr/nwaf421>
- **Code:** <https://github.com/Bin-Cao/XQueryer> · benchmark: <https://github.com/Bin-Cao/XqueryerBench>
- **TL;DR:** 1.03 B-parameter transformer trained on ~2 M high-fidelity simulated spectra; integrates with a powder diffractometer for real-time identification and ships RRUFF↔MP ID matching utilities and a PXRD simulator.

---

## Crystal System / Space Group / Lattice Prediction from XRD

### 2017 · Park et al. — CNN for crystal system / extinction group / space group

- **Title:** Classification of crystal structure using a convolutional neural network
- **Authors:** Woon Bae Park, Jiyong Chung, Jaeyoung Jung, Keemin Sohn, Satendra Pal Singh, Myoungho Pyo, Namsoo Shin; senior: Kee-Sun Sohn — Sejong University
- **Venue:** *IUCrJ* 4, 486–494 (2017)
- **Paper:** <https://journals.iucr.org/m/issues/2017/04/00/fc5018/index.html>
- **TL;DR:** Three CNNs trained on ~150 k synthetic PXRD patterns from ICSD; 94.99% crystal-system, 83.83% extinction-group, 81.14% space-group accuracy.

### 2019 · Aguiar et al. — CNN decoding crystallography from electron diffraction

- **Title:** Decoding crystallography from high-resolution electron imaging and diffraction datasets with deep learning
- **Authors:** Jeffery A. Aguiar (INL/Univ. of Utah), Matthew L. Gong, Raymond Unocic, Tolga Tasdizen, Brian Miller
- **Venue:** *Science Advances* 5, eaaw1949 (2019)
- **Paper:** <https://www.science.org/doi/10.1126/sciadv.aaw1949>
- **TL;DR:** CNN trained on 571,340 diffraction patterns across 7 families / 32 genera / 230 space groups; reduces the candidate space groups to the top 2 with >70–95% confidence; cross-validated on alloys and 2D materials.

### 2019 · Vecsei et al. — Neural network classification of crystal symmetries

- **Title:** Neural network based classification of crystal symmetries from x-ray diffraction patterns
- **Authors:** Pascal Marc Vecsei, Kenny Choo; senior: Titus Neupert — University of Zürich
- **Venue:** *Phys. Rev. B* 99, 245120 (2019)
- **Paper:** <https://journals.aps.org/prb/abstract/10.1103/PhysRevB.99.245120>
- **TL;DR:** Dense vs. CNN comparison on simulated and RRUFF experimental data — 54% (dense) vs. 42% (CNN) space-group accuracy on RRUFF.

### 2019 · Liu et al. — CNN space-group prediction from atomic PDF

- **Title:** Using a machine learning approach to determine the space group of a structure from the atomic pair distribution function
- **Authors:** Chia-Hao (Timothy) Liu, Yunzhe Tao, Daniel Hsu, Qiang Du; senior: Simon J. L. Billinge — Columbia University
- **Venue:** *Acta Crystallographica A* 75, 633–643 (2019)
- **Paper:** <https://journals.iucr.org/a/issues/2019/04/00/ae5079/>
- **TL;DR:** PDF-based (not direct PXRD) CNN; 91.9% top-6 space-group accuracy on experimental PDF inputs.

### 2020 · Suzuki et al. — Interpretable XGBoost for symmetry prediction

- **Title:** Symmetry prediction and knowledge discovery from X-ray diffraction patterns using an interpretable machine learning approach
- **Authors:** Yuta Suzuki et al. — Toyota Motor Corp. / RIKEN
- **Venue:** *Scientific Reports* 10, 21790 (2020)
- **Paper:** <https://www.nature.com/articles/s41598-020-77474-4>
- **TL;DR:** Tree-ensemble (XGBoost) with feature attribution; ~90% crystal-system, ~88% Top-5 space-group accuracy with extraction of human-interpretable rules.

### 2021 · Chitturi et al. — 1D-CNN lattice parameter prediction (DeepLPnet)

- **Title:** Automated prediction of lattice parameters from X-ray powder diffraction patterns
- **Authors:** Sathya R. Chitturi (Stanford/SLAC), Daniel Ratner, Richard C. Walroth, Vivek Thampy, Evan J. Reed, Mike Dunne, Christopher J. Tassone; senior: Kevin H. Stone — SLAC
- **Venue:** *J. Appl. Crystallogr.* 54, 1799–1810 (2021)
- **Paper:** <https://journals.iucr.org/j/issues/2021/06/00/vb5020/>
- **Code:** <https://github.com/sathya-chitturi/DeepLPnet>
- **TL;DR:** Per-crystal-system 1D-CNNs regress a/b/c lattice parameters from raw PXRD; ~10% MAPE corresponds to 100–1000× search-space reduction; trained on ICSD + CSD (~1 M structures).

### 2023 · Salgado et al. — Big-data symmetry CNN (SPGNet)

- **Title:** Automated classification of big X-ray diffraction data using deep learning models
- **Authors:** Jerardo E. Salgado, Samuel Lerman, Zhaotong Du, Chenliang Xu; senior: Niaz Abdolrahim, Jason Hattrick-Simpers — University of Toronto / Rochester
- **Venue:** *npj Computational Materials* 9, 214 (2023)
- **Paper:** <https://www.nature.com/articles/s41524-023-01164-8>
- **TL;DR:** 7-way crystal-system + 230-way space-group CNN with augmented synthetic data approximating real experimental noise.

### 2023 · Schopmans et al. — Synthetic crystals → ICSD symmetry extraction

- **Title:** Neural networks trained on synthetically generated crystals can extract structural information from ICSD powder X-ray diffractograms
- **Authors:** Henrik Schopmans, Patrick Reiser; senior: Pascal Friederich — KIT (AiMat group)
- **Venue:** *Digital Discovery* 2, 1414 (2023)
- **Paper:** <https://pubs.rsc.org/en/content/articlelanding/2023/dd/d3dd00071k>
- **Code:** <https://github.com/aimat-lab/ML4pXRDs>
- **TL;DR:** Models trained on purely synthetic randomly-generated crystals surpass models trained on ICSD itself for space-group classification on ICSD test patterns.

### 2026 · AlphaDiffract — 1D ConvNeXt for lattice & symmetry determination

- **Title:** AlphaDiffract: Automated Crystallographic Analysis of Powder X-ray Diffraction Data
- **Authors:** Nina Andrejevic, Ming Du, Hemant Sharma, James P. Horwath, Aileen Luo, Xiangyu Yin, Michael Prince, Brian H. Toby, Mathew J. Cherukara — Argonne National Laboratory
- **Venue:** arXiv:2603.23367 (Mar 2026)
- **Paper:** <https://arxiv.org/abs/2603.23367>
- **TL;DR:** 1D ConvNeXt backbone on 8192-bin PXRD vectors jointly predicts crystal system, space group, and lattice parameters; trained on GSAS-II-simulated patterns from NIST/ICSD structures; intended as a preprocessing stage for automated Rietveld.

---

## Multi-phase Decomposition & Rietveld Refinement

### 2018 · Stanev et al. — Unsupervised NMF phase mapping

- **Title:** Unsupervised phase mapping of X-ray diffraction data by nonnegative matrix factorization integrated with custom clustering
- **Authors:** Valentin Stanev (UMD / NIST), Velimir V. Vesselinov (LANL), A. Gilad Kusne (NIST / UMD), Graham Antoszewski, Ichiro Takeuchi; senior: Boian S. Alexandrov (LANL)
- **Venue:** *npj Computational Materials* 4, 43 (2018); arXiv:1802.07307
- **Paper:** <https://www.nature.com/articles/s41524-018-0099-2> · <https://arxiv.org/abs/1802.07307>
- **Multi-phase strategy:** *Joint matrix factorization across a library of patterns.*
- **TL;DR:** Stacks N PXRD patterns from a composition library into a non-negative matrix and decomposes it into K shared end-member basis patterns and per-sample mixture weights via NMF, with custom clustering and cross-correlation to stabilize K and resolve peak shifts. Unsupervised and requires no candidate phase list, but assumes the same K end-members are shared across the library.

### 2021 · Szymanski et al. — Probabilistic multi-phase decomposition (XRD-AutoAnalyzer)

- **Title:** Probabilistic deep learning approach to automate the interpretation of multi-phase diffraction spectra
- **Authors:** Nathan J. Szymanski, Christopher J. Bartel, Yan Zeng, Qingsong Tu; senior: Gerbrand Ceder — UC Berkeley / LBNL
- **Venue:** *Chemistry of Materials* 33, 4204–4215 (2021); arXiv:2103.16664
- **Paper:** <https://pubs.acs.org/doi/10.1021/acs.chemmater.1c01071> · <https://arxiv.org/abs/2103.16664>
- **Code:** <https://github.com/njszym/XRD-AutoAnalyzer>
- **Multi-phase strategy:** *Sequential identify-and-subtract with branching tree search.*
- **TL;DR:** Ensemble CNN trained on a fixed reference set scores the most likely single phase, subtracts its simulated contribution from the pattern, and recurses on the residual; branching keeps several hypothesis paths to mitigate error accumulation. Handles up to ~4 phases per pattern with quantitative weight fractions and per-call uncertainty, but is bound to the reference phase set used at training time.

### 2022 · BraggNN — Fast Bragg-peak localization with deep learning

- **Title:** *BraggNN*: fast X-ray Bragg peak analysis using deep learning
- **Authors:** Zhengchun Liu, Hemant Sharma, Jun-Sang Park, Peter Kenesei, Antonino Miceli, Jonathan Almer, Rajkumar Kettimuthu, Ian Foster — Argonne National Laboratory
- **Venue:** *IUCrJ* 9, 104–113 (2022)
- **Paper:** <https://journals.iucr.org/m/issues/2022/01/00/fs5198/>
- **Code:** <https://github.com/lzhengchun/BraggNN>
- **Multi-phase strategy:** *Per-peak regression (building block, not full decomposition).*
- **TL;DR:** Regression DNN that replaces pseudo-Voigt peak fitting at the level of individual Bragg spots in high-energy diffraction microscopy (HEDM). Orders of magnitude faster than conventional per-peak fitting with comparable precision; used as a front-end localizer feeding downstream phase / grain analysis rather than a pattern-level multi-phase decomposer.

### 2025 · Spotlight — Automated global optimization for Rietveld

- **Title:** Spotlight: efficient automated global optimization in Rietveld analysis of diffraction data
- **Authors:** C. M. Biwer, Z. Feng, D. Finstad, M. McDonnell, M. Knezevic, M. McKerns, D. J. Savage, S. C. Vogel — LANL (X Computational Physics / Materials Science & Tech.), with UNH, Syracuse, ORNL and the UQ Foundation
- **Venue:** *Scientific Reports* 15, 8358 (2025)
- **Paper:** <https://www.nature.com/articles/s41598-025-92452-4>
- **Multi-phase strategy:** *Known candidate phase set; parallel global optimization across a parametric series.*
- **TL;DR:** Python wrapper over MAUD / GSAS / GSAS-II that drives Rietveld refinement of multi-phase samples through an ensemble of optimizers running in parallel on HPC, with an iteratively learned surrogate of the refinement response surface. Targets parametric series (temperature, composition, in-situ time) where simple sequential refinement or DB-matching diverges as phase transformations occur; demonstrated on U–Mo, Ti–6Al–4V, Al₂O₃ and PbSO₄.

### 2026 · RAPID — Rietveld Analysis Pipeline with Intelligent Deep Learning

- **Title:** Automation of Rietveld refinement through machine learning
- **Authors:** Suk Jin Mun (IBS-CINAP / Sungkyunkwan University), Yoonsoo Nam (Rudolf Peierls Centre for Theoretical Physics, University of Oxford); senior: Sungkyun Choi (IBS-CINAP / SKKU / IBS-CVQS)
- **Venue:** *Journal of Applied Crystallography* 59, 564–577 (2026); accepted Feb 2026
- **Paper:** <https://journals.iucr.org/j/issues/2026/02/00/yt5169/> · open-access mirror: <https://pmc.ncbi.nlm.nih.gov/articles/PMC13060465/>
- **Code:** <https://github.com/DataForgeSci/RAPID>
- **Multi-phase strategy:** *Single-phase only; included as Rietveld-automation baseline.*
- **TL;DR:** Assumes the crystalline phase is already known and trains one CNN per compound on FullProf-simulated patterns to predict structural and profile parameters (lattice, B_iso, scale, U/V/W, zero shift) in a single forward pass. Validated on CeO₂, Tb₂BaCoO₅, PbSO₄ and monoclinic BaLu₆(Ge₂O₇)₂(Ge₃O₁₀) with R-factors matching manual refinement; the authors note that extension to multi-phase mixtures remains future work.

### 2026 · XDecomposer — Prior-free set decomposition for multiphase XRD

- **Title:** XDecomposer: Learning Prior-Free Set Decomposition for Multiphase X-ray Diffraction
- **Authors:** Hanyu Gao, Bin Cao — co-first; Yunyue Su; Tong-Yi Zhang, Qiang Liu (CASIA, HKUST(GZ))
- **Venue:** arXiv:2605.05866 (May 2026)
- **Paper:** <https://arxiv.org/abs/2605.05866>
- **Code:** <https://github.com/Licht0812/XDecomposer>
- **Multi-phase strategy:** *Permutation-invariant set prediction (one-shot blind source separation).*
- **TL;DR:** Reformulates multiphase PXRD analysis as one-dimensional blind source separation (BSS): a pretrained global bottleneck encodes peak structure, then a fixed-size set of K_max output slots jointly predicts component patterns + mixture proportions in a single forward pass, trained with permutation-invariant separation loss, slot-activity supervision and mixture-consistency regularization. Avoids the error accumulation of sequential identify-and-subtract and does not require a candidate phase list, structural templates, or the number of phases.

---

## Autonomous / In-situ XRD Analysis

### 2021 · XCA — Crystallography Companion Agent

- **Title:** Crystallography companion agent for high-throughput materials discovery
- **Authors:** Phillip M. Maffettone, Lars Banko, Peng Cui, Yury Lysogorskiy, Marc A. Little, Daniel Olds, Alfred Ludwig, Andrew I. Cooper — Brookhaven National Laboratory (NSLS-II), Ruhr-Universität Bochum, Univ. of Liverpool
- **Venue:** *Nature Computational Science* 1, 290–297 (2021)
- **Paper:** <https://www.nature.com/articles/s43588-021-00059-2>
- **Code:** <https://github.com/maffettone/xca> · examples: <https://github.com/bnl/pub-Maffettone_2020_08>
- **TL;DR:** Pseudo-unsupervised CNN ensemble trained on fully synthetic, physics-informed diffraction; provides real-time, probabilistic phase identification during high-throughput beam-time experiments.

### 2023 · Szymanski et al. — Adaptively driven XRD (Adaptive-XRD)

- **Title:** Adaptively driven X-ray diffraction guided by machine learning for autonomous phase identification
- **Authors:** Nathan J. Szymanski, Christopher J. Bartel, Yan Zeng, et al.; senior: Gerbrand Ceder — UC Berkeley / LBNL
- **Venue:** *npj Computational Materials* 9, 31 (2023)
- **Paper:** <https://www.nature.com/articles/s41524-023-00984-y>
- **Code:** <https://github.com/njszym/Adaptive-XRD>
- **TL;DR:** Ensemble CNN predicts phase mixtures with uncertainty; an adaptive policy decides the next 2θ ranges to measure, reducing total measurement time on transient or dilute samples.

### 2023 · Banko et al. — Self-supervised PXRD classification of phase transitions

- **Title:** Application of self-supervised approaches to the classification of X-ray diffraction spectra during phase transitions
- **Authors:** Lars Banko, Phillip M. Maffettone, Dennis Naujoks, Daniel Olds, Alfred Ludwig — Ruhr-Universität Bochum, BNL, DESY
- **Venue:** *Scientific Reports* 13, 9173 (2023)
- **Paper:** <https://www.nature.com/articles/s41598-023-36456-y>
- **TL;DR:** Self-supervised relational reasoning + contrastive learning to classify 1D PXRD spectra of in-situ phase transitions recorded at PETRA III (P02.2).

### 2023 · A-Lab — Autonomous materials laboratory closing the synthesis loop

- **Title:** An autonomous laboratory for the accelerated synthesis of novel materials
- **Authors:** Nathan J. Szymanski, Bernardus Rendy, Yuxing Fei, et al.; senior: Gerbrand Ceder — UC Berkeley / LBNL
- **Venue:** *Nature* 624, 86–91 (2023)
- **Paper:** <https://www.nature.com/articles/s41586-023-06734-w>
- **TL;DR:** End-to-end autonomous lab in which ML-based PXRD analysis closes the loop between synthesis attempts and recipe revision; reports 41 successful syntheses in 17 days.

---

## Datasets & Benchmarks

Listed chronologically. *(Reference databases (RRUFF, COD, Materials Project, ICSD, JARVIS-DFT) are grouped at the end for reference.)*

### 2015 · RRUFF — Empirical mineral XRD / Raman / IR database

- **Title:** The power of databases: the RRUFF project
- **Authors:** Barbara Lafuente, Robert T. Downs, Hexiong Yang, Nate Stone — University of Arizona
- **Venue:** *Highlights in Mineralogical Crystallography*, De Gruyter (2015)
- **Paper:** <https://www.degruyter.com/document/doi/10.1515/9783110417104-003>
- **Portal:** <https://rruff.info/>
- **TL;DR:** Curated experimental XRD / Raman / IR / chemistry database for minerals; the most widely used experimental benchmark for PXRD ML methods.

### 2023 · ML4pXRDs — Synthetic-crystal training pipeline

- **Authors:** Schopmans et al. — KIT (AiMat group)
- **Code:** <https://github.com/aimat-lab/ML4pXRDs>
- **TL;DR:** Reference pipeline for training symmetry classifiers from synthetically generated random crystals and evaluating against ICSD patterns (companion to Schopmans 2023).

### 2024 · CHILI-3K / CHILI-100K — Nanomaterials graph + scattering dataset

- **Title:** CHILI: Chemically-Informed Large-scale Inorganic Nanomaterials Dataset for Advancing Graph Machine Learning
- **Authors:** Ulrik Friis-Jensen, Frederik L. Johansen, Andy S. Anker, Erik B. Dam, Kirsten M. Ø. Jensen, Raghavendra Selvan — University of Copenhagen
- **Venue:** *KDD* 2024; arXiv:2402.13221
- **Paper:** <https://arxiv.org/abs/2402.13221>
- **Code/Data:** <https://github.com/UlrikFriisJensen/CHILI>
- **TL;DR:** Nanomaterials graph dataset with 11 classification (atom, crystal system, space group) and 8 regression tasks including PXRD, ND, SAXS, SANS, xPDF, nPDF.

### 2025 · SimXRD-4M — Large simulated PXRD benchmark

- **Title:** SimXRD-4M: Big Simulated X-ray Diffraction Data and Crystal Symmetry Classification Benchmark
- **Authors:** Bin Cao et al. — HKUST(GZ)
- **Venue:** *ICLR* 2025; arXiv:2406.15469
- **Paper:** <https://openreview.net/forum?id=mkuB677eMM> · <https://arxiv.org/abs/2406.15469>
- **Code/Data:** <https://github.com/Bin-Cao/SimXRD>
- **TL;DR:** 4,065,346 PXRD patterns from 119,569 distinct structures simulated under varying grain size, orientation, internal stress, inelastic scattering and thermal vibration; benchmarks 21 sequence models.

### 2025 · SIMPOD — COD-based 1D and 2D PXRD benchmark

- **Title:** A new benchmark for machine learning applied to powder X-ray diffraction
- **Authors:** Sergio Rincón, et al.; senior: Pablo Arbeláez — Universidad de los Andes
- **Venue:** *Scientific Data* 12 (2025)
- **Paper:** <https://www.nature.com/articles/s41597-025-05534-3>
- **Code/Data:** <https://github.com/BCV-Uniandes/SIMPOD>
- **TL;DR:** 467,861 simulated PXRD patterns sourced from COD in both 1D-vector and 2D radial-image format.

### 2025/2026 · opXRD — Open experimental PXRD database

- **Title:** opXRD: Open Experimental Powder X-Ray Diffraction Database
- **Authors:** Daniel Hollarek, Henrik Schopmans, Jona Östreicher, Jonas Teufel, et al.; senior: Pascal Friederich — KIT (AiMat group), with 18 contributing labs
- **Venue:** *Advanced Intelligent Discovery* 2, e202500044 (2026); arXiv:2503.05577
- **Paper:** <https://arxiv.org/abs/2503.05577>
- **Portal:** <https://xrd.aimat.science/> · <https://zenodo.org/records/15298026>
- **TL;DR:** ~92 k labeled + unlabeled experimental PXRD patterns aggregated from multiple high-throughput labs, covering many materials classes.

### 2025 · CrystDB / HKUST-CrystDB — Curated crystal databases for XRD / CSP / CPP

- **Title:** CrystDB / HKUST-CrystDB (Hugging Face datasets)
- **Maintainer:** Bin Cao — HKUST(GZ); companion data to SimXRD-4M and XQueryer.
- **Data:**
  - CrystDB — all thermodynamically stable structures from Materials Project (MP-2024.1, up to Jan 2024): <https://huggingface.co/datasets/caobin/CrystDB>
  - HKUST-CrystDB — 718,725 entries aggregated for generative CSP: <https://huggingface.co/datasets/caobin/HKUST-CrystDB>
- **TL;DR:** Two ASE-readable crystal databases targeted at XRD-based identification, crystal-property prediction (CPP), and crystal-structure prediction (CSP); each row exposes atomic species, fractional coordinates, lattice, and space group.

### Reference structure databases (used by virtually every entry above)

- **Materials Project / MP-20 / MP-PXRD** — <https://next-gen.materialsproject.org/> · MP-20: <https://github.com/txie-93/cdvae/tree/main/data/mp_20> · MP-20-PXRD: <https://github.com/gabeguo/cdvae_xrd>
- **Crystallography Open Database (COD)** — <http://www.crystallography.net/cod/>  (~500 k CIFs; free alternative to ICSD).
- **JARVIS-DFT XRD** — <https://jarvis.nist.gov/jarvisxrd/>  (simulated XRD over JARVIS-DFT structures; used by DiffractGPT).
- **ICSD** — <https://icsd.fiz-karlsruhe.de/> (licensed inorganic structures; common training source for Park 2017, Lee 2020, Schopmans 2023).
- **CSD** — <https://www.ccdc.cam.ac.uk/structures/> (licensed organic / metal-organic structures; used by DeepLPnet 2021 alongside ICSD).
- **PDF-4+ / ICDD PDF** — <https://www.icdd.com/> (commercial Powder Diffraction File; experimental benchmark for Crystalyze, XRDSol, RealPXRD-Solver).

---

## Simulation, Refinement, and Utility Tools

- **pymatgen XRDCalculator** — Python simulation of PXRD from CIF. <https://pymatgen.org/pymatgen.analysis.diffraction.html>
- **GSAS-II** — Open-source Rietveld refinement and structure determination (used by PXRDGen, RAPID, AlphaDiffract, etc.). Home: <https://advancedphotonsource.github.io/GSAS-II-tutorials/> · source: <https://github.com/AdvancedPhotonSource/GSAS-II> · docs: <https://gsas-ii.readthedocs.io/>
- **FullProf** — Classical Rietveld suite. <https://www.ill.eu/sites/fullprof/>
- **TOPAS-Academic** — Macro-language Rietveld engine. <http://www.topas-academic.net/>
- **diffpy-cmi / PDFfit2** — Pair distribution function modeling. <https://www.diffpy.org/>
- **xrdpattern** — Python package shipped with opXRD for unified PXRD I/O and curation. <https://github.com/aimat-lab/xrdpattern>
- **pysimxrd** — Domain-specific Python simulator behind SimXRD-4M; models peak broadening, lattice perturbation, instrumental and orientation effects. <https://pypi.org/project/pysimxrd/> · source: <https://github.com/Bin-Cao/SimXRD>
- **PyWPEM / PyXplore** — Whole Powder-pattern Expectation-Maximization (WPEM) toolkit by Bin Cao et al. for physics-constrained decomposition, quantitative analysis, and AI-assisted Rietveld-style refinement; supports XRD, XPS and EXAFS. PyPI: <https://pypi.org/project/PyXplore/> · source: <https://github.com/Bin-Cao/PyWPEM> · preprint: <https://arxiv.org/abs/2602.16372>
- **AtomGPT / DiffractGPT inference** — <https://github.com/usnistgov/atomgpt>

---

## Reviews & Surveys

Reviews directly focused on PXRD-driven analysis and structure determination:

- **X-ray Diffraction Data Analysis by Machine Learning Methods — A Review** — Surakhi et al., *Applied Sciences* 13, 9992 (2023). <https://www.mdpi.com/2076-3417/13/17/9992>
- **Identifying crystal structures beyond known prototypes from X-ray powder diffraction spectra** — *Phys. Rev. Materials* 8, 103801 (2024). <https://journals.aps.org/prmaterials/abstract/10.1103/PhysRevMaterials.8.103801>
- **Machine Learning in X-ray Scattering for Materials Discovery and Characterization** — ChemRxiv preprint (Dec 2024). <https://chemrxiv.org/engage/chemrxiv/article-details/67624f34fa469535b9f25aea>
- **End-to-End Crystal Structure Prediction from Powder X-Ray Diffraction** — Chinese-language review on themoonlight.io that motivated this repo. <https://www.themoonlight.io/zh/review/end-to-end-crystal-structure-prediction-from-powder-x-ray-diffraction>

Broader crystal-CSP / generative reviews (context for the methods above):

- **Machine learning assisted crystal structure prediction made simple** — *J. Mater. Inf.* (2024). <https://www.oaepublish.com/articles/jmi.2024.18>
- **Generative AI for crystal structures: a review** — *npj Computational Materials* (2025). <https://www.nature.com/articles/s41524-025-01881-2>
- **A Comprehensive Review of Machine-Learning Approaches for Crystal Structure/Property Prediction** — *Crystals* 15, 925 (2025). <https://www.mdpi.com/2073-4352/15/11/925>

---

## Related Curated Lists

- [awesome-materials-informatics](https://github.com/tilde-lab/awesome-materials-informatics) — broad materials-informatics list.
- [awesome-self-supervised-learning-for-graphs](https://github.com/LirongWu/awesome-graph-self-supervised-learning) — relevant for crystal-graph encoders.
- [awesome-generative-models-for-materials](https://github.com/usnistgov/jarvis_leaderboard) (JARVIS Leaderboard) — leaderboard tracking many of the generative models above.

---

## Contributing

**Additions, corrections, and translations are warmly welcomed — 欢迎补充、纠正与翻译！**

There are three easy ways to contribute:

- **[Open an issue](https://github.com/Bin-Cao/awesome-xrd2crystal/issues/new)** — paste the paper title, arXiv id or GitHub link and (if possible) the section it belongs in.
- **Open a Pull Request** — edit `README.md` following the format described in [CONTRIBUTING.md](CONTRIBUTING.md).
- **Email the maintainer** — for bulk additions (e.g. a whole research direction we missed).

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full entry-format template, chronology rules, and link conventions.

---

## Contributors

Thanks goes to these wonderful people who have contributed papers, corrections, and improvements to this list — 感谢以下贡献者对本仓库的补充、纠正与维护：

<a href="https://github.com/Bin-Cao/awesome-xrd2crystal/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=Bin-Cao/awesome-xrd2crystal" alt="Contributors" />
</a>

<sub>*Avatars are rendered automatically by [contrib.rocks](https://contrib.rocks) from the GitHub contributor graph.*</sub>
