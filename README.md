# Sequence-Driven Classification of Aptamers with Ensemble Models

This repository contains the code for the manuscript:

> **Sequence-Driven Classification of Aptamers with Ensemble Models**

A sequence-only machine learning framework for classifying DNA aptamers by target type (cellular vs. steroidal) using TF-IDF k-mer representations and an ensemble of XGBoost classifiers.

---

## Repository Contents

- `Aptamer_Sequence_UPDATED3.ipynb` | Main notebook: training, validation, and prediction pipeline |
- `Amanda_seq_scored8.csv` | The 13 experimentally derived aldosterone aptamers used for external validation, with model predictions and Kd values |

---

## Data

The training dataset was derived from the **UTexas Aptamer Database** (publicly available):

> Askari et al., "UTexas Aptamer Database: the collection and long-term preservation of aptamer sequence information," *Nucleic Acids Res*, vol. 52, no. D1, pp. D351–D359, Jan. 2024. https://doi.org/10.1093/nar/gkad959

Download the database and save it as `UTA_new.xlsx` in the same folder as the notebook before running.

---

## Requirements

Install dependencies with:

```bash
pip install pandas numpy scikit-learn xgboost imbalanced-learn scipy matplotlib python-Levenshtein openpyxl
```

Or in a Jupyter cell:

```python
!pip install pandas numpy scikit-learn xgboost imbalanced-learn scipy matplotlib python-Levenshtein openpyxl
```

---

## How to Run

1. Download or clone this repository
2. Download `UTA_new.xlsx` from the UTexas Aptamer Database and place it in the same folder
3. Open `Aptamer_Sequence_UPDATED3.ipynb` in Jupyter or VS Code
4. Run **Cell 1** — loads data, trains the ensemble, evaluates on the held-out test set, and scores the 13 external aptamers
5. Run **Cell 2** — applies the trained model to new sequences and saves calibrated predictions

---

## Methods Summary

- **Features:** Character-level TF-IDF of 3–6 nucleotide k-mer motifs, combined with GC content and sequence length
- **Model:** Bagged ensemble of 9 XGBoost classifiers with early stopping
- **Calibration:** Platt scaling (logistic regression on validation probabilities)
- **Threshold optimization:** Per-class threshold tuning to maximize macro-F1
- **External validation:** 13 aldosterone aptamers independently isolated via SELEX in our laboratory

---

## Results

- **Internal test set:** 97.92% accuracy, macro-F1 = 0.95 (n = 236)
- **External validation:** 100% recall on 13 novel experimentally derived steroid aptamers
- **Sequence novelty:** Mean normalized Levenshtein distance to nearest training neighbor = 0.40 ± 0.07

---

## License

This code is released for academic and research use. Please cite the manuscript if you use this code or data in your work.
