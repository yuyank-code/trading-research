# H123 — Incremental Signal Value vs. Strong Baselines

Date: 2026-09-21

## Hypothesis

A candidate ML forecast should only be considered economically useful if it adds statistically and economically meaningful **incremental net OOS utility** over a strong, frozen non-ML baseline using the same universe, portfolio construction, risk normalization, rebalance schedule, and execution-cost model.

## Motivation

Recent 2026 evidence shows that sophisticated ML pipelines can produce risk-adjusted performance that is largely attributable to portfolio construction, covariance regularization, or shrinkage rather than predictive content. A leak-free large-cap US equity benchmark reported that its best promoted ML model only marginally exceeded a no-ML Black-Litterman baseline while incurring more than three times cumulative transaction costs; an equal-weight baseline was also close in Sharpe. This makes baseline attribution a first-class promotion gate rather than a secondary comparison.

A separate large-scale futures benchmark finds some deep temporal models outperform linear baselines, but it evaluates significance, tail risk, break-even costs, seed robustness, and computational efficiency. Therefore this hypothesis is deliberately two-sided: ML may add value, but the burden is to demonstrate incremental value under identical economics.

## Test design

For each candidate model, compare against frozen baselines:

1. equal-weight / risk-parity baseline where applicable;
2. simple momentum or trend baseline using only information available at decision time;
3. no-ML portfolio-construction baseline with identical covariance/risk machinery;
4. candidate ML forecast with identical downstream construction.

Keep universe, rebalance timing, target horizon, position limits, volatility target, execution lag, cost model, and OOS folds identical.

## Primary metric

Incremental net OOS utility versus the strongest frozen baseline, measured on the same timestamps after commissions, spread, slippage, impact, borrow/funding where applicable.

## Secondary metrics

- paired OOS return difference;
- block-bootstrap confidence interval;
- Sharpe difference with dependence-aware inference;
- turnover and gross-to-net decay;
- maximum drawdown and tail loss;
- break-even transaction cost;
- seed dispersion for stochastic models;
- feature/model ablation;
- incremental value by regime and subperiod.

## Falsification criteria

Reject H123 if any of the following holds after multiplicity control:

- ML does not beat the strongest baseline on net OOS utility;
- the apparent gain disappears under realistic or stressed costs;
- the gain is concentrated in one short subperiod;
- the gain disappears across independent random seeds;
- the gain is explained by downstream portfolio construction rather than the forecast;
- the model requires a post-OOS choice to retain the advantage.

## Leakage and selection controls

Use point-in-time data, corrected forward-label-overlap purging/embargo, frozen feature-generation versions, and a single-use final holdout. Baseline and candidate must consume exactly the same information set and execution convention.

No candidate can be promoted merely because it beats a weak baseline.

## Status

Protocol/hypothesis only. The repository does not yet contain the immutable candidate-level OOS prediction/position/realized-return/cost matrix required to run this comparison credibly.
