<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>X-MGTNet</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; background: #0d1117; color: #e6edf3; line-height: 1.6; }
        
        /* Header */
        .header { text-align: center; padding: 60px 20px 40px; border-bottom: 1px solid #21262d; }
        .header h1 { font-size: 2.8rem; font-weight: 700; margin-bottom: 10px; }
        .header p { color: #8b949e; font-size: 1.1rem; max-width: 600px; margin: 0 auto 25px; }
        
        /* Badges */
        .badges { display: flex; flex-wrap: wrap; justify-content: center; gap: 8px; margin-bottom: 25px; }
        .badge { padding: 5px 12px; border-radius: 20px; font-size: 0.78rem; font-weight: 600; text-decoration: none; }
        .badge-blue   { background: #1f6feb; color: white; }
        .badge-orange { background: #e05d22; color: white; }
        .badge-green  { background: #238636; color: white; }
        .badge-purple { background: #8957e5; color: white; }
        .badge-grey   { background: #30363d; color: #e6edf3; }
        .badge-colab  { background: #f9ab00; color: #1a1a1a; }
        
        /* Nav */
        .nav { display: flex; justify-content: center; gap: 20px; flex-wrap: wrap; }
        .nav a { color: #58a6ff; text-decoration: none; font-size: 0.95rem; }
        .nav a:hover { text-decoration: underline; }
        
        /* Main */
        .container { max-width: 900px; margin: 0 auto; padding: 40px 20px; }
        
        /* Sections */
        .section { margin-bottom: 50px; }
        .section h2 { font-size: 1.4rem; font-weight: 600; padding-bottom: 10px; border-bottom: 1px solid #21262d; margin-bottom: 20px; }
        
        /* Tables */
        table { width: 100%; border-collapse: collapse; font-size: 0.9rem; margin-bottom: 15px; }
        th { background: #161b22; color: #8b949e; padding: 10px 14px; text-align: left; font-weight: 600; border: 1px solid #21262d; }
        td { padding: 10px 14px; border: 1px solid #21262d; }
        tr:hover td { background: #161b22; }
        td a { color: #58a6ff; text-decoration: none; }
        td a:hover { text-decoration: underline; }
        .star { color: #f0e68c; }
        .check { color: #3fb950; }
        
        /* Code blocks */
        pre { background: #161b22; border: 1px solid #21262d; border-radius: 8px; padding: 16px; overflow-x: auto; font-size: 0.85rem; color: #e6edf3; margin-bottom: 15px; }
        code { font-family: 'SF Mono', Consolas, monospace; }
        p code, td code { background: #161b22; padding: 2px 6px; border-radius: 4px; font-size: 0.85rem; color: #ff7b72; }
        
        /* Callouts */
        .callout { background: #161b22; border-left: 4px solid #f0e68c; border-radius: 6px; padding: 12px 16px; margin-bottom: 15px; font-size: 0.9rem; color: #8b949e; }
        .callout.blue { border-color: #58a6ff; }
        .callout.green { border-color: #3fb950; }
        
        /* Architecture */
        .arch { background: #161b22; border: 1px solid #21262d; border-radius: 8px; padding: 24px; font-family: monospace; font-size: 0.85rem; color: #e6edf3; white-space: pre; overflow-x: auto; }
        
        /* Colab buttons */
        .colab-btn { display: inline-block; background: #f9ab00; color: #1a1a1a; padding: 4px 10px; border-radius: 4px; font-size: 0.78rem; font-weight: 700; text-decoration: none; }
        .colab-btn:hover { background: #ffc107; }

        /* Contact */
        .contact-grid { display: grid; grid-template-columns: auto 1fr; gap: 8px 20px; font-size: 0.9rem; }
        .contact-grid strong { color: #e6edf3; }
        .contact-grid span { color: #8b949e; }

        /* Footer */
        .footer { text-align: center; padding: 30px; border-top: 1px solid #21262d; color: #8b949e; font-size: 0.85rem; }
        .footer span { color: #f85149; }
    </style>
</head>
<body>

<!-- HEADER -->
<div class="header">
    <h1>🧠 X-MGTNet</h1>
    <p>A reproducible, CC200-anchored preprocessing and augmentation framework for multimodal ASD diagnosis using fMRI and MEG neuroimaging data.</p>
    
    <div class="badges">
        <span class="badge badge-blue">🐍 Python 3.10+</span>
        <span class="badge badge-orange">🔥 PyTorch 2.0+</span>
        <span class="badge badge-green">🧠 MNE-Python 1.11</span>
        <span class="badge badge-purple">📊 nilearn 0.10</span>
        <span class="badge badge-grey">📄 CC-BY-NC-ND</span>
        <span class="badge badge-green">✅ KES 2026 Accepted</span>
        <a href="https://colab.research.google.com/github/sirinenaifar/X-MGTNet/blob/main/notebooks/01_fMRI_pipeline_ABIDE_I_II.ipynb" class="badge badge-colab">▶ Open in Colab</a>
    </div>

    <nav class="nav">
        <a href="#overview">📌 Overview</a>
        <a href="#datasets">🗂 Datasets</a>
        <a href="#quickstart">🚀 Quick Start</a>
        <a href="#structure">📁 Structure</a>
        <a href="#results">📊 Results</a>
        <a href="#architecture">🏗 Architecture</a>
        <a href="#paper">📄 Paper</a>
        <a href="#contact">📬 Contact</a>
    </nav>
</div>

<div class="container">

    <!-- OVERVIEW -->
    <div class="section" id="overview">
        <h2>📌 Overview</h2>
        <p style="margin-bottom:16px;"><strong>X-MGTNet</strong> addresses two critical bottlenecks in multimodal ASD deep learning:</p>
        <table>
            <tr><th>Bottleneck</th><th>Our Solution</th></tr>
            <tr><td>No standardized CC200 parcellation for ABIDE II</td><td>Custom fMRIPrep-to-CC200 pipeline via <code>NiftiLabelsMasker</code></td></tr>
            <tr><td>Scarce labeled pediatric MEG data</td><td>6 biologically-grounded augmentation techniques</td></tr>
        </table>
        <p>Both pipelines are anchored to the <strong>CC200 atlas</strong>, enabling seamless cross-attention fusion without modality-specific projections.</p>
    </div>

    <!-- DATASETS -->
    <div class="section" id="datasets">
        <h2>🗂 Datasets</h2>
        <table>
            <tr><th>Dataset</th><th>Modality</th><th>Subjects</th><th>Sites</th><th>Access</th></tr>
            <tr><td><a href="http://fcon_1000.projects.nitrc.org/indi/abide/">ABIDE I</a></td><td>fMRI</td><td>1,112 (539 ASD / 573 TC)</td><td>20</td><td>nilearn</td></tr>
            <tr><td><a href="http://fcon_1000.projects.nitrc.org/indi/abide/">ABIDE II</a></td><td>fMRI</td><td>1,114 (521 ASD / 593 TC)</td><td>19</td><td>S3 anonyme</td></tr>
            <tr><td><a href="https://openneuro.org/datasets/ds005234">OpenNeuro ds005234</a></td><td>MEG</td><td>75 (36 ASD / 39 TC)</td><td>6</td><td>OpenNeuro</td></tr>
        </table>
        <div class="callout">⚠️ Data is publicly available but must be downloaded independently. No raw neuroimaging data is included in this repository.</div>
    </div>

    <!-- QUICK START -->
    <div class="section" id="quickstart">
        <h2>🚀 Quick Start</h2>
        <p style="margin-bottom:12px;"><strong>1. Clone the repository</strong></p>
        <pre><code>git clone https://github.com/sirinenaifar/X-MGTNet.git
cd X-MGTNet</code></pre>

        <p style="margin-bottom:12px;"><strong>2. Install dependencies</strong></p>
        <pre><code>pip install -r requirements.txt</code></pre>

        <p style="margin-bottom:12px;"><strong>3. Run the pipelines on Google Colab</strong></p>
        <div class="callout blue">💡 Both notebooks are designed to run on <strong>Google Colab</strong> (free GPU). All experiments use <code>seed=42</code> for deterministic reproducibility.</div>
        <table>
            <tr><th>#</th><th>Notebook</th><th>Description</th><th>Runtime</th><th></th></tr>
            <tr>
                <td>01</td>
                <td><code>01_fMRI_pipeline_ABIDE_I_II.ipynb</code></td>
                <td>fMRI preprocessing → PyG graphs</td>
                <td>~3-4h</td>
                <td><a href="https://colab.research.google.com/github/sirinenaifar/X-MGTNet/blob/main/notebooks/01_fMRI_pipeline_ABIDE_I_II.ipynb" class="colab-btn">▶ Open in Colab</a></td>
            </tr>
            <tr>
                <td>02</td>
                <td><code>02_MEG_pipeline_OpenNeuro_ds005234.ipynb</code></td>
                <td>MEG preprocessing → feature tensors</td>
                <td>~2-3h</td>
                <td><a href="https://colab.research.google.com/github/sirinenaifar/X-MGTNet/blob/main/notebooks/02_MEG_pipeline_OpenNeuro_ds005234.ipynb" class="colab-btn">▶ Open in Colab</a></td>
            </tr>
        </table>
    </div>

    <!-- STRUCTURE -->
    <div class="section" id="structure">
        <h2>📁 Structure</h2>
        <pre><code>X-MGTNet/
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
└── README.md</code></pre>
    </div>

    <!-- RESULTS -->
    <div class="section" id="results">
        <h2>📊 Results</h2>

        <p style="margin-bottom:10px;font-weight:600;">fMRI Pipeline</p>
        <table>
            <tr><th>Metric</th><th>Value</th></tr>
            <tr><td>Subjects retained (post-QC)</td><td>1,166 across 32 sites</td></tr>
            <tr><td>PyG graphs produced</td><td>1,166 (200 nodes × 3 features)</td></tr>
            <tr><td>Mean edges per graph</td><td>~7,959 (top-20% threshold)</td></tr>
            <tr><td>Augmented training graphs</td><td>9,639 (×11.8)</td></tr>
            <tr><td>ASD hypoconnectivity ∆</td><td>0.031</td></tr>
        </table>

        <p style="margin-bottom:10px;font-weight:600;">MEG Pipeline</p>
        <table>
            <tr><th>Metric</th><th>Value</th></tr>
            <tr><td>Subjects retained (post-QC)</td><td>74 / 75 (98.7% yield)</td></tr>
            <tr><td>ERF sequences shape</td><td>250 × 510 (T × Features)</td></tr>
            <tr><td>Augmented training sequences</td><td>837 (×16.4)</td></tr>
            <tr><td>M100 latency drift after aug.</td><td>4.95 ms</td></tr>
        </table>

        <p style="margin-bottom:10px;font-weight:600;">Augmentation Fidelity</p>
        <table>
            <tr><th>Modality</th><th>Check</th><th>Result</th></tr>
            <tr><td>fMRI</td><td>Wasserstein distance FCM</td><td>0.00837 <span class="check">✅</span></td></tr>
            <tr><td>fMRI</td><td>∆ hypoconnectivity drift</td><td>0.0000 <span class="check">✅</span></td></tr>
            <tr><td>fMRI</td><td>Label preservation (GraphMixup)</td><td>100.0% <span class="check">✅</span></td></tr>
            <tr><td>MEG</td><td>KS p-value alpha band</td><td>0.728 <span class="check">✅</span></td></tr>
            <tr><td>MEG</td><td>KS p-value gamma band</td><td>0.283 <span class="check">✅</span></td></tr>
            <tr><td>MEG</td><td>Label preservation (MixupSeq)</td><td>100.0% <span class="check">✅</span></td></tr>
        </table>

        <p style="margin-bottom:10px;font-weight:600;">Graph Thresholding Sensitivity</p>
        <table>
            <tr><th>Threshold</th><th>Mean edges</th><th>∆ hypoconnectivity</th></tr>
            <tr><td>top-10%</td><td>1,990</td><td>0.0265</td></tr>
            <tr style="background:#1f2937;"><td><strong>top-20% <span class="star">⭐</span></strong></td><td><strong>3,994</strong></td><td><strong>0.0228</strong></td></tr>
            <tr><td>top-30%</td><td>5,982</td><td>0.0204</td></tr>
        </table>
    </div>

    <!-- ARCHITECTURE -->
    <div class="section" id="architecture">
        <h2>🏗 Architecture</h2>
        <div class="arch">fMRI (ABIDE I+II)          MEG (OpenNeuro ds005234)
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
         ASD / TC Classifier</div>
    </div>

    <!-- PAPER -->
    <div class="section" id="paper">
        <h2>📄 Paper</h2>
        <p style="margin-bottom:12px;">If you use this code, please cite:</p>
        <pre><code>@inproceedings{naifar2026xmgtnet,
  title     = {From Raw Neuroimaging to Graph-Ready Data: A Reproducible
               Multimodal fMRI+MEG Pipeline for ASD Deep Learning},
  author    = {Naifar, Sirine and Douss, Rim and Farah, Imed Riadh},
  booktitle = {Procedia Computer Science},
  series    = {KES 2026 -- 30th International Conference on Knowledge-Based
               and Intelligent Information & Engineering Systems},
  year      = {2026},
  publisher = {Elsevier}
}</code></pre>
    </div>

    <!-- CONTACT -->
    <div class="section" id="contact">
        <h2>📬 Contact</h2>
        <div class="contact-grid">
            <strong>Sirine Naifar</strong><span>naifar.sirine@gmail.com</span>
            <strong>Institution</strong><span>National School of Computer Sciences (ENSI), University of Manouba, Tunisia</span>
            <strong>Laboratory</strong><span>RIADI Laboratory</span>
        </div>
    </div>

</div>

<!-- FOOTER -->
<div class="footer">
    Made with <span>❤️</span> for reproducible neuroimaging research<br>
    © 2026 Sirine Naifar, Rim Douss, Imed Riadh Farah — ENSI, University of Manouba
</div>

</body>
</html>
