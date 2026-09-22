# H160 — Paired OOS Incremental Alpha vs Frozen Baselines

Date: 2026-09-22

## Hypothesis

After point-in-time reconstruction, corrected purge/embargo, realistic execution costs and a frozen portfolio construction layer, a candidate ML model should improve paired net economic utility versus the strongest pre-registered baseline, not merely exhibit a higher standalone Sharpe.

## Null hypothesis

The candidate has no positive incremental net utility versus the frozen baseline.

## Primary comparison

For every identical decision timestamp, compute candidate net return minus baseline net return. Use dependence-aware block/bootstrap inference on the paired differences. Apply search-aware inference over the full declared candidate family after the final holdout has been frozen.

## Stress tests

- baseline costs;
- 1.5x costs;
- 2.0x costs;
- liquidity-conditioned costs where available;
- execution-delay stress;
- turnover-matched placebo;
- predefined market/regime subperiods.

## Leakage controls

The experiment is BLOCKED unless information cutoff, label end, purge/embargo, feature fitting, universe membership and execution timestamps satisfy the project OOS contract.

## Promotion criterion

Promote only if incremental net utility is positive with dependence-aware uncertainty, survives 1.5x and 2x cost stress, remains economically meaningful across predefined subperiods, and passes selection-adjusted inference over the complete trial registry. Otherwise classify as BLOCKED or REJECTED according to which invariant failed.

## Expected falsifier

A candidate that wins on standalone Sharpe but loses the paired net-return test, collapses under cost stress, or fails search-adjusted inference falsifies the economic claim even if its raw backtest looks strong.

## Status

Registered; numerical test pending a complete PIT-clean executable dataset and candidate artifact satisfying the OOS contract.
