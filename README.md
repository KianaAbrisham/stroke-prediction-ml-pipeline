# Stroke Classification: a scikit-learn Pipeline Example

An executed tabular classification example demonstrating preprocessing, imbalanced-class evaluation
and model selection. The included **200-row synthetic CSV** is for software demonstration;
its metrics do not establish stroke prediction performance on patient data.

## Workflow

1. Reserve a stratified 25% test split before model selection.
2. Use a ColumnTransformer for numeric imputation/scaling and categorical imputation/one-hot encoding.
3. Compare class-weighted logistic regression and random forest with up to five stratified cross-validation folds
   on the training split (five for the included demo). Preprocessing is fitted inside each fold.
4. Select the model by mean cross-validation **average precision** and evaluate it on the reserved test split.
5. Report average precision, ROC-AUC, a precision–recall curve, a confusion matrix and a classification report.
6. Inspect permutation importance of the original input columns as a diagnostic of the selected model.

Average precision is the scikit-learn metric used here; it is not a trapezoidal integral under
the precision–recall curve. Test-set permutation importance is descriptive and should not be used
to select features or tune the model while continuing to call that set an untouched final evaluation.

## Files and data

- [notebooks/stroke_pipeline.ipynb](notebooks/stroke_pipeline.ipynb): executed workflow and figures.
- [data/sample.csv](data/sample.csv): synthetic example, not patient records.
- [requirements.txt](requirements.txt): notebook dependencies.

For your own dataset, place a CSV at `data/stroke.csv` and set `use_demo = False` in the notebook.
Expected columns include `gender`, `age`, `hypertension`, `heart_disease`, `ever_married`,
`work_type`, `Residence_type`, `avg_glucose_level`, `bmi`, `smoking_status` and binary target `stroke`.
An optional `id` column is excluded from predictors. Check label quality and ensure enough examples
of both classes for the split and cross-validation. Repeated patients or time-dependent observations
require a suitable group or temporal split instead of this independent-row demonstration.

## Run locally

From the repository folder, create a separate environment:

```bash
python -m venv .venv
```

Activate with `.venv\Scripts\activate` in Windows Command Prompt or
`source .venv/bin/activate` on Linux/macOS, then run:

```bash
python -m pip install -r requirements.txt
jupyter notebook notebooks/stroke_pipeline.ipynb
```

The saved notebook contains outputs from the synthetic example. Performance on another dataset,
calibration, subgroup behavior and prospective clinical usefulness have not been established.

## About this example

The workflow was revised and executed with AI coding assistance. Its purpose is to demonstrate how preprocessing, cross-validation, and average-precision-based selection fit together when the positive class is uncommon. The supplied data are synthetic, and the recorded outputs cover that demonstration.

## License

MIT — see [LICENSE](LICENSE).
