# H167 — Null Falsification and Injected-Signal Power

**Status:** Registered
**Date:** 2026-09-23

## Hypothesis

A valid trading-research workflow should not produce systematic net OOS alpha on controlled no-signal data, while it should recover a predefined injected signal under the same search, validation, execution and cost machinery.

## Design

Freeze the workflow before running the test. Apply the identical pipeline to:

- **A:** martingale/null returns;
- **B:** block-shuffled returns preserving local dependence;
- **C:** microstructure placebo data;
- **D:** a controlled injected-signal dataset with a predefined effect size.

Keep feature construction, scaling, model family, hyperparameter search budget, folds, purge/embargo, execution lag, transaction-cost model, slippage model and selection procedure identical.

## Primary endpoints

For A-C: distribution of paired net OOS utility, Sharpe, maximum drawdown, turnover and false-promotion rate across repeated datasets.

For D: power to recover the injected signal and preserve its sign under realistic costs.

## Required controls

- full trial ledger;
- no final-holdout tuning;
- realistic commissions, spread, slippage and impact;
- 1x / 1.5x / 2x cost stress;
- seed aggregation for stochastic candidates;
- paired candidate-minus-baseline inference;
- regime and implementation-sensitivity checks.

## Falsification

Reject the workflow if it repeatedly generates economically significant alpha on A-C. Reject the experimental implementation as underpowered or broken if it cannot recover D at the predefined effect size.

## Promotion rule

Historical strategy results remain non-promotable until the complete workflow passes both null falsification and injected-signal power checks.
