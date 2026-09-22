# H148 — Incremental ML Complexity vs Shrinkage Baseline

## Hypothesis

A nonlinear ML forecasting layer improves net out-of-sample trading utility beyond a strong shrinkage/risk-controlled baseline after realistic trading costs and multiple-testing controls.

## Null

Any apparent improvement from ML is fully explained by shrinkage, portfolio construction, turnover reduction, or research-selection effects.

## Test arms

A. Strong linear/shrinkage baseline.
B. Same portfolio construction + nonlinear ML forecast.
C. Same as B + pre-specified cost-aware trading threshold.
D. Matched-complexity placebo using shuffled labels / null data.

## Primary metrics

- net OOS Sharpe and certainty-equivalent return;
- incremental net return vs baseline;
- breakeven transaction cost;
- turnover and capacity;
- downside/tail metrics;
- seed distribution for stochastic models.

## Falsification gates

- exact point-in-time information set;
- purged/embargoed OOS;
- untouched final OOS;
- 1x/1.5x/2x cost stress;
- execution-lag stress;
- null-workflow tests;
- effective trial count and multiple-testing adjustment.

## Promotion criterion

Only promote if C or B shows persistent incremental net OOS utility versus A, remains positive under cost stress, is not reproduced by the null controls, and is not dependent on a single seed, regime, or selected horizon.

## Status

Protocol added 2026-09-22. No numerical result is claimed until the corrected validation pipeline is executable and the forward-label-overlap issue is resolved.
