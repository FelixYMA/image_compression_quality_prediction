# Predicting Image Compression Quality with Machine Learning

This project builds a **two-stage machine learning pipeline** to predict image compression quality metrics (**PSNR / SSIM / FID**) from:
- the original high-quality image, and
- a specified compression method/level (e.g., JPEG, PNG, DNG, TIF; including unseen JPEG levels).

## Approach (Two-Stage Pipeline)
**Stage 1 — Semantic Classification**
- Extract deep visual features using **InceptionV3**
- Train an **SVM** to classify images into semantic categories

**Stage 2 — Metric Regression**
- Encode the compression method (e.g., jpeg66) + use the predicted image category
- Train a **Random Forest Regressor** (multi-output) to predict **PSNR / SSIM / FID**

## Key Results (from report)
- SVM classification achieved **~96.8%** test accuracy (reported).
- Regression performance (reported): PSNR shows the strongest fit (R² ~0.75), SSIM moderate (R² ~0.49), and FID weaker (R² ~0.14).

## Repository Structure
.
├── notebooks/n
│ ├── 01_svm_train_test.ipynb
│ └── 02_regression_train_test.ipynb
├── docs/
│ └── CS4442_Project_Report.pdf
└── README.md
