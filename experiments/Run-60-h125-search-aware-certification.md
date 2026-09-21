# Run 60 — H125 Search-Aware Certification

## Objective

Operationalize H125 without opening or tuning the final holdout.

## Required inputs

- corrected purged/embargoed OOS folds with forward-label overlap handled;
- immutable candidate prediction/position/turnover/realized-return/cost matrix;
- frozen strong baselines;
- complete research-trial ledger;
- fixed execution and liquidity-conditioned cost engine;
- null/placebo candidate set.

## Required outputs

- gross and net OOS performance by candidate and fold;
- incremental net utility versus each baseline;
- 1x/1.5x/2x cost stress;
- execution-lag sensitivity;
- search-aware significance metrics;
- candidate ranking before and after selection correction;
- null-workflow winner distribution;
- explicit promotion/block/reject decision.

## Hard stop

If any required input is missing, status is `BLOCKED` and no Sharpe/CAGR/alpha claim is reported as a project result.

## Current status

Blocked pending the immutable candidate-level OOS artifact and corrected forward-label-overlap validation. This run records the executable evaluation contract only; it does not create synthetic performance numbers.
