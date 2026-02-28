<div align="center">

# 🧬 iGS — Intelligent Genomic Selection Platform

**A comprehensive, GUI-driven platform for genomic selection (GS) design in crop breeding.**

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey)]()
[![Models](https://img.shields.io/badge/GS%20Models-33-orange)]()

![Benchmark Demo](docs/images/Comprehensive_Benchmark_Wheat_Yield.png)

</div>

---

## ✨ Features

| Module | Description |
|---|---|
| 🧬 **Genomic Selection (GS)** | 33 models covering statistical, ML, and deep learning methods |
| 📊 **Benchmark System** | Automated multi-trait, multi-model accuracy comparison |
| 🖥️ **Modern GUI** | PyQt5-based desktop application with dark sidebar |
| 📁 **Data Pipeline** | VCF → imputation → PCA → GBLUP/ML prediction |

---

## 🔬 Supported GS Models (33 Total)

<details>
<summary><b>Statistical / Bayesian Models (R-based)</b></summary>

| Model | Backend | Description |
|---|---|---|
| rrBLUP | R (rrBLUP) | Ridge Regression BLUP |
| GBLUP | R / Python | Genomic BLUP via G-matrix |
| BRR | R (BGLR) | Bayesian Ridge Regression |
| BayesA | R (BGLR) | Bayesian regression (scaled-t) |
| BayesB | R (BGLR) | Bayesian variable selection |
| BayesC | R (BGLR) | Spike-and-slab prior |
| LASSO | R (BGLR) | Least Absolute Shrinkage |
| Elastic Net | Python (sklearn) | L1+L2 regularization |
| RKHS | R (BGLR) | Reproducing Kernel Hilbert Space |
| BFR | R | Bayesian Functional Regression |
| PLS | Python | Partial Least Squares |
| SOMMER | R (sommer) | Mixed model with sommer |
| PCA+RR | R | Principal Component Regression |

</details>

<details>
<summary><b>Machine Learning Models (Python-based)</b></summary>

| Model | Description |
|---|---|
| Random Forest | Ensemble of decision trees |
| Extra Trees | Extremely Randomized Trees |
| XGBoost | Gradient Boosted Trees |
| LightGBM | Light Gradient Boosting Machine |
| CatBoost | Categorical feature boosting |
| SVM | Support Vector Machine (R/Python) |
| Ridge | Linear Ridge Regression |

</details>

<details>
<summary><b>Deep Learning / Graph Neural Network Models</b></summary>

| Model | Description |
|---|---|
| MLP-GS | Multi-Layer Perceptron |
| DNN-GS | Deep Neural Network |
| CNN-GS | 1D Convolutional Neural Network |
| Transformer-GS | Self-attention Transformer with SNP patching |
| DeepBLUP | Hybrid deep+BLUP model |
| DeepResBLUP | ResNet-style BLUP |
| GraphConv-GS | Graph Convolutional Network |
| GraphAttn-GS | Graph Attention Network (GAT) |
| GraphSAGE-GS | GraphSAGE neighbor sampling |
| GraphFormer | Graph Transformer |
| Ensemble-GS | Stacking ensemble of all models |

</details>

---

## 🚀 Quick Start

### 1. Prerequisites

- **Python** ≥ 3.8
- **R** ≥ 4.0 (for Bayesian / BLUP models) — [Download R](https://cran.r-project.org/)
- **PLINK** (for VCF processing) — [Download PLINK](https://www.cog-genomics.org/plink/)

### 2. Installation

```bash
git clone https://github.com/YOUR_USERNAME/iGS-Breeding.git
cd iGS-Breeding

# Install Python dependencies
pip install -r requirements.txt

# Optional: deep learning and graph neural networks
pip install -r requirements-optional.txt
```

### 3. Install R packages

Open R and run:

```r
install.packages(c("rrBLUP", "BGLR", "sommer", "glmnet", "e1071"))
```

### 4. Launch the GUI

```bash
python gui_main.py
```

### 5. Command-line Benchmark

```bash
# Wheat multi-trait benchmark (33 models × 6 traits)
python wheat_gs_batch_benchmark.py

# Maize benchmark (maize8652 dataset)
python maize_gs_batch_benchmark.py
```

---

## 📁 Project Structure

```
iGS-Breeding/
├── gui_main.py                  # Main GUI entry point (PyQt5)
├── wheat_gs_batch_benchmark.py  # Wheat GS benchmark runner
├── maize_gs_batch_benchmark.py  # Maize GS benchmark runner
│
├── scripts/                     # GS model worker scripts
│   ├── worker_gblup.py          # GBLUP (Python)
│   ├── worker_rrblup.R          # rrBLUP (R)
│   ├── worker_bglr.R            # BGLR Bayesian models (R)
│   ├── worker_transformer.py    # Transformer-GS
│   ├── worker_graphattngs.py    # Graph Attention Network
│   ├── worker_xgboost.py        # XGBoost
│   ├── worker_design.py         # CRISPR sgRNA design
│   └── ...                      # 30+ other workers
│
├── testdata/                    # Sample datasets for testing
│   ├── wheat_genotype_withID.csv
│   ├── wheat_phenotype_withID.csv
│   ├── Real_Breeder_Data.vcf
│   └── Test_Data_With_NA.vcf
│
├── resources/                   # Runtime dependencies (not tracked by git)
│   ├── R-Portable/              # Portable R (Windows)
│   ├── Python-Portable/         # Portable Python (Windows)
│   └── plink/                   # PLINK binary
│
├── docs/                        # Documentation & images
│   └── images/
│
├── examples/                    # Usage examples
│
├── Result_Output/               # GS pipeline outputs (auto-generated)
├── Result_GeneEditing/          # CRISPR design outputs (auto-generated)
│
├── requirements.txt             # Core Python dependencies
├── requirements-optional.txt   # Deep learning dependencies
├── setup.cfg                    # Package metadata
└── LICENSE
```

---

## 🖥️ GUI Overview

The GUI is organized into two main modules accessible from the sidebar:

**🧬 Genomic Selection (GS)**
1. **Data Import** — Load VCF or CSV genotype/phenotype files
2. **Quality Control** — Filter SNPs, handle missing data
3. **Imputation** — Impute missing genotypes
4. **GWAS** — Genome-wide association analysis
5. **PCA** — Principal component analysis
6. **Model Training** — Select and run any of 33 GS models
7. **Results** — View accuracy metrics (r, RMSE) and plots

**✂️ Gene Editing (CRISPR)**
1. Upload genome FASTA
2. Configure PAM type (SpCas9 / AsCas12a)
3. Export sgRNA candidate list

---

## 📊 Benchmark Results

| Dataset | Best Model | Pearson r |
|---|---|---|
| Wheat2000 — TKW | BayesB | 0.84 |
| Wheat2000 — HARD | rrBLUP | 0.87 |
| Wheat2000 — PROT | GBLUP | 0.72 |
| maize8652 — PH | LightGBM | 0.89 |
| maize8652 — DTT | XGBoost | 0.91 |

> Full benchmark plots: `docs/images/`

---

## 🤝 Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](docs/CONTRIBUTING.md) first.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-model`)
3. Commit your changes (`git commit -m 'Add new GS model'`)
4. Push to branch (`git push origin feature/new-model`)
5. Open a Pull Request

---

## 📚 Citation

If you use iGS in your research, please cite:

```bibtex
@software{iGS2026,
  author  = {iGS Development Team},
  title   = {iGS: Intelligent Genomic Selection Platform},
  year    = {2026},
  url     = {https://github.com/YOUR_USERNAME/iGS-Breeding},
  version = {0.1.0}
}
```

---

## 📄 License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.
