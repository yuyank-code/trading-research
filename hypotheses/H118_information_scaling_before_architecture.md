# H118 — Information Scaling Before Architecture Scaling

## Hypothesis

For a fixed candidate model class, increasing the amount of point-in-time training information will produce more stable out-of-sample net utility than increasing model size or architectural complexity, unless the larger model delivers statistically credible incremental utility after costs and search correction.

## Test

Compare:

- fixed architecture + 1x training history
- fixed architecture + 2x training history
- fixed architecture + maximum eligible history
- larger architecture + same training history

All variants use the same features, labels, folds, purge/embargo, execution lag, portfolio construction and cost model.

## Primary metrics

- net OOS Sharpe / downside risk
- cumulative net return
- maximum drawdown
- turnover and cost decomposition
- break-even transaction cost
- fold-level performance dispersion
- model-ranking stability
- DSR/PBO or equivalent search-adjusted evidence

## Falsification

Reject H118 if larger architecture consistently produces statistically credible incremental net OOS utility over the fixed architecture and information-scaled variants, survives cost stress and remains stable across predefined time/regime partitions.

## Leakage controls

- point-in-time data only
- fold-local preprocessing and feature selection
- explicit forward-label overlap purge
- embargo where required
- no tuning on final OOS
- immutable trial IDs and search ledger

## Status

Preregistered. No numerical result yet because immutable candidate-level OOS artifacts are still required.
