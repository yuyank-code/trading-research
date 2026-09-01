# Model Selection and Search Budget — 2026-09-01

## Research update

Additional literature review reinforces two points that directly affect the current BTC/USDT ML project.

Gu, Kelly & Xiu (Review of Financial Studies, 2020) find that trees and neural networks can improve empirical asset-pricing forecasts by capturing nonlinear predictor interactions, while momentum, liquidity and volatility remain dominant information sources. This supports testing nonlinear models, but does not justify assuming that a nonlinear model will transfer to a single-asset crypto strategy. [DOI: 10.1093/rfs/hhaa009]

Bailey & López de Prado (Journal of Portfolio Management, 2014) show that selection among many backtests inflates the apparent Sharpe ratio and motivate the Deflated Sharpe Ratio as a correction for multiple testing, non-normality and finite samples. [DOI: 10.3905/jpm.2014.40.5.094]

## New methodological finding

The project should treat the **research search space as an experimental variable**. A model result cannot be evaluated independently of how many related specifications were tried.

Therefore each candidate family must have a declared search budget before evaluation:

- feature groups included
- model family
- hyperparameter ranges
- prediction horizon
- decision threshold range
- stop/target rules
- position sizing rule
- transaction-cost assumptions
- maximum number of experiments

All trials, including failures, should be retained in the trial registry.

## New hypotheses

### H13 — Nonlinear incremental value
A shallow tree/boosting model improves untouched OOS net performance over a frozen linear benchmark after identical costs and leakage controls.

### H14 — Complexity efficiency
Any incremental OOS improvement from a nonlinear model remains economically meaningful after accounting for additional model/search complexity.

### H15 — Cost-aware ranking
The model with the best predictive metric is not necessarily the model with the best net portfolio performance; candidate ranking should therefore be based on net OOS economics, not AUC alone.

### H16 — Threshold stability
A valid trading edge should survive a neighborhood of decision thresholds rather than exist only at one optimized cutoff.

## Required experiment

The next controlled comparison should use the same point-in-time feature matrix and identical chronological splits:

1. frozen logistic/linear baseline
2. shallow gradient/tree model
3. shallow regularized neural model

No candidate may tune against the final OOS period.

For every candidate, report:

- probability calibration
- AUC / Brier / log loss
- gross return
- net return
- CAGR
- maximum drawdown
- Sharpe / Sortino
- turnover
- number of trades
- cost sensitivity
- performance by regime
- threshold sensitivity
- feature-group ablation
- search-trial count
- DSR/selection-adjusted evidence where sample size permits

## Leakage gate

The project previously identified a forward-label overlap problem around walk-forward boundaries. The corrected pipeline must purge observations whose **label event interval overlaps the test interval**, not merely remove an arbitrary number of rows. An embargo should then remove observations immediately following the test interval when dependence can persist.

## Cost gate

Do not rely on one optimistic cost assumption. Evaluate a conservative grid around the base estimate for fees, spread and slippage. A candidate that survives only under the lowest cost scenario is not robust evidence.

## Promotion rule

No candidate becomes the project's authoritative model solely because it has the highest backtest return or Sharpe. Promotion requires:

1. leakage-safe chronological validation;
2. frozen final OOS evaluation;
3. realistic cost/slippage sensitivity;
4. threshold and parameter neighborhood stability;
5. comparison with strong simple baselines;
6. explicit accounting of the number of research trials;
7. no material evidence that selection bias explains the result.

## Current conclusion

There is **no new confirmed trading edge in this update**. The robust progress is methodological: the model search is now explicitly constrained so that nonlinear ML can be tested without allowing the research process itself to become the source of the apparent edge.

## Sources

- Gu, S., Kelly, B., Xiu, D. (2020), *Empirical Asset Pricing via Machine Learning*, Review of Financial Studies 33(5), 2223–2273. DOI 10.1093/rfs/hhaa009.
- Bailey, D.H., López de Prado, M. (2014), *The Deflated Sharpe Ratio: Correcting for Selection Bias, Backtest Overfitting, and Non-Normality*, Journal of Portfolio Management 40(5), 94–107. DOI 10.3905/jpm.2014.40.5.094.
