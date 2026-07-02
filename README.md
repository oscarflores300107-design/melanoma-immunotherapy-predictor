# Melanoma Immunotherapy Response Predictor

[![Python](https://img.shields.io/badge/Python-3.10-blue)]()
[![License](https://img.shields.io/badge/License-MIT-green)]()
[![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)]()

> Predicting checkpoint inhibitor response in cutaneous melanoma using multi-omic data from TCGA-SKCM.

<!-- Cuando tengas el dashboard: agrega aquí un GIF de 5-10 seg mostrando el Streamlit app en acción.
Un GIF vale más que cualquier párrafo de descripción para un visitante casual. -->

## Why this matters

Anti-PD-1/CTLA-4 checkpoint inhibitors (pembrolizumab, nivolumab) generate $15B+ in annual melanoma sales, yet only a subset of patients respond durably. Identifying likely non-responders before treatment could redirect them toward alternative therapies faster, avoiding months of ineffective — and toxic — treatment.

This project builds an end-to-end ML pipeline that integrates RNA-seq expression, tumor mutation burden (TMB), and clinical variables to predict immunotherapy response in cutaneous melanoma patients.

## Data

| Source | Role | Samples |
|---|---|---|
| TCGA-SKCM (GDC Portal) | Primary training cohort | ~470 patients, RNA-seq + clinical |
| GSE91061 (Riaz et al., Cell 2017) | External validation | Nivolumab, pre/on-treatment |
| GSE78220 (Hugo et al., Cell 2016) | External validation | Pembrolizumab, pre-treatment |

## Methods

- **Feature engineering**: gene expression (top variance genes), TMB, clinical covariates (age, stage, sex)
- **Normalization**: `pydeseq2` / `gseapy`, applied strictly after train/test split to avoid data leakage
- **Models**: scikit-learn baselines → XGBoost
- **Explainability**: SHAP for feature-level interpretation
- **Survival analysis**: `lifelines` for Kaplan-Meier stratification by predicted response
- **Validation**: external cohorts (GSE91061, GSE78220) — no result is trusted without external validation

## Results

<!-- PLACEHOLDER — no borrar esta sección, actualízala en semana 5-6.
Un README sin esta sección se ve incompleto; un README que dice "in progress" se ve honesto y en ejecución activa. -->

*In progress — baseline model and EDA results expected week 3-4 of the 8-week build. See [`notes/01_literature_review.md`](notes/01_literature_review.md) for current literature synthesis.*

## Repository structure

```
melanoma-immunotherapy-predictor/
├── data/               # download scripts only — raw data not versioned
├── notebooks/          # 00_data_verification → 04_shap
├── src/                # data_loader.py, features.py, model.py
├── app/                # Streamlit dashboard
├── notes/              # literature review, working notes
└── reports/            # final technical report (week 8)
```

## Installation

```bash
git clone https://github.com/oscarflores300107-design/melanoma-immunotherapy-predictor.git
cd melanoma-immunotherapy-predictor
conda create -n skcm-imt python=3.10
conda activate skcm-imt
pip install -r requirements.txt
```

## References

1. Hugo et al., *Cell* 2016 — genomic and transcriptomic features of response to anti-PD-1
2. Riaz et al., *Cell* 2017 — tumor and microenvironment evolution during immunotherapy
3. Thorsson et al., *Immunity* 2018 — the immune landscape of cancer
4. Snyder et al., *NEJM* 2014 — genetic basis for clinical response to CTLA-4 blockade
5. Chen & Mellman, *Nature* 2017 — oncology meets immunology: the cancer-immunity cycle

## License

MIT — see [LICENSE](LICENSE)

---
*Built as part of an independent research project during summer 2026. Feedback and issues welcome.*
