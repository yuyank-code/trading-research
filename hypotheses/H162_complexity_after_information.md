# H162 — Complexity After Information

**Status:** Registered / numerical test blocked

## Claim

With a fixed point-in-time information set, fixed effective sample size, and fixed execution contract, higher model/feature complexity should not be credited unless it improves paired net OOS utility and survives search-aware validation and stochastic-seed aggregation.

## Null

Complexity adds no reliable incremental net OOS utility over a strong shrinkage/regularized baseline.

## Alternative

At least one higher-capacity model delivers positive incremental net OOS utility that survives 1.5x and 2x costs, predefined regime checks, seed aggregation, and selection-adjusted inference.

## Design

Freeze the PIT dataset, folds, embargo, execution timing, universe, risk scaling and cost model. Compare regularized linear, tree-based nonlinear, sequence and higher-capacity attention models. Log every trial and prohibit final-holdout tuning.

## Required outputs

Immutable row-level candidate artifact, paired net-return differences, cost-stress table, seed distribution, regime/subperiod table, leakage audit, and search-aware inference.

## Falsification

Reject H162's null only if the incremental advantage is robust to the complete pre-registered validation stack. A higher standalone Sharpe or lower prediction error is insufficient.
