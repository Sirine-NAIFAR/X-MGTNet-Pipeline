# 🧠 X-MGTNet: Multimodal fMRI+MEG Pipeline for ASD Deep Learning
 
<div align="center">
 
[![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)](https://python.org)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-orange?logo=pytorch)](https://pytorch.org)
[![MNE](https://img.shields.io/badge/MNE--Python-1.11-green)](https://mne.tools)
[![nilearn](https://img.shields.io/badge/nilearn-0.10-purple)](https://nilearn.github.io)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20349524.svg)](https://doi.org/10.5281/zenodo.20349524)
 
*A reproducible, CC200-anchored preprocessing and augmentation framework  
for multimodal ASD diagnosis using fMRI and MEG neuroimaging data.*
 
[🚀 Quick Start](#-quick-start) • [📊 Results](#-results) • [📬 Contact](#-contact)
 
</div>
 
## 📌 Overview
 
**X-MGTNet** addresses two critical bottlenecks in multimodal ASD deep learning:
 
| Bottleneck | Our Solution |
|---|---|
| No standardized CC200 parcellation for ABIDE II | Custom fMRIPrep-to-CC200 pipeline via `NiftiLabelsMasker` |
| Scarce labeled pediatric MEG data | 6 biologically-grounded augmentation techniques |
 
Both pipelines are anchored to the **CC200 atlas**, enabling seamless cross-attention fusion without modality-specific projections.
 
---
 
## 🗂 Datasets
 
| Dataset | Modality | Subjects | Sites | Access |
|---|---|---|---|---|
| [ABIDE I](http://fcon_1000.projects.nitrc.org/indi/abide/) | fMRI | 1,112 (539 ASD / 573 TC) | 20 | nilearn |
| [ABIDE II](http://fcon_1000.projects.nitrc.org/indi/abide/) | fMRI | 1,114 (521 ASD / 593 TC) | 19 | S3 anonyme |
| [OpenNeuro ds005234](https://openneuro.org/datasets/ds005234) | MEG | 75 (36 ASD / 39 TC) | 6 | OpenNeuro |
 
> ⚠️ Data is publicly available but must be downloaded independently.  
> No raw neuroimaging data is included in this repository.
 
---
## 🚀 Quick Start
 
### 1. Set up Google Drive
 
In your Google Drive, create the following folder structure and import the notebooks and phenotypic files inside:
 
```
Colab Notebooks/
└── Finale/
    ├── 01_fMRI_pipeline_ABIDE_I_II.ipynb
    ├── 02_MEG_pipeline_OpenNeuro_ds005234.ipynb
    ├── Phenotypic_ABIDE1.csv
    └── Phenotypic_ABIDE2.csv
```
 
### 2. Run the pipelines on Google Colab
 
> 💡 Open each notebook in **Google Colab** and execute cells **one by one, step by step, in order**.  
> All dependencies are installed automatically inside each notebook.  
> All experiments use `seed=42` for deterministic reproducibility.
 
| # | Notebook | Description | Runtime |
|---|---|---|---|
| 01 | `X_MGTNet_Diagnostic_TSA_par_architecture_hybride_GNN_+_Transformer_ABIDE_I_II.ipynb` | fMRI preprocessing → PyG graphs | ~3-4h |
| 02 | `X_MGTNet_Diagnostic_TSA_par_architecture_hybride_Transformer_MEG.ipynb` | MEG preprocessing → feature tensors | ~2-3h |
 
---
 
## 📊 Results
 
### fMRI Pipeline
 
| Metric | Value |
|---|---|
| Subjects retained (post-QC) | 1,166 across 32 sites |
| PyG graphs produced | 1,166 (200 nodes × 3 features) |
| Mean edges per graph | ~7,959 (top-20% threshold) |
| Augmented training graphs | 9,639 (×11.8) |
| ASD hypoconnectivity ∆ | 0.031 |
 
### MEG Pipeline
 
| Metric | Value |
|---|---|
| Subjects retained (post-QC) | 74 / 75 (98.7% yield) |
| ERF sequences shape | 250 × 510 (T × Features) |
| Augmented training sequences | 837 (×16.4) |
| M100 latency drift after aug. | 4.95 ms |
 
### Augmentation Fidelity
 
| Modality | Check | Result |
|---|---|---|
| fMRI | Wasserstein distance FCM | 0.00837 ✅ |
| fMRI | ∆ hypoconnectivity drift | 0.0000 ✅ |
| fMRI | Label preservation (GraphMixup) | 100.0% ✅ |
| MEG | KS p-value alpha band | 0.728 ✅ |
| MEG | KS p-value gamma band | 0.283 ✅ |
| MEG | Label preservation (MixupSeq) | 100.0% ✅ |
 
### Graph Thresholding Sensitivity
 
| Threshold | Mean edges | ∆ hypoconnectivity |
|---|---|---|
| top-10% | 1,990 | 0.0265 |
| **top-20%** ⭐ | **3,994** | **0.0228** |
| top-30% | 5,982 | 0.0204 |
 
---
 
## 🏗 Architecture
 
```
fMRI (ABIDE I+II)          MEG (OpenNeuro ds005234)
      │                              │
      ▼                              ▼
 GATv2 Encoder               Temporal Transformer
 (3 layers, 8 heads)          (4 blocks, 8 heads)
      │                              │
      ▼                              ▼
 Spatial embedding           Temporal embedding
      (256-d)                    (512-d)
      │                              │
      └──────────┬───────────────────┘
                 ▼
      Bidirectional Cross-Attention
      + Dempster-Shafer Uncertainty
                 │
                 ▼
         ASD / TC Classifier
```
---
 
## 📬 Contact
 
| | |
|---|---|
| **Sirine Naifar** | naifar.sirine@gmail.com |
| **Institution** | National School of Computer Sciences (ENSI), University of Manouba, Tunisia |
| **Laboratory** | RIADI Laboratory |
 
---
 
<div align="center">
Made with ❤️ for reproducible neuroimaging research  
© 2026 Sirine Naifar, Rim Douss, Imed Riadh Farah — ENSI, University of Manouba
</div>
