# H70 — Complexity Premium Audit

## Question
Does additional nonlinear model complexity produce incremental, leakage-safe, cost-aware out-of-sample trading value over a simple baseline when the feature set, information set, validation schedule, search budget, and execution model are held fixed?

## Motivation
Recent evidence in *The Review of Financial Studies* (2025), "Man versus Machine Learning Revisited," reports that a previously published machine-learning trading result disappeared after correcting look-ahead bias, with linear models remaining competitive. This makes model complexity itself a testable hypothesis rather than an assumption of superiority.

## Pre-registered comparison

Compare a fixed baseline ladder:

1. regularized linear/logistic model;
2. random forest;
3. gradient-boosted trees;
4. one neural candidate only if justified by the same feature horizon and sample size.

All candidates must use:

- identical point-in-time features;
- identical labels and horizon;
- identical purged/embargoed walk-forward folds;
- identical hyperparameter-search budget per model family;
- identical cost, spread, slippage and impact model;
- identical abstention/sizing rules unless those rules are themselves frozen before comparison.

## Primary test

For each model family record every trial, then evaluate the selected configuration on untouched OOS data. The complexity premium is the incremental **net** OOS performance over the linear baseline, not gross prediction accuracy.

Required outputs:

- net OOS Sharpe and Sortino;
- annualized return and maximum drawdown;
- turnover and break-even cost;
- OOS rank stability across folds;
- DSR and PBO;
- SPA/Reality Check at the model-family level;
- seed/re-fit stability where stochastic models are used;
- adverse cost stress of +25%, +50%, +100%.

## Falsification criteria

Reject a complexity claim if the nonlinear model:

- loses its incremental net OOS edge after realistic costs;
- wins only in the development sample;
- requires materially larger search to obtain its apparent advantage;
- is unstable across folds/seeds;
- fails the multiple-testing gates;
- or is indistinguishable from the simple baseline within uncertainty.

## Leakage controls

No scaling, feature selection, imputation, dimensionality reduction, target encoding, threshold choice, or hyperparameter selection may use future observations. Model selection must occur strictly inside the development layer; the final confirmation period is never used for selection.

## Interpretation

A finding that a simple model matches or beats a complex model is a positive research result: complexity has failed to earn its place. A complex model wins only if the incremental advantage survives untouched OOS testing, costs, stress tests, and multiple-testing controls.

## Status

Pre-registered hypothesis. No empirical pass or promotion until the frozen OOS prediction/return matrix is available.
