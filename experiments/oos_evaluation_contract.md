# OOS Evaluation Contract — v1

## Purpose

This contract defines the minimum artifact required before any candidate trading model can produce a project-level performance claim.

## Required immutable row

Each decision timestamp must retain:

- `timestamp`
- `asset`
- `information_cutoff`
- `label_end`
- `fold_id`
- `model_id`
- `model_version`
- `prediction`
- `prediction_std_or_confidence`
- `position_target`
- `position_executed`
- `execution_timestamp`
- `price_reference`
- `turnover`
- `gross_return`
- `commission`
- `spread_cost`
- `slippage_cost`
- `market_impact_cost`
- `borrow_or_funding_cost`
- `net_return`

## Leakage invariants

1. `information_cutoff <= execution_timestamp`.
2. Every feature must be computable using information timestamped no later than `information_cutoff`.
3. Training observations must not overlap the evaluation label interval after applying the declared purge/embargo rule.
4. Any scaler, imputer, selector, feature transformer, calibrator, threshold, or portfolio parameter must be fit only inside the corresponding training/validation window.
5. Candidate selection cannot inspect the final holdout.
6. Data revisions and universe membership must be point-in-time where relevant.

## Cost protocol

Every candidate is evaluated at:

- baseline costs;
- 1.5x baseline costs;
- 2.0x baseline costs;
- liquidity-conditioned costs when liquidity data are available.

Execution timing is explicit. If execution occurs at the next bar, the next-bar price—not the signal-bar close—is used.

## Comparison protocol

Candidate and frozen baselines must share identical timestamps, universe, portfolio construction, risk scaling and execution assumptions. Report paired net-return differences rather than comparing standalone Sharpe ratios only.

## Required evidence before promotion

- corrected purged/embargoed OOS validation;
- immutable candidate-level artifact satisfying this contract;
- positive incremental net OOS utility versus the strongest frozen baseline;
- survival under 1.5x and 2x cost stress;
- dependence-aware confidence interval/test on paired differences;
- selection-adjusted evidence accounting for the full trial registry;
- stability across predefined regimes/subperiods;
- seed/model stochasticity analysis where applicable;
- no unresolved leakage or label-overlap violations.

## Failure rule

If any required artifact or invariant is missing, the result is `BLOCKED`, not `NEGATIVE` and not `PROMOTED`. No Sharpe, CAGR, alpha, or model-ranking claim should be treated as project evidence until the contract is satisfied.
