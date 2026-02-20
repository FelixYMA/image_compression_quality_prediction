# Predicting Image Compression Quality with Machine Learning

A two-stage machine learning pipeline to predict image compression quality metrics (**PSNR / SSIM / FID**) from:
- a high-quality original image, and
- a specified compression method/level (e.g., JPEG, PNG, DNG, TIF; including unseen JPEG levels).

> This repository contains the implementation notebooks and the final report (in `docs/`).  
> **Note:** The dataset/images are not included in this public repo.

---

## Project Overview

### Goal
Build a compression quality prediction system that can estimate **PSNR, SSIM, and FID** for a compressed image outcome based on:
1) semantic content of the original image, and  
2) the compression method/level applied.

### Approach (Two-Stage Pipeline)

**Stage 1 — Semantic Classification**
- Extract deep visual features using **InceptionV3**
- Train an **SVM classifier** to categorize images by semantic content

**Stage 2 — Metric Regression**
- Encode compression method/level (e.g., `jpeg66`) + predicted semantic category
- Train a **multi-output Random Forest Regressor** to predict **PSNR / SSIM / FID**

---

## Key Results (reported in the course report)

- **Stage 1 (SVM):** ~**96.8%** test accuracy (reported).
- **Stage 2 (Regression):**
  - **PSNR:** strongest fit (**R² ~ 0.75**, reported)
  - **SSIM:** moderate fit (**R² ~ 0.49**, reported)
  - **FID:** weaker fit (**R² ~ 0.14**, reported)

See the full report for methodology details, experiments, and discussion:
- `docs/` (PDF)

---

## Repository Structure

```text
.
├── docs/
│   └── final_project_report.pdf          # final report (PDF)
├── notebooks/
│   ├── 01_svm_train_test.ipynb           # Stage 1: feature extraction + SVM training/testing
│   └── 02_regression_train_test.ipynb    # Stage 2: regression training/testing for PSNR/SSIM/FID
├── .gitignore
├── LICENSE
└── README.md
