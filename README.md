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
```

If your report filename differs, update the path above accordingly.

---

## Data & Setup

### Data Availability
This public repository **does not include** the image dataset/compressed outputs due to size and/or distribution constraints.

### Expected Local Data Layout (recommended)

Create a `data/` folder locally (it should remain ignored by git):

```text
data/
├── images_original/
├── images_compressed/
└── labels_or_metadata.xlsx   # (if applicable)
```
Then, open the notebooks and update the path variables (look for cells such as `DATA_ROOT`, `DATA_DIR`, `IMAGE_DIR`, etc.).
> Tip: if you already have an archive (zip) used for testing, keep it locally and extract into `data/`.

## How to Run (Reproducibility)
### Option A — Run in order (recommended)
1. **Stage 1**: `notebooks/01_svm_train_test.ipynb`
  - Extract InceptionV3 features
  - Train/test SVM classifier
  - Save intermediate outputs if your notebook does so (optional)

2. **Stage 2**: `notebooks/02_regression_train_test.ipynb`
  - Load/compute required features and labels
  - Train/test the multi-output regressor
  - Generate evaluation metrics and plots

### Option B — Run individually
Each notebook can be run independently as long as the dataset paths are correctly configured.

## Environment / Dependencies
This project is implemented in **Python** using Jupyter notebooks.

Recommended steps:

1. Create a clean environment (conda/venv)
2. Install dependencies (choose one approach):
  - If you have `requirements.txt`, run:
    ```text
    pip install -r requirements.txt
    ```
  - Otherwise, install the common stack used in the notebooks (example):
    ```text
    pip install numpy pandas scikit-learn matplotlib notebook
    pip install tensorflow
    ```
    > (Adjust based on imports in your notebooks.)
If you want, you can generate a requirements.txt after confirming everything runs:
    ```text
    pip freeze > requirements.txt
    ```

## Notes
- This is a **team project**. Co-authors are omitted in this public version.
- The reported results and experiments are documented in the accompanying PDF report.
- If you plan to share this repo in applications, keep the README focused on: **problem** → **method** → **results** → **how to run**.

## License
This repository is released under the **MIT License** (see `LICENSE`).
