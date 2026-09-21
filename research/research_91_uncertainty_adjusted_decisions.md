# Research 91 — Uncertainty-Adjusted Trading Decisions

## Date
2026-09-22

## Research question
Does explicitly accounting for model uncertainty improve net out-of-sample trading performance relative to ranking assets/signals by point forecasts alone?

## Literature signal
A 2026 study, *Uncertainty-Adjusted Sorting for Asset Pricing with Machine Learning*, reports that sorting on uncertainty-adjusted prediction bounds can improve portfolio performance versus point-prediction sorting, with gains driven primarily by lower volatility and stronger effects for flexible ML models. This is currently preprint evidence, so it is a hypothesis generator rather than established evidence.

A 2026 *Financial Analysts Journal* paper, *Rethinking Variable Importance in Machine Learning*, provides complementary evidence that in-sample ML importance is unreliable and that economic restrictions plus out-of-sample evaluation are necessary. A 2026 Journal of Financial Markets paper on nonlinear parametric portfolio policies reports that autoregressive smoothing can reduce turnover and improve performance, highlighting a second mechanism by which uncertainty-aware decisions may help: reducing unstable position changes rather than improving raw forecasts.

## Proposed experiment
Hold the forecasting model, features, timestamps, folds, universe, and research budget fixed. Compare:

1. Point-estimate ranking/position sizing.
2. Uncertainty-adjusted ranking using a pre-specified prediction interval or ensemble dispersion.
3. Confidence-thresholded trading: trade only when expected edge exceeds an uncertainty-and-cost threshold.
4. A matched random-confidence placebo.
5. A simple non-ML baseline.

The confidence estimate must be generated without access to the test fold. If ensembles/seeds are used, every seed is retained; the best seed cannot be selected on OOS performance.

## Economic evaluation
The primary metric is net OOS utility after commission, spread, slippage, market impact and borrow/capacity costs where applicable. Report turnover, hit rate, gross return, net return, Sharpe/Sortino, drawdown, tail loss, and breakeven transaction cost.

Stress the execution layer at 1x, 1.5x and 2x baseline costs and with execution-lag perturbations. Report results by volatility/liquidity regime and by uncertainty bucket.

## Leakage controls
- Exact point-in-time feature availability.
- No test-fold fitting of scalers, uncertainty calibrators, thresholds, or portfolio rules.
- Purging and embargo based on the full label horizon.
- Immutable final OOS period.
- Explicit trial ledger for every confidence definition, threshold, model seed, and execution rule.
- Label-shuffled and random-confidence placebos.

## Promotion rule
The uncertainty-aware method is promoted only if its incremental net OOS utility over point-estimate trading is positive and economically material, survives all cost stresses, is not concentrated in one regime, and is robust across seeds. A reduction in volatility without improved net utility is not sufficient.

## Current status
Hypothesis generated; numerical result pending corrected purged/embargoed OOS runner and immutable execution ledger. Existing historical results remain untrusted until the repository's previously identified forward-label-overlap issue is resolved.
