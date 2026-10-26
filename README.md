# Reducing Churn with Machine Learning
### GCI World 2026 — Final Assignment | Telecom Customer Retention

An applied data science project exploring telecom customer churn and proposing a proactive, model-assisted retention program. The work combines exploratory data analysis, feature engineering, an XGBoost classifier, held-out evaluation, and a scenario-based business proposal.

**Author:** Victoria Rodriguez Denis  
**Program:** GCI World 2026  
**Project date:** June 2026

## Executive summary

The assignment analyzes a telecom dataset described as containing approximately 100,000 customers and around 90 variables. The submitted report describes a churn rate of 49.6% (49,562 customers) and proposes prioritizing customers who are both at elevated churn risk and above-median revenue.

The business proposal maps plausible risk signals to targeted interventions: device upgrades, plan adjustments, and loyalty offers. A controlled experiment is recommended before real-world deployment.

### Results reported in the original final-assignment presentation

These are the figures in the submitted report, **not guaranteed outputs of the revised notebook**. The notebook's preprocessing and targeting workflow has been updated to improve evaluation integrity; run it with the authorized source data to regenerate metrics.

| Measure | Original report |
| --- | ---: |
| Dataset size | 100,000 customers |
| Customers who churned | 49,562 |
| Churn rate | 49.6% |
| Model | XGBoost |
| ROC-AUC | 0.695 |
| Accuracy | 63.8% |
| Recall for churn | 0.64 |
| High-risk, high-value segment | 13,574 customers |
| Monthly revenue represented by segment | USD 1.19M |
| Scenario net benefit over 24 months | USD 7.89M |
| Scenario ROI | 11.6× |

**Financial interpretation:** The original report's revenue and ROI values are scenario estimates based on assumptions, including a 30% retention rate and a 24-month revenue horizon. They are not measured incremental impact, verified net profit, or causal evidence that the campaign works.

## Research question

Can customer, usage, billing, and equipment features help prioritize telecom customers for proactive retention, and how can predictions be translated into a testable business intervention?

## Methodology

1. **Business framing** — define churn as a customer-retention challenge.
2. **Exploratory data analysis** — inspect data quality, target distribution, and feature patterns.
3. **Hypothesis development** — examine tenure, device age, overage usage/charges, and revenue signals.
4. **Feature engineering** — derive row-level indicators such as `overage_ratio`, `rev_per_mou`, and `rev_declining`.
5. **Preprocessing and modeling** — use a scikit-learn pipeline with numeric imputation and one-hot encoding, then train an XGBoost classifier.
6. **Evaluation** — evaluate predictions on a stratified held-out test set using classification metrics, ROC-AUC, average precision, confusion matrix, ROC curve, and feature importance.
7. **Business proposal** — demonstrate a high-risk/high-value targeting rule and an explicitly assumption-driven scenario.
8. **Validation plan** — use A/B testing, human review, and ongoing monitoring before deployment.

## Getting started

### Requirements

Python 3.10 or 3.11 is recommended. Install dependencies from the repository root:

```bash
python -m venv .venv
```

Windows PowerShell:
```powershell
.venv\Scripts\Activate.ps1
```

macOS / Linux:
```bash
source .venv/bin/activate
```

Then:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### Dataset setup

The notebook expects two authorized CSV files:

- `Client.csv`
- `Record.csv`

Both should include `Customer_ID`; `Record.csv` must also include a binary `churn` target encoded as `0` or `1`. Place the files in `data/` or the notebook's working directory. Read `data/README.md` before adding or redistributing data.

The source data is intentionally **not included** in this repository. Do not publish customer-level data unless its license and the provider's terms explicitly permit redistribution. Never publish personal or confidential information.

### Run the notebook

Open `notebooks/telecom_churn_analysis.ipynb` in JupyterLab, Jupyter Notebook, or Google Colab. Run cells in order. If you use the repository's `data/` folder, the notebook searches common working-directory locations automatically.

The notebook has been saved with outputs cleared. Metrics and plots appear after a successful run with the authorized dataset.

## Reproducibility and evaluation improvements

The revised notebook addresses key risks in the original draft:

- **Split before learned preprocessing:** imputation and encoding are fitted only on the training partition.
- **Pipeline-based transformations:** numeric imputation and categorical imputation/one-hot encoding are part of the model pipeline.
- **Unknown categories:** one-hot encoding ignores categories that were not present during training.
- **Held-out evaluation:** classification metrics are computed on a stratified test partition not used to fit preprocessing or the classifier.
- **Safer business demonstration:** the targeting and scenario sections use held-out test customers rather than using in-sample predictions across the entire dataset.
- **More complete metrics:** includes average precision in addition to accuracy, classification report, ROC-AUC, and confusion matrix.

These changes may produce metrics and business-segment sizes that differ from the original presentation. The updated notebook has not been executed against the source CSV files in this repository because those files were not supplied here.

## Limitations and responsible use

- The assignment dataset's reported churn rate (~49.6%) may not represent the real-world population. Absolute volume estimates need recalibration against representative production data.
- Predictive feature importance is not proof of causal churn drivers.
- A scenario that subtracts outreach costs from revenue does not necessarily represent profit: it may omit discounts, subsidized devices, service costs, and the counterfactual outcome.
- Retention uplift should be estimated with a randomized treatment/control experiment.
- Thresholds should be chosen based on campaign capacity, calibration, and the business costs of false positives and false negatives.
- Human review should remain part of the decision process.
- Verify data rights, privacy obligations, and applicable policies before any operational use.

## Technology

Python · pandas · NumPy · Matplotlib · Seaborn · scikit-learn · XGBoost · Jupyter

## References

The notebook's final section includes the project's market and business references, including Harvard Business Review, Tridens Technology, CustomerGauge, Statista, XGBoost documentation, scikit-learn documentation, and GCI World 2026 lecture materials. Check the notebook for the full bibliography.

---

*Educational project and proposed analytical workflow. Not a production-ready churn system.*
