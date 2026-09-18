# H71 — Model Confidence Set and OOS Replication-Ratio Gate

## Motivation

A model that wins a backtest is not necessarily distinguishable from its competitors once model-selection uncertainty is accounted for. Recent work on in-sample versus out-of-sample Sharpe ratios finds that the OOS replication ratio deteriorates for more complex strategies built from many weak signals, while larger training samples improve replication. Model Confidence Set (MCS) methods provide a complementary way to avoid treating a single noisy winner as uniquely superior.

## Hypothesis

After identical causal feature construction, purged/embargoed validation, realistic execution costs, and a fixed search budget, the apparent winner will often not be statistically distinguishable from a simpler subset of candidate models.

## Pre-registered comparison

Candidate families:
- regularized linear baseline;
- tree/boosting model;
- sequence/deep model only if justified by available data.

For every candidate preserve the full OOS return series and evaluate:
- net Sharpe and Sortino;
- maximum drawdown and tail loss;
- break-even transaction cost;
- OOS/IS Sharpe replication ratio;
- Model Confidence Set at 10% and 5% where sample size permits;
- DSR, PBO, and family-level SPA/Reality Check;
- sensitivity to adverse execution costs and one-period execution delay.

## Success criterion

A more complex model is promoted only if it has a statistically defensible OOS advantage over the simpler baseline after the above corrections, and the advantage survives cost stress. If MCS cannot distinguish the winner from simpler models, prefer the simpler model.

## Failure condition

Any advantage that exists only in-sample, disappears after cost stress, is driven by one validation split, or is not distinguishable after multiple-testing/model-selection correction is classified as non-robust.

## Important limitation

This is a test protocol, not an empirical result. The repository currently lacks the frozen candidate-level OOS return matrix needed to calculate the statistics without introducing post-hoc selection.
