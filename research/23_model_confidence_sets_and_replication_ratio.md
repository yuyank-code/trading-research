# Research 23 — Model Confidence Sets and OOS Replication

## Literature synthesis

Bailey, López de Prado and coauthors show that selecting the best strategy from many alternatives creates backtest-overfitting risk; PBO and DSR were developed specifically to quantify selection effects. Harvey and Liu likewise argue that trading-strategy evaluation must account for the number of tests performed rather than interpreting an isolated Sharpe ratio.

More recent work by Mulligan, Jacquier and Muhle-Karbe (2025 revision) derives an approximation for the gap between in-sample and out-of-sample Sharpe ratios for linear predictive strategies. Their central result is relevant to this project: replication deteriorates as the number of assets/signals and weak predictors grows, while more training data improves replication.

A separate literature on Model Confidence Sets (Hansen et al.; later applications to trading-model selection) provides a useful decision rule: do not force a single winner when the data cannot statistically distinguish several candidates.

## Pipeline implication

Our evaluation should therefore retain candidate-level OOS returns instead of storing only the selected model's metrics. The selection layer must be evaluated separately from the prediction layer.

The required order is:
1. freeze the feature and label definitions;
2. generate predictions using only information available at each timestamp;
3. create candidate-level OOS returns under identical execution assumptions;
4. compute IS/OOS replication ratios;
5. apply MCS/SPA/Reality Check plus DSR/PBO where appropriate;
6. apply cost and execution stress;
7. reserve a final untouched confirmation period for the surviving family.

## Current evidence status

No empirical promotion is claimed. The frozen candidate-level OOS return matrix is still required before numerical MCS or replication-ratio conclusions can be produced.

## Sources

- Bailey et al., *Pseudo-Mathematics and Financial Charlatanism* (2014).
- Bailey & López de Prado, *The Deflated Sharpe Ratio* (2014).
- Bailey et al., *The Probability of Backtest Overfitting* (2015/2016).
- Harvey & Liu, *Evaluating Trading Strategies* (2014).
- Mulligan, Jacquier & Muhle-Karbe, *In-Sample and Out-of-Sample Sharpe Ratios for Linear Predictive Models* (2025 revision).
