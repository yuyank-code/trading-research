# H161 — Seed Stability and Incremental Decision Utility

**Status:** Registered
**Date:** 2026-09-22

## Hypothesis

A candidate trading model should demonstrate positive and stable paired OOS net decision utility relative to a frozen baseline across independent stochastic training/selection seeds. A positive result concentrated in a small subset of seeds is not robust evidence.

## Null

After realistic transaction costs, slippage, execution delay and leakage-safe validation, the candidate's paired OOS net utility is not reliably greater than the frozen baseline; any apparent advantage is attributable to seed variation or selection noise.

## Primary test

For each frozen candidate specification, evaluate >=10 independent seeds. Aggregate paired candidate-minus-baseline net utility without selecting the best seed. Report median, mean, dispersion, lower-tail seed performance and dependence-aware confidence intervals.

## Stress tests

- baseline transaction costs
- 1.5x transaction costs
- 2x transaction costs
- execution-delay stress
- turnover-matched placebo
- PIT information lineage
- purge/embargo for overlapping labels
- full search-budget accounting

## Promotion rule

No promotion if the advantage is seed-fragile, disappears under modest cost stress, or depends on post-hoc seed selection. Final untouched OOS remains locked until all upstream validation gates pass.

## Falsification

Reject H161 if the candidate's incremental net utility is unstable across seeds or fails to beat the frozen baseline after the prescribed economic and leakage controls.
