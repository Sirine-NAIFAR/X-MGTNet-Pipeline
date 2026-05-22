<div align="center">
🧠 X-MGTNet
Multimodal fMRI+MEG Pipeline for ASD Deep Learning
Afficher l'image
Afficher l'image
Afficher l'image
Afficher l'image
Afficher l'image
Afficher l'image
A reproducible, CC200-anchored preprocessing and augmentation framework
for multimodal ASD diagnosis using fMRI and MEG neuroimaging data.
📄 Paper • 🚀 Quick Start • 📁 Structure • 📊 Results • 📬 Contact
</div>

📌 Overview
X-MGTNet addresses two critical bottlenecks in multimodal ASD deep learning:
BottleneckOur SolutionNo standardized CC200 parcellation for ABIDE IICustom fMRIPrep-to-CC200 pipeline via NiftiLabelsMaskerScarce labeled pediatric MEG data6 biologically-grounded augmentation techniques
Both pipelines are anchored to the CC200 atlas, enabling seamless cross-attention fusion without modality-specific projections.

🗂 Datasets
DatasetModalitySubjectsSitesAccessABIDE IfMRI1,112 (539 ASD / 573 TC)20nilearnABIDE IIfMRI1,114 (521 ASD / 593 TC)19S3 anonymeOpenNeuro ds005234MEG75 (36 ASD / 39 TC)6OpenNeuro

⚠️ Data is publicly available but must be downloaded independently.
No raw neuroimaging data is included in this repository.


🚀 Quick Start
1. Clone the repository
bashgit clone https://github.com/sirinenaifar/X-MGTNet.git
cd X-MGTNet
2. Install dependencies
bashpip install -r requirements.txt
3. Run the pipelines
Open in Google Colab and execute in order:
#NotebookDescriptionRuntime01notebooks/01_fMRI_pipeline_ABIDE_I_II.ipynbfMRI preprocessing → PyG graphs~3-4h02notebooks/02_MEG_pipeline_OpenNeuro_ds005234.ipynbMEG preprocessing → feature tensors~2-3h

💡 All experiments use seed=42 for deterministic reproducibility.


📁 Structure
X-MGTNet/
│
├── 📓 notebooks/
│   ├── 01_fMRI_pipeline_ABIDE_I_II.ipynb         # fMRI pipeline
│   └── 02_MEG_pipeline_OpenNeuro_ds005234.ipynb   # MEG pipeline
│
├── 📊 outputs/
│   ├── module4_9_fidelite_augmentation.png        # fMRI fidelity figure
│   ├── meg_fidelite_augmentation.png              # MEG fidelity figure
│   └── sensitivity_topk.png                      # Thresholding sensitivity
│
├── requirements.txt
├── LICENSE
└── README.md

📊 Results
fMRI Pipeline
MetricValueSubjects retained (post-QC)1,166 across 32 sitesPyG graphs produced1,166 (200 nodes × 3 features)Mean edges per graph~7,959 (top-20% threshold)Augmented training graphs9,639 (×11.8)ASD hypoconnectivity ∆0.031
MEG Pipeline
MetricValueSubjects retained (post-QC)74 / 75 (98.7% yield)ERF sequences shape250 × 510 (T × Features)Augmented training sequences837 (×16.4)M100 latency drift after aug.4.95 ms
Augmentation Fidelity
ModalityCheckResultfMRIWasserstein distance FCM0.00837 ✅fMRI∆ hypoconnectivity drift0.0000 ✅fMRILabel preservation (GraphMixup)100.0% ✅MEGKS p-value alpha band0.728 ✅MEGKS p-value gamma band0.283 ✅MEGLabel preservation (MixupSeq)100.0% ✅
Graph Thresholding Sensitivity
ThresholdMean edges∆ hypoconnectivitytop-10%1,9900.0265top-20% ⭐3,9940.0228top-30%5,9820.0204

🏗 Architecture
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

📄 Paper
If you use this code, please cite:
bibtex@inproceedings{naifar2026xmgtnet,
  title     = {From Raw Neuroimaging to Graph-Ready Data: A Reproducible
               Multimodal fMRI+MEG Pipeline for ASD Deep Learning},
  author    = {Naifar, Sirine and Douss, Rim and Farah, Imed Riadh},
  booktitle = {Procedia Computer Science},
  series    = {KES 2026 -- 30th International Conference on Knowledge-Based
               and Intelligent Information \& Engineering Systems},
  year      = {2026},
  publisher = {Elsevier}
}

📬 Contact
Sirine Naifarnaifar.sirine@gmail.comInstitutionNational School of Computer Sciences (ENSI), University of Manouba, TunisiaLaboratoryRIADI Laboratory

<div align="center">
Made with ❤️ for reproducible neuroimaging research
© 2026 Sirine Naifar, Rim Douss, Imed Riadh Farah — ENSI, University of Manouba
</div>
