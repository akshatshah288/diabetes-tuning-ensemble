# Results comparison

| Model | CV Accuracy | Test Accuracy | Best Params |
|---|---:|---:|---|
| Baseline Decision Tree | 67.26% | 68.18% | Fixed, not tuned: criterion=gini, max_depth=None, min_samples_split=2, min_samples_leaf=1 |
| Decision Tree - GridSearchCV | 74.43% | 68.83% | {"criterion": "gini", "max_depth": 3, "min_samples_leaf": 1, "min_samples_split": 2} |
| Decision Tree - RandomizedSearchCV | 74.43% | 68.83% | {"min_samples_split": 2, "min_samples_leaf": 1, "max_depth": 3, "criterion": "gini"} |
| Random Forest Ensemble | 76.87% | 74.68% | Fixed, not tuned: n_estimators=300, min_samples_leaf=2, max_features=sqrt, max_depth=None |

CV Accuracy is mean training-only five-fold accuracy. Tuned scores are search-selected; see notebook for the selection-bias caveat.
