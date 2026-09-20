# H112 — CPCV vs Purged Walk-Forward Model-Ranking Stability

## Motivation

Controlled evidence comparing out-of-sample validation methods reports that combinatorial purged cross-validation (CPCV) can reduce backtest-overfitting risk relative to conventional validation in non-stationary financial settings. This is a validation-method hypothesis, not evidence that CPCV itself creates alpha.

## Hypothesis

If a candidate model has genuine and sufficiently persistent predictive value, its relative ranking against transparent baselines should remain broadly stable when evaluated with both the project's preregistered purged/embargoed walk-forward protocol and a preregistered CPCV protocol. Large ranking reversals concentrated in one validation method indicate sensitivity to split geometry and elevated model-selection risk.

## Null hypothesis

After realistic costs and multiple-testing adjustment, model rankings and incremental net economic conclusions do not materially differ between the two validation families; observed differences are sampling variation.

## Test

Use the same point-in-time dataset, feature definitions, labels, candidate implementations, execution model, cost/slippage assumptions, and trial ledger. Only the validation partitioning method changes.

Compare:

1. purged + embargoed walk-forward;
2. combinatorial purged cross-validation with the preregistered embargo/label-overlap rules.

Do not tune candidates separately for either validation family. Any additional configuration is a counted trial.

## Primary endpoint

Agreement of candidate-vs-baseline ranking by net OOS utility and benchmark-relative performance across validation families.

## Secondary endpoints

- rank correlation;
- sign agreement of incremental net alpha;
- DSR/PBO/SPA or equivalent multiplicity-adjusted evidence;
- dispersion across test paths;
- turnover and break-even cost;
- regime/subperiod stability.

## Failure criteria

Reject robustness if the apparent winner changes materially between validation families, if significance exists only under one split geometry, or if the preferred model loses its economic advantage after realistic costs.

## Promotion rule

Validation-method agreement is necessary but not sufficient. No candidate is promoted without immutable candidate-level OOS predictions/returns, corrected forward-label-overlap validation, complete trial accounting, and cost-aware economic evidence.

## Status

Protocol committed. Numerical evaluation remains blocked until the immutable candidate-level OOS artifact contract is satisfied.
