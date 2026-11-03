# Homework 6 — Decision Trees and Ensemble Learning

Car fuel efficiency (`fuel_efficiency_mpg`) with a decision tree, a random forest and XGBoost.
Notebook: [homework.ipynb](homework.ipynb). Run with scikit-learn 1.7.2 and xgboost 3.1.1:

```bash
uv run --no-project --with jupyter,pandas,numpy,scikit-learn==1.7.2,xgboost==3.1.1 jupyter notebook homework.ipynb
```

| Q | Question | Result | Answer |
|---|---|---|---|
| 1 | Split feature of a `max_depth=1` tree | `model_year <= 1997.5` | `model_year` |
| 2 | Random forest RMSE (`n_estimators=10`) | 1.8371 | 1.837 |
| 3 | Lowest RMSE among `n_estimators` 10/50/100/150 | 1.837 / 1.772 / **1.768** / 1.769 | 100 |
| 4 | Best `max_depth` by mean RMSE | 10: **1.7554**, 15: 1.7840, 20: 1.7882, 25: 1.7863 | 10 |
| 5 | Most important feature (among the 4) | vehicle_weight 0.204 | `vehicle_weight` |
| 6 | XGBoost `eta` 0.3 vs 0.1 | 1.8265 vs **1.7248** | 0.1 |

Note: with scikit-learn 1.9 the Q3 values become 1.770 (100) and 1.769 (150), which flips the answer to 150.
The options were computed with 1.7.2 (Q2 matches 1.837 exactly only with that version).
