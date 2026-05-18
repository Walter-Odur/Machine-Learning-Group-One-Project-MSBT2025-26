# Transcriptomic Prediction of Pathological Complete Response to Neoadjuvant Chemotherapy in Breast Cancer

A Spearman-filtered, Bayesian-optimised machine learning framework with SHAP explainability for predicting pCR from pre-treatment RNA-seq tumour profiles.

## Overview

Neoadjuvant chemotherapy (NAC) is standard-of-care for locally advanced breast cancer, yet only 15-53% of patients achieve pathological complete response (pCR). This project develops an explainable ML pipeline to predict which patients will benefit from NAC using transcriptomic data, enabling personalised treatment decisions.

## Dataset

- **GSE163882** - 222 multi-institutional breast cancer biopsies (RNA-seq, TPM)
- Published by Park et al. (2020), *Nature Communications*
- Pre-treatment biopsies with known pCR/RD outcomes after anthracycline/taxane-based NAC

## Methodology

| Step | Method | Reference |
|------|--------|-----------|
| Feature Selection | Spearman rank correlation (P < 0.001) | Chen et al. (2022) |
| Class Imbalance | Cost-sensitive learning (class weights) | Blagus & Lusa (2013) |
| Hyperparameter Tuning | Bayesian optimisation (50 iterations/model) | Snoek et al. (2012) |
| Explainability | SHAP (SHapley Additive exPlanations) | Lundberg & Lee (2017) |
| Clinical Utility | Decision curve analysis | Vickers & Elkin (2006) |

## Key Results

- **Best model**: Logistic Regression (AUROC = 0.709, Sensitivity = 56.3%, MCC = 0.321)
- **Feature reduction**: 60,279 genes reduced to 575 (99.05% reduction)
- **9 consensus genes** validated across XGBoost and Random Forest SHAP analysis
- **Decision curve analysis** confirms net clinical benefit across relevant threshold range

## Repository Structure

```
.
├── pipeline_notebook.ipynb
├── results_spearman/
│   ├── results_test_performance.csv
│   ├── shap_top30_xgboost.csv
│   ├── shap_top30_rf.csv
│   ├── consensus_shap_genes.csv
│   ├── roc_prc_curves.png
│   ├── confusion_matrices.png
│   ├── shap_summary.png
│   ├── calibration_plot.png
│   ├── decision_curve_analysis.png
│   └── final_summary_figure.png
└── README.md
```

## Requirements

```
python >= 3.11
scikit-learn >= 1.3
xgboost >= 2.0
shap >= 0.43
scikit-optimize >= 0.10
pandas
numpy
matplotlib
seaborn
scipy
```

## Usage

1. Clone the repository
2. Download `GSE163882_all.data.tpms_222Samples.csv` and `GSE163882_series_matrix.txt` from [GEO](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE163882)
3. Place data files in the project root
4. Run `GSE163882_pCR_Spearman_Pipeline.ipynb` cell by cell

## Contributors

- **WALTER ODUR**
- **SARAH NAMUBIRU**
- **ELASTUS SSEMWANGA**
- **GABRIEL PATROVAS OKIDI**
- **LATIFAH NAKAYENGA**
- **MARTIN ODONG**
- **GODWIN TUSHABE**

## References

1. Park, Y.H., et al. (2020). Chemotherapy induces dynamic immune responses in breast cancers that impact treatment outcome. *Nature Communications*, 11, 6175.
2. Chen, J., et al. (2022). Machine learning models based on immunological genes to predict the response to neoadjuvant therapy in breast cancer patients. *Frontiers in Immunology*, 13, 948601.
3. Cortazar, P., et al. (2014). Pathological complete response and long-term clinical benefit in breast cancer: the CTNeoBC pooled analysis. *The Lancet*, 384(9938), 164-172.
4. Lundberg, S.M., and Lee, S.I. (2017). A Unified Approach to Interpreting Model Predictions. *NeurIPS*, 30.
5. Vickers, A.J., and Elkin, E.B. (2006). Decision Curve Analysis: A Novel Method for Evaluating Prediction Models. *Medical Decision Making*, 26(6), 565-574.

## License

This project is for academic and research purposes.
