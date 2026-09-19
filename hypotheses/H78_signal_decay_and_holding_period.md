# H78 — Signal Decay and Holding-Period Robustness

## Hypothesis
A predictive signal should have a measurable, economically coherent decay profile. If apparent trading alpha exists only at one narrowly selected holding period, the result is more likely to reflect horizon-specific noise, leakage, or backtest selection.

## Test
For a frozen feature set and frozen model specification, evaluate a pre-registered holding-period grid (short, medium, and longer horizons) without selecting the best horizon on the confirmation set.

For every horizon, preserve the complete OOS return series and report:
- net Sharpe and Sortino;
- max drawdown and tail losses;
- turnover and holding-time distribution;
- break-even transaction cost;
- performance degradation under adverse slippage/impact;
- fold-by-fold sign consistency;
- DSR/PBO and SPA/Reality Check across the entire horizon family.

## Leakage controls
- Features must be timestamped at or before decision time.
- Label end times must be explicit and used for purging.
- Overlapping labels require purge intervals at least as long as the maximum tested horizon.
- Embargo length is fixed before looking at confirmation results.
- The confirmation block is never used to choose the holding period.

## Robustness / falsification
Compare the observed decay curve with matched-count randomized signals and synthetic zero-alpha controls. A credible signal should show a stable economic region rather than an isolated winning horizon.

## Promotion rule
No horizon is promoted solely because it has the highest OOS Sharpe. Promotion requires economically meaningful net performance, stability across chronological folds, realistic cost survival, and statistical evidence that accounts for testing the complete horizon family.

## Status
Pre-registered research hypothesis. No empirical pass and no model promotion until the frozen candidate-level OOS prediction/return matrix is available.
