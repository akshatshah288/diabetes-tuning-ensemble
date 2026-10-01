# Diabetes Classifier: Tuning and Ensembling

Author: Akshat Shah

This assignment evaluates a baseline Decision Tree using five-fold cross-validation, tunes it with **both GridSearchCV and RandomizedSearchCV**, then compares it with a Random Forest ensemble on the same held-out test split.

## Source and data
Requested Kaggle page: https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database

That endpoint returned an access error during preparation. The actual CSV used is the public Pima mirror at https://github.com/npradaschnor/Pima-Indians-Diabetes-Dataset/blob/master/diabetes.csv . The supplied file contains 768 records, eight predictors and Outcome (0/1). It could not be byte-compared with the inaccessible Kaggle copy. The notebook displays its SHA256, also stored in outputs/experiment_settings.json. The downloaded CSV is unchanged.

Treat zeros in Glucose, BloodPressure, SkinThickness, Insulin and BMI as missing, following the corrected Pima convention documented at https://search.r-project.org/CRAN/refmans/mlbench/html/PimaIndiansDiabetes.html . Zeros in Pregnancies and Outcome are retained. Median imputation is fitted inside training-fold pipelines.

## Experiment
- 80/20 stratified train/test split, random_state=42: 614 training and 154 test records.
- Identical five-fold stratified CV splits for every model.
- Baseline: untuned Decision Tree.
- Grid search: 90 candidates, 450 CV fits plus final refit.
- Randomized search: 30 candidates sampled without replacement from the same 90-candidate space, 150 CV fits plus final refit.
- Ensemble: Random Forest with 300 trees, min_samples_leaf=2 and max_features=sqrt; fixed before evaluation, not tuned.
- Accuracy is the selection and evaluation metric. Model settings are not adjusted after inspecting test scores.

## Required results table
| Model | CV Accuracy | Test Accuracy | Best Params |
|---|---:|---:|---|
| Baseline Decision Tree | 67.26% | 68.18% | Fixed, not tuned: criterion=gini, max_depth=None, min_samples_split=2, min_samples_leaf=1 |
| Decision Tree - GridSearchCV | 74.43% | 68.83% | {"criterion": "gini", "max_depth": 3, "min_samples_leaf": 1, "min_samples_split": 2} |
| Decision Tree - RandomizedSearchCV | 74.43% | 68.83% | {"min_samples_split": 2, "min_samples_leaf": 1, "max_depth": 3, "criterion": "gini"} |
| Random Forest Ensemble | 76.87% | 74.68% | Fixed, not tuned: n_estimators=300, min_samples_leaf=2, max_features=sqrt, max_depth=None |

## Interpretation
Random Forest Ensemble had the highest mean training CV accuracy (76.87%) and achieved 74.68% on the held-out test set. The highest observed test accuracy was 74.68% for Random Forest Ensemble; this is a descriptive result from one split, not a reason to retune on the test set. Grid search evaluated 90 candidates and randomized search evaluated 30, illustrating the trade-off between exhaustive coverage and a smaller search budget.

Both searches found the same best Decision Tree configuration. Randomized search used one-third as many CV candidate fits in this run, but it could miss the optimum with a different sample. Random Forest's aggregation across randomized trees is consistent with improved performance here, though one small test split does not prove universal superiority.

Tuned CV accuracies are selected maxima from a search, whereas baseline and ensemble CV accuracies evaluate fixed configurations. They are not nested-CV estimates and can contain selection optimism. The untouched test set provides the separate generalization comparison.

## Run
Kaggle: import the notebook and attach a dataset containing diabetes.csv. Colab: upload the notebook and diabetes.csv using the Files sidebar. Local Jupyter: retain the directory structure, then run:

```bash
python -m pip install -r requirements.txt
jupyter notebook Diabetes_Tuning_Ensemble.ipynb
```

Run all cells in order. CPU is sufficient. No runtime internet access is needed once the CSV is attached. Saved outputs are included so the notebook can also be read without execution.

## Files
- Diabetes_Tuning_Ensemble.ipynb: executed notebook with baseline fold scores, both searches' best_params_/best_score_, ensemble evaluation and the single comparison table.
- data/diabetes.csv: source CSV used for the executed results.
- outputs/tuning_ensemble_results.csv and .md: the required four-column comparison.
- outputs/grid_search_trials.csv and randomized_search_trials.csv: all evaluated settings and scores.
- outputs/cv_fold_scores.csv: individual fold scores for the four entries.
- outputs/split_manifest.csv and test_predictions.csv: split membership and held-out predictions.
- outputs/experiment_settings.json: random seed, source hash, search spaces and fitted estimator settings.
- outputs/charts/: class distribution and CV/test accuracy comparison.
- outputs/conclusion.md: interpretation of results.
- DIABETES_SUBMISSION_GUIDE.md: steps for Kaggle, GitHub, Colab and submission.

Original data credit: National Institute of Diabetes and Digestive and Kidney Diseases; public mirror maintained by GitHub user npradaschnor. This project claims no ownership of the dataset and assigns it no new license. This is an educational experiment, not a clinical diagnostic tool.
