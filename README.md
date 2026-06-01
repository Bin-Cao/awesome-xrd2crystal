# Awesome XRD → Crystal [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated collection of papers, code, and datasets on **(powder) X-ray diffraction (XRD/PXRD) → crystal structure** identification, prediction, generation, refinement, and related machine-learning topics.

The PXRD → structure problem is an ill-posed inverse problem: many candidate structures can produce similar 1D patterns, and experimental profiles contain instrumental broadening, finite-size effects, texture/preferred orientation, background, impurity phases, and peak overlap. Recent deep-learning work tackles the problem from multiple angles — direct PXRD-to-CIF generation, diffusion/flow-based coordinate sampling, language-model generation of CIF text, lattice/symmetry classification, retrieval/search-match, and multi-phase decomposition.

Contributions are welcome — see [Contributing](#contributing).

---

## Contents

- [End-to-End PXRD → Crystal Structure (Generative)](#end-to-end-pxrd--crystal-structure-generative)
- [Phase Identification from XRD](#phase-identification-from-xrd)
- [Crystal System / Space Group / Lattice Prediction from XRD](#crystal-system--space-group--lattice-prediction-from-xrd)
- [Retrieval / Search-Match](#retrieval--search-match)
- [Multi-phase Decomposition & Rietveld Refinement](#multi-phase-decomposition--rietveld-refinement)
- [Autonomous / In-situ XRD Analysis](#autonomous--in-situ-xrd-analysis)
- [Foundational Crystal Generative Models (no XRD conditioning)](#foundational-crystal-generative-models-no-xrd-conditioning)
- [Datasets & Benchmarks](#datasets--benchmarks)
- [Simulation, Refinement, and Utility Tools](#simulation-refinement-and-utility-tools)
- [Reviews & Surveys](#reviews--surveys)
- [Related Curated Lists](#related-curated-lists)
- [Contributing](#contributing)

---

## End-to-End PXRD → Crystal Structure (Generative)

Methods that take a PXRD pattern (optionally + composition / lattice) and output a full 3D crystal structure (atomic positions + lattice, typically as CIF).

### XtalNet — Contrastive PXRD-Crystal Pretraining + Conditional Diffusion (2024)

- **Title:** End-to-End Crystal Structure Prediction from Powder X-Ray Diffraction
- **First author / affiliation:** Qingsi Lai — DP Technology, Beijing (collab. Peking Univ., Xiamen Univ., AI for Science Institute)
- **Venue:** *Advanced Science* (2025); arXiv:2401.03862
- **Paper:** <https://arxiv.org/abs/2401.03862> · <https://onlinelibrary.wiley.com/doi/10.1002/advs.202410722>
- **Code:** <https://github.com/dptech-corp/XtalNet>
- **Data / artifact:** <https://zenodo.org/records/13629658>
- **Highlights:** First end-to-end equivariant generative model for PXRD → MOF-scale structures (≤400 atoms/cell). Top-10 match rate 90.2% on hMOF-100, 79% on hMOF-400.

### PXRDnet — SE(3)-Equivariant Score-Based Diffusion (2025)

- **Title:** Ab initio structure solutions from nanocrystalline powder diffraction data via diffusion models
- **First author / affiliation:** Gabe Guo — Columbia University (collab. Stanford, Hod Lipson lab)
- **Venue:** *Nature Materials* 24, 1726–1734 (2025); arXiv:2406.10796
- **Paper:** <https://www.nature.com/articles/s41563-025-02220-y> · <https://arxiv.org/abs/2406.10796>
- **Code:** <https://github.com/gabeguo/cdvae_xrd>
- **Highlights:** Score-based generative model conditioned on finite-size-broadened PXRD + formula; works on simulated nanocrystals as small as 10 Å and real experimental patterns across all seven crystal systems; median RMSD ≤0.11 Å on MP-20-PXRD.

### Crystalyze — XRD CNN + CDVAE (2024)

- **Title:** Crystal Structure Determination from Powder Diffraction Patterns with Generative Machine Learning
- **First author / affiliation:** Eric A. Riesel — MIT (Freedman group); co-led with Tsach Mackey (Yale); senior authors Danna E. Freedman (MIT), Jure Leskovec (Stanford)
- **Venue:** *Journal of the American Chemical Society* 146, 30340–30348 (2024)
- **Paper:** <https://pubs.acs.org/doi/10.1021/jacs.4c10244>
- **Code:** <https://github.com/ML-PXRD/Crystalyze>
- **Highlights:** Couples XRD representation learning with CDVAE; reported ~42% match rate on experimental and ~67% on simulated patterns; solved previously-unsolved Powder Diffraction File entries.


### PXRDGen — Pretrained XRD Encoder + Diffusion/Flow + Auto-Rietveld (2025)

- **Title:** Powder diffraction crystal structure determination using generative models
- **First authors / affiliation:** Qi Li (Institute of Physics, CAS), Rui Jiao (Tsinghua); senior authors Wenbing Huang (Renmin Univ.), Shifeng Jin (IoP CAS)
- **Venue:** *Nature Communications* 16, 7428 (2025); arXiv:2409.04727
- **Paper:** <https://www.nature.com/articles/s41467-025-62708-8> · <https://arxiv.org/abs/2409.04727>
- **Code / artifact:** <https://codeocean.com/capsule/2196660/> (DOI: 10.24433/CO.6347299.v1)
- **Highlights:** XRD encoder pretrained by contrastive learning + diffusion/flow-based generator + integrated Rietveld refinement; 82% valid compounds from a single sample on MP-20, 96% within 20 samples.

### deCIFer — Autoregressive Transformer over CIF tokens (2025)

- **Title:** deCIFer: Crystal Structure Prediction from Powder Diffraction Data using Autoregressive Language Models
- **First author / affiliation:** Frederik Lizak Johansen — University of Copenhagen (Dept. of Computer Science)
- **Venue:** OpenReview / TMLR 2025; arXiv:2502.02189
- **Paper:** <https://arxiv.org/abs/2502.02189> · <https://openreview.net/forum?id=LftFQ35l47>
- **Code:** <https://github.com/FrederikLizakJohansen/deCIFer>
- **Highlights:** Transformer that directly generates CIF text conditioned on PXRD embeddings; ~94% structure match in author setting; trained on NOMA1 / CHILI-100K-derived data.

### DiffractGPT / AtomGPT — Generative Pretrained Transformer for XRD → Structure (2025)

- **Title:** DiffractGPT: Atomic Structure Determination from X-ray Diffraction Patterns Using a Generative Pretrained Transformer
- **Author / affiliation:** Kamal Choudhary — NIST, Material Measurement Laboratory (also Johns Hopkins)
- **Venue:** *Journal of Physical Chemistry Letters* (2025); arXiv:2508.08349
- **Paper:** <https://pubs.acs.org/doi/10.1021/acs.jpclett.4c03137> · <https://arxiv.org/abs/2508.08349>
- **Code:** <https://github.com/usnistgov/atomgpt> · <https://github.com/usnistgov/diffractgpt>
- **Highlights:** Mistral-style LLM fine-tuned on JARVIS-DFT simulated PXRD to emit CIF-like crystal descriptions; lattice MAE ~0.17–0.27 Å for a/b/c (DGPT-formula).

### Uni-3DAR — Unified 3D Autoregressive Generation (2025)

- **Title:** Uni-3DAR: Unified 3D Generation and Understanding via Autoregression on Compressed Spatial Tokens
- **First author / affiliation:** Shuqi Lu — DP Technology (collab. Peking Univ., AI for Science Institute)
- **Venue:** arXiv:2503.16278 (2025)
- **Paper:** <https://arxiv.org/abs/2503.16278> · <https://uni-3dar.github.io/>
- **Code:** <https://github.com/dptech-corp/Uni-3DAR> · <https://huggingface.co/dptech/Uni-3DAR>
- **Highlights:** Octree-based hierarchical tokenization + autoregressive 3D modeling; PXRD-conditioned CSP on MP-20: 75.08% match rate, RMSE 0.0276.

### XRDSol — Equivariant GNN Diffusion Solver (2026)

- **Title:** Equivariant diffusion solution for inorganic crystal structure determination from powder X-ray diffraction data
- **Affiliation:** ai4mat group (Zhejiang Univ. & collaborators)
- **Venue:** *Nature Communications* (in press, 2026)
- **Paper:** <https://www.nature.com/articles/s41467-026-70035-9>
- **Code / data:** <https://github.com/ai4mat-zhu/XRDSol>
- **Highlights:** Conditions on stoichiometry + unit cell + PXRD; ~82.3% success on MP-20, 81.6% on ICDD-20 experimental benchmark; ~0.6 s per solution on one GPU.

### RealPXRD-Solver — Generative Model for Experimental PXRD with Augmentation (2026)

- **Title:** Experimental Powder X-ray Diffraction Crystal Structure Determination with RealPXRD-Solver
- **First author / affiliation:** Qi Li — Institute of Physics, CAS (with DP Technology, Tsinghua, Renmin Univ., SJTU, AISI)
- **Venue:** arXiv:2603.00965 (Mar 2026)
- **Paper:** <https://arxiv.org/abs/2603.00965>
- **Code:** <https://github.com/liqi-529/RealPXRD-Solver>
- **Highlights:** Universal encoder of d-spacing–intensity fingerprints trained on 6,250,238 theoretical structures with experiment-mimicking augmentations; supports lattice-conditioned and lattice-free inference. 98.3% Top-20 on 10k-structure theoretical benchmark; 77.9% / 91.9% Top-1/Top-20 on CNRS, 78.8% / 92.9% on RRUFF; solved 39 previously-unreported PDF entries.

### CrystalNet — Coordinate-Based VAE for Electron Density (2024)

- **Title:** Towards end-to-end structure determination from X-ray diffraction data using deep learning
- **First author / affiliation:** Gabe Guo — Columbia University (Hod Lipson lab)
- **Venue:** *npj Computational Materials* 10, 209 (2024); arXiv:2312.15136
- **Paper:** <https://www.nature.com/articles/s41524-024-01401-8> · <https://arxiv.org/abs/2312.15136>
- **Code:** <https://github.com/gabeguo/deep-crystallography-public>
- **Highlights:** Conditional implicit neural representation (Cartesian-mapped electron density) from PXRD + composition; up to 93.4% SSIM on cubic test cases, 74.1% average on trigonal.

### Hybrid Ab-initio PXRD Solver (2026)

- **Title:** Ab-initio Crystal Structure Determination from Powder X-Ray Diffraction
- **First author / affiliation:** Kaixiang Su — UNC Charlotte (with Osman Goni Ridwan, Hongfei Xue; senior: Qiang Zhu)
- **Venue:** arXiv:2605.24594 (May 2026)
- **Paper:** <https://arxiv.org/abs/2605.24594>
- **Highlights:** Hierarchical hybrid framework: (1) discrete selection of space group / unit cell / Wyckoff site combinations, (2) continuous optimization of atomic coordinates. Combines AI-based peak profile analysis, density estimation and energy minimization with physics-informed constraints to overcome limits of purely data-driven solvers.

### XQueryer — 1.03B-Parameter Transformer Identifier (2024)

- **Title:** XQueryer: An Intelligent Crystal Structure Identifier for Powder X-ray Diffraction
- **First author / affiliation:** Bin Cao — HKUST(GZ) / HKUST
- **Code:** <https://github.com/Bin-Cao/XQueryer>
- **Highlights:** 1.03B-parameter model integrated with diffractometers; provides high-fidelity simulation, an RRUFF↔MP ID matching utility, and an associated benchmarking repo (XqueryerBench).

### CrystaLLM-π — XRD-Conditioned CIF Language Model (2025)

- **Title:** CrystaLLM-π: Property- and PXRD-Conditioned Generation of Crystal Structures with a CIF Language Model
- **First author / affiliation:** UCL (C-Bone-UCL group); builds on CrystaLLM (Antunes et al., Univ. of Reading)
- **Code:** <https://github.com/C-Bone-UCL/CrystaLLM-2.0>
- **Original CrystaLLM:** <https://arxiv.org/abs/2307.04340> · <https://github.com/lantunes/CrystaLLM>
- **Highlights:** Extends the autoregressive CIF language model CrystaLLM with conditioning on bandgap, density, photovoltaic efficiency, and XRD patterns (`CrystaLLM-pi_COD-XRD`, `CrystaLLM-pi_Mattergen-XRD` checkpoints on Hugging Face).


---

## Phase Identification from XRD

Methods that, given a PXRD pattern, predict which known phase(s) it corresponds to (classification / multi-label / search).

### CNN Phase ID in Multiphase Inorganic Compounds (Lee et al., 2020)

- **Title:** A deep-learning technique for phase identification in multiphase inorganic compounds using synthetic XRD powder patterns
- **First author / affiliation:** Jin-Woong Lee — Sejong University (with Woon Bae Park; senior: Kee-Sun Sohn)
- **Venue:** *Nature Communications* 11, 86 (2020)
- **Paper:** <https://www.nature.com/articles/s41467-019-13749-3>
- **Highlights:** Trained a deep CNN on ~1.78M simulated PXRD patterns across the Sr-Li-Al-O quaternary; near-perfect phase identification on experimental multi-phase compounds.

### Data-driven XRD Protocol with Phase-Fraction Prediction (Lee et al., 2021)

- **Title:** A data-driven XRD analysis protocol for phase identification and phase-fraction prediction of multiphase inorganic compounds
- **First author / affiliation:** Jin-Woong Lee — Sejong University (senior: Kee-Sun Sohn)
- **Venue:** *Inorganic Chemistry Frontiers* 8, 2492 (2021)
- **Paper:** <https://pubs.rsc.org/en/content/articlelanding/2021/qi/d0qi01513j>
- **Highlights:** Extends the CNN protocol from phase identification to quantitative phase-fraction prediction.

### CPICANN — Convolutional Self-Attention Phase Identifier (2024)

- **Title:** Crystallographic phase identifier of a convolutional self-attention neural network (CPICANN) on powder diffraction patterns
- **First author / affiliation:** Shouyang Zhang — HKUST(GZ) (with Bin Cao; senior: Tong-Yi Zhang)
- **Venue:** *IUCrJ* 11, 634 (2024)
- **Paper:** <https://journals.iucr.org/m/issues/2024/04/00/lt5076/>
- **Code:** <https://github.com/WPEM/CPICANN>
- **Data:** <https://huggingface.co/datasets/caobin/datasetCPICANN>
- **Highlights:** Self-attention augmented CNN; whole-pattern phase identification across four benchmarks (varying background and noise levels).

### Fast & Interpretable XRD Classification via Data Augmentation (Oviedo et al., 2019)

- **Title:** Fast and interpretable classification of small X-ray diffraction datasets using data augmentation and deep neural networks
- **First author / affiliation:** Felipe Oviedo — MIT Photovoltaics Research Lab (collab. NIST)
- **Venue:** *npj Computational Materials* 5, 60 (2019)
- **Paper:** <https://www.nature.com/articles/s41524-019-0196-x>
- **Code:** <https://github.com/PV-Lab/autoXRD>
- **Highlights:** Demonstrates physics-informed augmentation for training deep CNNs on small experimental XRD datasets; introduces class-activation visualization for interpretability.

---

## Crystal System / Space Group / Lattice Prediction from XRD

### Park et al. — CNN for Crystal System / Extinction Group / Space Group (2017)

- **Title:** Classification of crystal structure using a convolutional neural network
- **First author / affiliation:** Woon Bae Park — Sejong University (senior: Kee-Sun Sohn)
- **Venue:** *IUCrJ* 4, 486–494 (2017)
- **Paper:** <https://journals.iucr.org/m/issues/2017/04/00/fc5018/index.html>
- **Highlights:** Early CNN study; ~150k synthetic PXRD patterns; 94.99% crystal system, 83.83% extinction group, 81.14% space group accuracy.

### Vecsei et al. — Neural Networks for Crystal Symmetries (2019)

- **Title:** Neural network based classification of crystal symmetries from x-ray diffraction patterns
- **First author / affiliation:** Pascal Marc Vecsei — University of Zürich (senior: Titus Neupert)
- **Venue:** *Physical Review B* 99, 245120 (2019)
- **Paper:** <https://journals.aps.org/prb/abstract/10.1103/PhysRevB.99.245120>
- **Highlights:** Compares CNN vs. dense network; 54% (dense) vs. 42% (CNN) accuracy on experimental RRUFF data.

### SPGNet / Salgado et al. — Big-Data Symmetry Classification (2023)

- **Title:** Automated classification of big X-ray diffraction data using deep learning models
- **First author / affiliation:** Jerardo E. Salgado — University of Toronto (senior: Jason Hattrick-Simpers)
- **Venue:** *npj Computational Materials* 9, 214 (2023)
- **Paper:** <https://www.nature.com/articles/s41524-023-01164-8>
- **Highlights:** 7-way crystal system + 230-way space group CNN with augmented synthetic data resembling real experimental noise.

### Schopmans et al. — Synthetic Crystals → ICSD Symmetry Extraction (2023)

- **Title:** Neural networks trained on synthetically generated crystals can extract structural information from ICSD powder X-ray diffractograms
- **First author / affiliation:** Henrik Schopmans — KIT (AiMat group, senior: Pascal Friederich)
- **Venue:** *Digital Discovery* 2, 1414 (2023)
- **Paper:** <https://pubs.rsc.org/en/content/articlelanding/2023/dd/d3dd00071k>
- **Highlights:** Shows that purely synthetic randomly-generated crystals can train ML models that surpass models trained on ICSD itself for space-group classification on ICSD-derived test data.

### Suzuki et al. — Interpretable ML for Symmetry Prediction (2020)

- **Title:** Symmetry prediction and knowledge discovery from X-ray diffraction patterns using an interpretable machine learning approach
- **First author / affiliation:** Yuta Suzuki — Toyota Motor Corp. / RIKEN
- **Venue:** *Scientific Reports* 10, 21790 (2020)
- **Paper:** <https://www.nature.com/articles/s41598-020-77474-4>
- **Highlights:** Tree-ensemble (XGBoost) approach with feature attribution; ~90% crystal-system, 88% top-5 space-group accuracy and extraction of human-interpretable rules.

### Liu et al. — CNN Space-Group Prediction from PDF (2019)

- **Title:** Using a machine learning approach to determine the space group of a structure from the atomic pair distribution function
- **First author / affiliation:** Chia-Hao (Timothy) Liu — Columbia University (senior: Simon J. L. Billinge)
- **Venue:** *Acta Crystallographica A* 75, 633–643 (2019)
- **Paper:** <https://journals.iucr.org/a/issues/2019/04/00/ae5079/>
- **Highlights:** PDF-based (not direct PXRD) CNN; 91.9% top-6 space-group accuracy; demonstrates utility on experimental PDF inputs.

---

## Retrieval / Search-Match

### Szymanski et al. — Beam-Time Search-Match with Multi-Phase ID (adaptiveXRD, 2023)

- **Title:** Adaptively driven X-ray diffraction guided by machine learning for autonomous phase identification
- **First author / affiliation:** Nathan J. Szymanski — UC Berkeley / LBNL (Ceder group)
- **Venue:** *npj Computational Materials* 9, 31 (2023)
- **Paper:** <https://www.nature.com/articles/s41524-023-00984-y>
- **Code:** <https://github.com/njszym/Adaptive-XRD>
- **Highlights:** Ensemble of CNNs predicts phase mixtures and uncertainty; adaptive sampling decides next 2θ ranges to measure, reducing required measurement time.

### Wang et al. — Interpretable CNN for One-to-One MOF XRD ID (2020)

- **Title:** Rapid Identification of X-ray Diffraction Patterns Based on Very Limited Data by Interpretable Convolutional Neural Networks
- **First author / affiliation:** Hong Wang — University of Missouri (senior: Jian Lin)
- **Venue:** *Journal of Chemical Information and Modeling* 60, 2004–2011 (2020)
- **Paper:** <https://pubs.acs.org/doi/10.1021/acs.jcim.0c00020> · arXiv: <https://arxiv.org/abs/1912.07750>
- **Highlights:** CNN trained on theoretical MOF XRD patterns augmented with noise from limited experiments; 96.7% top-5 identification accuracy with class-activation interpretation.

---

## Multi-phase Decomposition & Rietveld Refinement

### RAPID — Rietveld Analysis Pipeline with Intelligent Deep Learning (2025)

- **Title:** Automation of Rietveld refinement through machine learning
- **Venue:** *IUCrJ* (2025)
- **Paper:** <https://pmc.ncbi.nlm.nih.gov/articles/PMC13060465/>
- **Highlights:** CNN trained on GSAS-II-simulated patterns to initialize and drive Rietveld refinement; validated on CeO₂, Tb₂BaCoO₅ and PbSO₄.

### AlphaDiffract — Lattice & Symmetry Determination via 1D ConvNeXt (2026)

- **Title:** AlphaDiffract: A Unified Deep Learning Framework for Lattice and Symmetry Determination from Powder X-ray Diffraction
- **Venue:** arXiv:2603.23367 (2026)
- **Paper:** <https://arxiv.org/abs/2603.23367>
- **Highlights:** 1D ConvNeXt backbone over 8192-bin PXRD vectors; serves as preprocessing for automated Rietveld; trained on GSAS-II-simulated patterns from NIST/ICSD structures.

### Szymanski et al. — Multi-Phase Decomposition via Tree Search (2021)

- **Title:** Probabilistic deep learning approach to automate the interpretation of multi-phase diffraction spectra
- **First author / affiliation:** Nathan J. Szymanski — UC Berkeley / LBNL (Ceder group)
- **Venue:** *Chemistry of Materials* 33, 4204–4215 (2021)
- **Paper:** <https://pubs.acs.org/doi/10.1021/acs.chemmater.1c01071>
- **Code:** <https://github.com/njszym/XRD-AutoAnalyzer>
- **Highlights:** Iteratively identifies and subtracts phases, accommodating up to 4 components per pattern with quantitative weight-fraction estimates.


---

## Autonomous / In-situ XRD Analysis

### XCA — Crystallography Companion Agent (2021)

- **Title:** Crystallography companion agent for high-throughput materials discovery
- **First author / affiliation:** Phillip M. Maffettone — Brookhaven National Laboratory (NSLS-II)
- **Venue:** *Nature Computational Science* 1, 290–297 (2021)
- **Paper:** <https://www.nature.com/articles/s43588-021-00059-2>
- **Code:** <https://github.com/maffettone/xca> · examples: <https://github.com/bnl/pub-Maffettone_2020_08>
- **Highlights:** Pseudo-unsupervised ensemble trained on fully synthetic, physics-informed diffraction; provides real-time, probabilistic phase identification during high-throughput experiments.

### Szymanski et al. — Autonomous Materials Discovery with A-Lab (2023)

- **Title:** An autonomous laboratory for the accelerated synthesis of novel materials
- **First author / affiliation:** Nathan J. Szymanski — UC Berkeley / LBNL (Ceder group)
- **Venue:** *Nature* 624, 86–91 (2023)
- **Paper:** <https://www.nature.com/articles/s41586-023-06734-w>
- **Highlights:** End-to-end autonomous lab where ML-based PXRD analysis closes the loop between synthesis attempts and recipe revision.

### Banko et al. — Self-Supervised XRD Classification of Phase Transitions (2023)

- **Title:** Application of self-supervised approaches to the classification of X-ray diffraction spectra during phase transitions
- **First author / affiliation:** Lars Banko — Ruhr-Universität Bochum (collab. BNL, DESY)
- **Venue:** *Scientific Reports* 13, 9173 (2023)
- **Paper:** <https://www.nature.com/articles/s41598-023-36456-y>
- **Highlights:** Applies self-supervised relational reasoning and contrastive learning to 1D PXRD classification of in-situ phase transitions recorded at PETRA III (P02.2 beamline).

---

## Foundational Crystal Generative Models (no XRD conditioning)

These models do not consume XRD directly but underpin many XRD-conditional methods listed above (CDVAE, DiffCSP, MatterGen, etc.).

### CDVAE — Crystal Diffusion Variational Autoencoder (2022)

- **Title:** Crystal Diffusion Variational Autoencoder for Periodic Material Generation
- **First author / affiliation:** Tian Xie — MIT (with Hannes Stärk, Octavian Ganea); senior: Tommi Jaakkola, Regina Barzilay
- **Venue:** *ICLR* 2022
- **Paper:** <https://arxiv.org/abs/2110.06197>
- **Code:** <https://github.com/txie-93/cdvae>
- **Highlights:** Score-based generation of periodic crystal structures; backbone of Crystalyze and PXRDnet.

### DiffCSP / DiffCSP++ — Diffusion-based CSP (2023–2024)

- **Title:** Crystal Structure Prediction by Joint Equivariant Diffusion
- **First author / affiliation:** Rui Jiao — Tsinghua University
- **Venue:** *NeurIPS* 2023; ICLR 2024 (DiffCSP++)
- **Paper:** <https://arxiv.org/abs/2309.04475> · <https://arxiv.org/abs/2402.03992>
- **Code:** <https://github.com/jiaor17/DiffCSP> · <https://github.com/jiaor17/DiffCSP-PP>
- **Highlights:** Joint diffusion over fractional coordinates and lattice; DiffCSP++ adds symmetry constraints. Backbone of PXRDGen.

### MatterGen — Foundation Diffusion Model for Inorganic Crystals (2025)

- **Title:** A generative model for inorganic materials design
- **First author / affiliation:** Claudio Zeni — Microsoft Research AI for Science
- **Venue:** *Nature* 639, 624–632 (2025)
- **Paper:** <https://www.nature.com/articles/s41586-025-08628-5> · arXiv: <https://arxiv.org/abs/2312.03687>
- **Code:** <https://github.com/microsoft/mattergen>
- **Highlights:** Diffusion model over coordinates, lattice and atom types; supports a wide variety of conditioning adapters (composition, symmetry, properties); used as data source for some PXRD-conditioning experiments.

### CrystalFormer — Space-Group Informed Transformer (2024)

- **Title:** Space Group Informed Transformer for Crystalline Materials Generation
- **First author / affiliation:** Zhendong Cao — Institute of Physics, CAS (senior: Lei Wang)
- **Venue:** arXiv:2403.15734
- **Paper:** <https://arxiv.org/abs/2403.15734>
- **Code:** <https://github.com/deepmodeling/CrystalFormer>
- **Highlights:** Autoregressive transformer over Wyckoff-position / species / lattice tokens; explicit symmetry inductive bias.

### CrystaLLM — Decoder-only LM on CIF Text (2024)

- **Title:** Crystal structure generation with autoregressive large language modeling
- **First author / affiliation:** Luis M. Antunes — University of Reading
- **Venue:** *Nature Communications* 15, 10570 (2024)
- **Paper:** <https://www.nature.com/articles/s41467-024-54639-7> · arXiv: <https://arxiv.org/abs/2307.04340>
- **Code:** <https://github.com/lantunes/CrystaLLM>
- **Highlights:** GPT-style decoder LM trained on millions of CIFs; supports space-group conditioned generation. Direct precursor to deCIFer and CrystaLLM-π.

---

## Datasets & Benchmarks

### opXRD — Open Experimental PXRD Database (2025)

- **Title:** opXRD: Open Experimental Powder X-Ray Diffraction Database
- **First author / affiliation:** Daniel Hollarek — KIT (AiMat, senior: Pascal Friederich)
- **Venue:** *Advanced Intelligent Discovery* 2, e202500044 (2026); arXiv:2503.05577
- **Paper:** <https://arxiv.org/abs/2503.05577>
- **Data portal:** <https://xrd.aimat.science/> · <https://zenodo.org/records/15298026>
- **Highlights:** 92,552 labeled + unlabeled experimental patterns contributed by multiple labs, covering many materials classes.

### SimXRD-4M (ICLR 2025)

- **Title:** SimXRD-4M: Big Simulated X-ray Diffraction Data and Crystal Symmetry Classification Benchmark
- **First author / affiliation:** Bin Cao — HKUST(GZ)
- **Venue:** *ICLR* 2025
- **Paper:** <https://openreview.net/forum?id=mkuB677eMM> · <https://arxiv.org/abs/2406.15469>
- **Code / data:** <https://github.com/Bin-Cao/SimXRD>
- **Highlights:** 4,065,346 PXRD patterns from 119,569 distinct structures simulated under varying grain size, orientation, internal stress, inelastic scattering and thermal vibration. Benchmarks 21 sequence models (CNN, RNN, Transformer).

### CHILI-3K / CHILI-100K (2024)

- **Title:** CHILI: Chemically-Informed Large-scale Inorganic Nanomaterials Dataset for Advancing Graph Machine Learning
- **First author / affiliation:** Ulrik Friis-Jensen — University of Copenhagen
- **Venue:** *KDD* 2024; arXiv:2402.13221
- **Paper:** <https://arxiv.org/abs/2402.13221>
- **Code / data:** <https://github.com/UlrikFriisJensen/CHILI>
- **Highlights:** Large-scale nanomaterials graph dataset; 11 property tasks (atom, crystal system, space group) and 8 regression tasks including PXRD, ND, SAXS, SANS, xPDF, nPDF.

### SIMPOD (2025)

- **Title:** A new benchmark for machine learning applied to powder X-ray diffraction
- **First author / affiliation:** Sergio Rincón — Universidad de los Andes (senior: Pablo Arbeláez)
- **Venue:** *Scientific Data* 12 (2025)
- **Paper:** <https://www.nature.com/articles/s41597-025-05534-3>
- **Code / data:** <https://github.com/BCV-Uniandes/SIMPOD>
- **Highlights:** 467,861 simulated PXRD patterns sourced from the Crystallography Open Database (COD) in both 1D-vector and 2D radial-image format.

### RRUFF (Lafuente et al., 2015)

- **Title:** The power of databases: the RRUFF project
- **Paper:** <https://www.degruyter.com/document/doi/10.1515/9783110417104-003>
- **Portal:** <https://rruff.info/>
- **Highlights:** Empirical XRD / Raman / IR / chemistry database for minerals; widely used as the experimental benchmark for PXRD ML methods.

### Materials Project / MP-20 / MP-PXRD

- **Materials Project:** <https://next-gen.materialsproject.org/>
- **MP-20 (CDVAE):** <https://github.com/txie-93/cdvae/tree/main/data/mp_20>
- **MP-20-PXRD (PXRDnet):** patterns derived in <https://github.com/gabeguo/cdvae_xrd>
- **Highlights:** De facto training set for most PXRD ↔ structure generative models.

### Crystallography Open Database (COD)

- **Portal:** <http://www.crystallography.net/cod/>
- **Highlights:** ~500k CIFs (organic / inorganic / minerals); used as a free alternative to ICSD for many ML training sets (e.g. SIMPOD, CrystaLLM-π COD-XRD).

### JARVIS-DFT XRD

- **Portal:** <https://jarvis.nist.gov/jarvisxrd/>
- **Highlights:** Simulated XRD lookup over JARVIS-DFT structures; used to train DiffractGPT.

### ICSD-derived Synthetic-Crystal Benchmark (Schopmans et al., 2023)

- **Code:** <https://github.com/aimat-lab/ML4pXRDs>
- **Highlights:** Pipeline for training symmetry classifiers from synthetically generated random crystals and evaluating against ICSD patterns.

---

## Simulation, Refinement, and Utility Tools

- **pymatgen XRDCalculator** — Python simulation of PXRD from CIF. <https://pymatgen.org/pymatgen.analysis.diffraction.html>
- **GSAS-II** — Open-source Rietveld refinement (used by PXRDGen, RAPID, AlphaDiffract, etc.). <https://subversion.xray.aps.anl.gov/trac/pyGSAS>
- **FullProf** — Classical Rietveld suite. <https://www.ill.eu/sites/fullprof/>
- **TOPAS-Academic** — Macro-language Rietveld engine. <http://www.topas-academic.net/>
- **diffpy-cmi / PDFfit2** — Pair distribution function modeling. <https://www.diffpy.org/>
- **xrdpattern** — Python package shipped with opXRD for unified PXRD I/O and curation. <https://github.com/aimat-lab/xrdpattern>
- **WPEM** — Whole Powder Pattern Modelling toolbox by the CPICANN authors. <https://github.com/Bin-Cao/WPEM>
- **AtomGPT / DiffractGPT inference** — <https://github.com/usnistgov/atomgpt>

---

## Reviews & Surveys

- **End-to-End Crystal Structure Prediction from Powder X-Ray Diffraction** — Chinese-language review on themoonlight.io that motivated this repo. <https://www.themoonlight.io/zh/review/end-to-end-crystal-structure-prediction-from-powder-x-ray-diffraction>
- **Machine learning assisted crystal structure prediction made simple** — *J. Mater. Inf.* (2024). <https://www.oaepublish.com/articles/jmi.2024.18>
- **A Comprehensive Review of Machine-Learning Approaches for Crystal Structure/Property Prediction** — *Crystals* 15, 925 (2025). <https://www.mdpi.com/2073-4352/15/11/925>
- **Identifying crystal structures beyond known prototypes from X-ray powder diffraction spectra** — *Phys. Rev. Materials* 8, 103801 (2024). <https://journals.aps.org/prmaterials/abstract/10.1103/PhysRevMaterials.8.103801>

---

## Related Curated Lists

- [awesome-materials-informatics](https://github.com/tilde-lab/awesome-materials-informatics) — broad materials-informatics list.
- [awesome-self-supervised-learning-for-graphs](https://github.com/LirongWu/awesome-graph-self-supervised-learning) — relevant for crystal-graph encoders.
- [awesome-generative-models-for-materials](https://github.com/usnistgov/jarvis_leaderboard) (JARVIS Leaderboard) — leaderboard tracking many of the generative models above.

---

## Notes on "Who was first?"

Multiple recent works each claim some form of "first end-to-end PXRD → crystal" status. The claims are not contradictory because they differ in scope:

| Work | Specific "first" claim |
| --- | --- |
| **Park et al. (2017)** | First CNN to classify crystal system / space group from PXRD. |
| **Lee et al. (2020)** | First deep CNN demonstrated for multiphase inorganic phase ID at scale. |
| **XCA (2021)** | First autonomous companion agent for real-time PXRD phase ID. |
| **CrystalNet / Guo et al. (2024)** | First end-to-end neural network producing 3D electron density from PXRD. |
| **XtalNet (2024)** | First equivariant *generative* model for PXRD-conditioned CSP (≤400 atoms/cell). |
| **Crystalyze (2024)** | First demonstrated solution of previously-unsolved PDF entries with a generative model. |
| **PXRDnet (2025)** | First diffusion-based ab-initio solver applied to *experimental nanocrystalline* PXRD across all 7 crystal systems. |
| **PXRDGen (2025)** | First to integrate generative model + automated Rietveld refinement in one pipeline. |
| **deCIFer (2025)** | First autoregressive CIF *language model* conditioned on PXRD. |
| **DiffractGPT (2025)** | First generative *pretrained* transformer adapted to XRD-conditioned structure prediction. |
| **XRDSol (2026)** | First sub-second equivariant diffusion solver explicitly benchmarked on the ICDD experimental PDF database. |
| **RealPXRD-Solver (2026)** | First solver trained on a >6M-entry theoretical corpus with experiment-mimicking augmentations, validated on CNRS + RRUFF. |

---

## Contributing

PRs are welcome. Please follow the existing format:

```
### <ShortName> — <One-sentence method tagline> (<year>)

- **Title:** <full paper title>
- **First author / affiliation:** <name> — <institution>
- **Venue:** <journal / conf> (<year>); arXiv:<id>
- **Paper:** <https://...>
- **Code:** <https://...>
- **Highlights:** <1–3 sentences>
```

Please open an issue first for entries whose claims are still pre-print and not yet peer-reviewed.
