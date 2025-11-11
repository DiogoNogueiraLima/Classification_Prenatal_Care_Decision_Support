# Maternal Health Risk Stratification

## Project Highlights
- **Clinical motivation.** Maternal and infant mortality remains ~295k deaths/year worldwide; proactive risk stratification helps clinicians allocate care.
- **Dataset.** UCI Maternal Health Risk (1,014 records of prenatal vital signs gathered via IoT devices in hospitals and community clinics).
- **Approach.** Rigorous data quality audit plus a **Cumulative Ordinal Classification** pipeline (two binary tasks for \(y\geq1\) and \(y\geq2\)) using RandomForest, KNN, and XGBoost candidates.
- **Key metrics.** RandomForest ordinal model reached **Accuracy 76.47%**, **F1-Weighted 0.7238** (outperforming the best Kaggle F1-Weighted benchmark (as of Nov 11 2025)), and **Quadratic Weighted Kappa (QWK) 0.7815**.
- **Kaggle notebook.** Executable version hosted at [Classification – Prenatal Care Decision Support](https://www.kaggle.com/code/diogonoglima/classification-prenatal-care-decision-support).

## Repository Structure
- `notebook0be4bc3a32.ipynb` — polished Kaggle-style notebook with narrative sections, visuals, and code.
- `relatorio.md` — Portuguese technical report detailing context, methodology, and discussion points that guided the notebook rewrite.

## Methodology Overview
1. **Problem framing.** Preserve the ordinal nature of `RiskLevel` (low, medium, high) and adopt healthcare-aware evaluation (QWK + F1-Weighted).
2. **Data validation.** Encode the target, remove duplicates (reducing the dataset to 452 unique patients), flag unrealistic ages (<13) and vitals (7 bpm heart rate), and document sensor quantization.
3. **Exploratory analysis.** Inspect univariate/bivariate patterns, highlight the dominance of low-risk cases, and connect age, blood pressure, and blood sugar to rising risk levels.
4. **Modeling.** Build cumulative classifiers for each ordinal threshold, using pipelines with optional scaling plus RandomizedSearchCV for hyperparameters.
5. **Evaluation.** Report accuracy, F1-Weighted, and QWK; visualize confusion matrices and feature importances to keep interpretations clinically grounded.

## Results and Benchmark Comparison
Our cumulative RandomForest delivered **F1-Weighted = 0.7238**, exceeding the published Weighted F1 scores of the following Kaggle references (links below), which were authored by domain experts, a Kaggle Master, and a Kaggle Grandmaster:

| Author & Role | Notebook | Highlight |
| --- | --- | --- |
| `csafrit2` (dataset expert) | [Predicting Pregnancy Risk Conditions](https://www.kaggle.com/code/csafrit2/predicting-pregnancy-risk-conditions) | Baseline reference shared by the dataset creator. |
| `yasserhessein` (Kaggle Master) | [Classification – Maternal Health (5 Algorithms)](https://www.kaggle.com/code/yasserhessein/classification-maternal-health-5-algorithms-ml) | Multi-algorithm benchmark; our F1-Weighted surpasses the reported scores. |
| `annastasy` (Kaggle Grandmaster) | [Pregnancy Risks – EDA & Modeling](https://www.kaggle.com/code/annastasy/pregnancy-risks-eda-modeling-hypothesis) | Grandmaster baseline; our cumulative approach edges out the weighted F1 reported there. |

## Reproducing the Notebook
1. Clone the repository and ensure Python 3.11 with `pip install -r requirements.txt` (or install pandas, seaborn, scikit-learn, xgboost manually).
2. Download the dataset from Kaggle (or place `Maternal Health Risk Data Set.csv` in the project root/Kaggle input directory).
3. Open `notebook0be4bc3a32.ipynb` (locally or on Kaggle) and run all cells sequentially. The notebook keeps consistent seeds so the reported metrics are reproducible.

## References
- Technical article: `relatorio.md` (Portuguese) — primary narrative source for the notebook.
- Kaggle notebook (Diogo): <https://www.kaggle.com/code/diogonoglima/classification-prenatal-care-decision-support>
- Kaggle baselines cited above.
- AHMED, M. Maternal Health Risk. UCI Machine Learning Repository, 2020. Disponível em: https://doi.org/10.24432/C5DP5D.
- BISHOP, C. M. Pattern Recognition and Machine Learning. Springer, 2006.
- HASTIE, T.; TIBSHIRANI, R.; FRIEDMAN, J. The Elements of Statistical Learning: Data Mining, Inference, and Prediction. 2. ed. Springer Science & Business Media, 2009.
- MEYER, M. D. E. The Cost of Winning the Pregnancy Lottery: An Autoethnographic Account of How My Life Was Consumed by Secondary Infertility. Journal of Autoethnography, 2022.
- LU, X. Prediction of Gestational Diabetes and Hypertension Based on Pregnancy Examination Data. Journal of Mechanics in Medicine and Biology, 2022.

