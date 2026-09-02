# Run 16 — Validation hardening and cost-aware evidence

Date: 2026-09-02

## Executive result

No new trading-edge claim is promoted in this run. The main progress is that the validation-harness repair is present as PR #4 in the model repository, while the model-selection protocol is being tightened around multiple-testing control and realistic execution costs.

## Repository audit

`yuyank-code/bitcoin-ml-trading` has PR #4 open (`fix/validation-harness`) against `main`. The patch fixes two previously identified defects in `validation.py`:

1. duplicate timestamps are counted before deduplication and become an explicit validation error;
2. the cost-stress adapter now calls the authoritative backtest using scalar `fee_bps` and `slip_bps` arguments instead of the incompatible `StressConfig` object.

The stress grid remains deterministic at 0.5x, 1x, 1.5x, 2x, and 3x baseline costs.

PR #4 is intentionally not treated as merged evidence until its tests/CI are verified. No performance result is inferred from the patch itself.

## Literature update

### Deflated Sharpe Ratio

Bailey and López de Prado (2014) show that selecting the best result from many backtests inflates apparent performance and propose the Deflated Sharpe Ratio to account for multiple testing and non-normal returns.

Implication: the project's 75 model/feature/threshold configurations cannot be judged solely by the largest observed Sharpe. The trial registry must include every configuration evaluated, including failures and discarded candidates.

### Probability of Backtest Overfitting / CSCV

Bailey, Borwein, López de Prado and Zhu (2017) propose combinatorially symmetric cross-validation to estimate the probability that a strategy selected in-sample will fail out-of-sample. This reinforces the requirement for a development selection period plus an untouched final holdout, rather than repeatedly selecting policies on the same OOS stream.

### Purging and embargo

Financial ML validation must remove training observations whose label spans overlap validation observations, with embargo used where residual serial dependence can contaminate adjacent samples. The project's fixed six-hour forward-return horizon is currently handled by the production research path through horizon-based purging, but future variable-horizon labels should be represented explicitly by event start/end times rather than by row counts.

### BTC/USDT cost-aware ML evidence

Bysik & Ślepaczuk (2026) evaluate roughly 70,000 hourly BTC-USDT observations across 27 walk-forward folds. Their results indicate that naive sign-based ML strategies can lose apparent profitability under 10 bps transaction costs, while a forecast-magnitude cost-aware filter can reduce turnover and recover profitability in selected configurations. They do not establish statistically significant dominance of one model family. This supports testing cost-aware abstention while treating it as a hypothesis, not an established edge.

## Testable hypotheses

- H35: the repaired validation harness produces zero duplicate-date validation errors on the canonical prediction artifact.
- H36: all selected OOS predictions can be reproduced byte-for-byte from a frozen code/data/version manifest.
- H37: cost-aware abstention remains beneficial when predictions are frozen and only execution thresholds vary.
- H38: the candidate's performance survives the full 0.5x–3x cost grid without selecting a favorable cost level after seeing results.
- H39: DSR/PBO-adjusted evidence remains positive after accounting for the complete trial registry.
- H40: the final untouched holdout agrees directionally with the development-period selection without any retuning.

## Promotion gate

A candidate is not promotable unless all are true:

1. no duplicate timestamps;
2. no train/test label-span overlap;
3. prediction features are timestamp-causal;
4. OOS predictions are frozen before policy selection;
5. execution costs are predeclared and stress-tested;
6. every tested configuration is registered;
7. final holdout is untouched until the policy is frozen;
8. fold-level results are available, not just pooled metrics;
9. DSR/PBO or an equivalent multiple-testing assessment is reported.

## Current conclusion

The research process is materially safer, but the project still lacks a verified immutable OOS artifact set from the repaired harness. Therefore no new Sharpe, CAGR, or profitability figure is promoted from this run.
