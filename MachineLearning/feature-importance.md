kaggle tutorial: https://www.kaggle.com/learn/machine-learning-explainability

## Permutation importance

https://www.kaggle.com/dansbecker/permutation-importance

关键点：Instead we will ask the following question: If I randomly shuffle a single column of the validation data, leaving the target and all other columns in place, how would that affect the accuracy of predictions in that now-shuffled data?

## partial dependence plots (PDP)

https://www.kaggle.com/dansbecker/partial-plots

To see how partial plots separate out the effect of each feature, we start by considering a single row of data. For example, that row of data might represent a team that had the ball 50% of the time, made 100 passes, took 10 shots and scored 1 goal.

We will use the fitted model to predict our outcome (probability their player won "man of the match"). But we repeatedly alter the value for one variable to make a series of predictions. We could predict the outcome if the team had the ball only 40% of the time. We then predict with them having the ball 50% of the time. Then predict again for 60%. And so on. We trace out predicted outcomes (on the vertical axis) as we move from small values of ball possession to large values (on the horizontal axis).

## SHAP （SHapley Additive exPlanations）

https://www.kaggle.com/dansbecker/shap-values

理论：
https://towardsdatascience.com/one-feature-attribution-method-to-supposedly-rule-them-all-shapley-values-f3e04534983d
