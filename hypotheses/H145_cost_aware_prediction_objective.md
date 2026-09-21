# H145 — Cost-Aware Prediction Objective vs Gross-Return Prediction

## Claim

A model trained or selected using a point-in-time estimate of the tradable net edge should outperform an otherwise identical model trained on gross returns and charged costs only after execution.

## Why it is testable

Transaction costs are state-dependent. If spread, liquidity, volatility and expected impact contain information about whether a forecast is economically tradable, a model that sees those variables at decision time should be able to avoid economically marginal predictions. But the same variables can also create leakage if future realized execution conditions are used.

## Controlled arms

- A: gross-return target; ex-post realistic costs.
- B: point-in-time net-return target.
- C: gross-return target with cost-aware threshold.
- D: gross-return target with matched-noise cost covariates.

## Controls

Hold constant:
- exact point-in-time information timestamps;
- purged/embargoed walk-forward folds;
- final untouched OOS period;
- model class and search budget;
- execution simulator;
- commission, spread, slippage and impact assumptions;
- liquidity/capacity constraints;
- random-seed reporting.

## Primary metric

Median outer-OOS net utility after all modeled costs, with uncertainty intervals. Secondary metrics: turnover, breakeven cost, downside risk, fold consistency, seed consistency and capacity.

## Stress tests

- 1x / 1.5x / 2x transaction-cost assumptions
- execution lag perturbations
- liquidity buckets
- regime/tail periods
- matched-noise placebo
- shuffled-label placebo

## Leakage guard

Cost covariates must be lagged or forecast from data available before the trading decision. Realized future spread, volume, slippage or market impact may not enter either target construction or feature computation.

## Decision rule

Do not promote based on a single fold, seed or gross-return metric. A positive result must beat the strong baseline and placebo controls and remain economically meaningful under cost stress.

## Status

Pending implementation after the corrected forward-label-overlap validation layer is operational.
