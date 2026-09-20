# H122 — Single-Use Final Holdout and Multi-Gate Promotion

## Hypothesis

A candidate that survives a frozen development protocol and is evaluated exactly once on an untouched final holdout will show materially less apparent performance inflation than a candidate whose final period is repeatedly inspected during research. Promotion should require simultaneous statistical, economic, stability, and implementation gates rather than a single optimized score.

## Motivation

Recent 2026 research emphasizes that walk-forward window choices can materially affect apparent performance and that a single untouched out-of-sample evaluation is useful for preserving independence. Other recent work combines Deflated Sharpe Ratio, Probability of Backtest Overfitting, Superior Predictive Ability, minimum track-record requirements, and regime stability as complementary robustness gates rather than treating one backtest statistic as decisive.

## Test design

1. Freeze the candidate universe, feature definitions, model classes, hyperparameter ranges, execution assumptions, and development-period selection rules.
2. Split data into development windows, a locked validation layer, and one final holdout that is never inspected for candidate selection.
3. Use purging and embargo sized to the maximum forecast/label horizon; explicitly test that no training observation overlaps a final-test label interval.
4. Produce immutable final-holdout artifacts containing timestamp, prediction, target, position, turnover, realized return, every cost component, and model/version identifiers.
5. Evaluate each promoted candidate once on the final holdout. Do not use final-holdout results to tune thresholds, features, model class, cost assumptions, or portfolio construction.
6. Require all predeclared gates: positive incremental net utility versus frozen baseline; realistic-cost survival; cost-stress survival; stability across development folds; no leakage audit failure; and acceptable multiple-testing-adjusted evidence.
7. Record every failed candidate and every development trial so the effective search count is preserved.

## Primary outcome

The primary statistic is the candidate's incremental annualized net utility versus the frozen baseline on the untouched final holdout, together with a predeclared confidence interval or appropriate dependent-data uncertainty estimate.

## Secondary outcomes

- Deflated Sharpe Ratio / PBO where applicable.
- Break-even transaction cost.
- Cost-stress degradation at 1.5x and 2x baseline costs.
- Turnover and capacity diagnostics.
- Worst-fold and regime-level incremental utility.
- Seed/model-selection dispersion.
- Difference between development/validation and final-holdout performance.

## Falsification criteria

Reject H122's promotion protocol if repeated development decisions continue to materially alter final-holdout results, if final-holdout performance is required to choose among candidates, or if apparently strong candidates routinely fail the predeclared economic/stability gates despite passing a single statistical metric.

## Non-goals

This hypothesis does not claim that a particular model or strategy has alpha. It tests whether the research and promotion protocol prevents us from converting search luck into a false model-selection result.
