# Research 84 — Breakeven Transaction Cost as a Model-Selection Objective

## Date
2026-09-21

## Question
Can selecting models by their estimated breakeven transaction cost produce more robust out-of-sample trading performance than selecting by gross Sharpe or gross return?

## Literature signal
The 2026 large-scale deep-learning futures benchmark evaluates models not only by Sharpe, but also by breakeven transaction-cost buffers, downside/tail risk, statistical significance, seed robustness, and computational efficiency. Its framing is useful because gross risk-adjusted performance can hide how little execution friction a strategy can tolerate. The benchmark reports that some sequence models have materially larger breakeven-cost buffers than models that rank similarly on conventional metrics.

A separate 2026 Bitcoin walk-forward study finds that naive sign-based trading can become uneconomic at 10 bps, while a cost-aware execution filter can improve turnover and selected net results. This suggests that the economic margin above costs is itself a first-class object of study, not merely a post-hoc sensitivity check.

The 2026 GT-Score work also argues for multi-dimensional objectives incorporating performance, significance, consistency, and downside risk to reduce optimization overfitting. We treat its empirical claims as preliminary because it is an arXiv preprint, but the design principle is directly testable.

## Proposed experiment
For every candidate produced by a fixed research budget, calculate:

1. gross Sharpe;
2. net Sharpe under the base cost model;
3. breakeven proportional transaction cost;
4. breakeven spread/slippage multiplier;
5. performance stability across OOS folds;
6. maximum drawdown and tail loss;
7. seed sensitivity where applicable.

Compare model selection rules:

- gross-Sharpe winner;
- base-cost net-Sharpe winner;
- breakeven-cost winner;
- a pre-specified composite robustness score.

The selection rule must be frozen before the final OOS period is opened. All thresholds are estimated only inside training/validation data.

## Required controls
- point-in-time data;
- purging/embargo for overlapping labels;
- fold-local preprocessing and feature selection;
- complete trial ledger;
- matched-capacity placebo/search control;
- commission, spread, slippage, market impact, borrow and turnover where applicable;
- 1x, 1.5x and 2x cost stress;
- execution-lag perturbation;
- regime/tail subperiods;
- untouched final OOS;
- selection-aware inference.

## Falsification criterion
If breakeven-cost selection does not improve final-OOS net utility or robustness relative to gross-Sharpe selection, the hypothesis is rejected. A larger breakeven buffer alone is not sufficient if it comes with materially lower OOS utility.

## Status
Hypothesis-generating. No numerical alpha claim is made until the corrected OOS execution artifact exists.
