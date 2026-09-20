# Research 62 — CPCV as a Validation-Method Stress Test

## Research question

Does the project's model ranking and economic conclusion remain stable when purged/embargoed walk-forward validation is replaced by combinatorial purged cross-validation (CPCV), while holding the data, labels, candidates, execution model, costs, and search budget fixed?

## Literature

A 2024 *Knowledge-Based Systems* study compared out-of-sample testing methods in a controlled synthetic financial environment and reported that CPCV reduced backtest-overfitting risk relative to traditional methods, with lower Probability of Backtest Overfitting and stronger Deflated Sharpe statistics in that setting. This is useful methodological evidence, not proof that CPCV improves real trading performance.

Bailey, Borwein, López de Prado and Zhu's work on Probability of Backtest Overfitting motivates explicit treatment of split selection and repeated model comparison as sources of false discoveries. Bailey and López de Prado's Deflated Sharpe Ratio further motivates correcting selected Sharpe statistics for trial count and non-normal returns.

## Test design

Freeze:

- point-in-time data snapshot;
- feature definitions and availability timestamps;
- forward-label construction;
- candidate model implementations;
- transaction costs, spread/slippage and impact assumptions;
- position sizing and execution timing;
- benchmark set;
- trial ledger and search budget.

Change only the validation partition family:

- purged + embargoed walk-forward;
- CPCV with the same label-overlap purge and embargo logic.

The same candidate is not re-tuned for each validation family. Any such retuning is a new counted trial.

## Required artifact

For every candidate and validation path, preserve immutable rows containing at minimum:

`candidate_id, validation_method, train_start, train_end, test_start, test_end, decision_timestamp, feature_snapshot_id, prediction, realized_return, position, turnover, spread_cost, slippage_cost, impact_cost, net_return, random_seed, trial_id`.

## Primary analysis

Measure candidate-vs-baseline ranking agreement and the sign of incremental net OOS performance across the two validation families.

## Secondary analysis

Compute rank correlation, path-level dispersion, DSR/PBO/SPA where applicable, turnover, break-even cost, drawdown and regime stability.

## Interpretation

Agreement strengthens confidence that the conclusion is not an artifact of one split geometry. Disagreement is a robustness failure, not an invitation to choose the more favorable validation method.

## Current status

Protocol and artifact contract defined. Numerical evaluation is blocked until the repository contains immutable candidate-level OOS prediction/return records and the forward-label-overlap correction is validated.
