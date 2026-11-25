# Temporal Explainable AI for Dynamic Pulmonary Embolism Risk Assessment

This repository holds the analysis code for the paper *Temporal Explainable AI for Dynamic Pulmonary Embolism Risk Assessment Using Longitudinal EHR Data*.

The pipeline builds a leakage-safe inpatient cohort from the INSPECT dataset and represents 14 vital signs and laboratory tests in 6-hour bins. A prefix-trained GRU updates pulmonary embolism (PE) risk every 6 hours. Temporal SHAP (expected gradients) explains both the current risk and its change between prediction points.

**No data is included.** INSPECT is available from the Stanford Center for Artificial Intelligence in Medicine and Imaging (AIMI) under a data use agreement, and it cannot be redistributed. This repository contains code only.

## What the notebook does

| Part | Cells | Content |
|---|---|---|
| 1 | 0–8 | Data setup: CSV to Parquet, DuckDB views, crosswalk checks, labelled cohort funnel |
| 2 | P2-0 to P2-11 | Cohort per horizon, visit anchor, vitals/labs extraction with unit fixes, 6-hour bins, leakage-safe static features, tensors |
| 3 | H1, I1, J1, K1 | Logistic regression, XGBoost, and GRU with 5-fold patient-level CV; calibration, decision curves, alert burden |
| 4 | M1, K2, K3, L1 | Prefix-trained GRU, temporal SHAP, risk-change attribution with common random numbers, explanation quality |
| 5 | S1, C1, N1 | Sensitivity analyses and secondary horizons (12, 48, 72 h) |
| 6 | W1, P1, A1, M2 | Approximate Wells/Geneva, prior-VTE leakage audit, age filter, medication and procedure features |
| 7 | V1, F1 | Verification-bias analysis and final paper tables and figures |

## Requirements

The notebook runs on Google Colab with a GPU runtime. Python packages are listed in `requirements.txt`. Install them with:

```bash
pip install -r requirements.txt
```

## How to run

1. Get access to INSPECT and accept its data use agreement.
2. Put the INSPECT EHR CSV files and label files in your own Google Drive.
3. Open `notebooks/inspect_pe_pipeline.ipynb` in Colab and set the paths in cell 1 (Config).
4. Run all cells in order. The notebook writes Parquet files, tensors and results to `INSPECT_outputs/` in your Drive.

Patient-level data and intermediate files stay in your Drive. Share only aggregate tables and figures, as the data use agreement requires.

## Repository layout

```
notebooks/   analysis notebook (outputs cleared)
paper/       LaTeX source of the paper (added after review)
```

## Citation

Citation details will be added after publication.
