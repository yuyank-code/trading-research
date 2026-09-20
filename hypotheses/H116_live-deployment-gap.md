# H116 — Live-Deployment Gap and Predictive-to-Economic Decoupling

## Status
Pre-registered protocol. Not tested yet.

## Motivation
Recent 2026 research reinforces that predictive accuracy and backtest profitability are not interchangeable. A large financial time-series benchmark evaluates models with out-of-sample returns, statistical significance, tail risk, break-even transaction costs, random-seed robustness, and computational efficiency rather than prediction metrics alone. A separate 2026 Bitcoin study reports that naive sign-based ML trading loses profitability under 10 bps transaction costs while cost-aware forecast-magnitude filtering can materially reduce turnover. A 2026 empirical asset-pricing study also finds that research-design choices materially change ML portfolio results and that in-sample variable importance is unreliable.

## Falsifiable hypothesis
After fixing the information set, validation geometry, portfolio construction, and execution model, improvements in forecast metrics (e.g. MSE, directional accuracy, rank IC) will not reliably translate into improvements in net OOS portfolio utility once realistic trading frictions are applied.

## Experiment
For each candidate model and each OOS decision date, persist:
- timestamp and information-set cutoff;
- forecast and forecast uncertainty if available;
- realized forward return;
- position/weight before and after rebalance;
- turnover;
- spread, commission, slippage and impact components;
- gross and net return;
- model seed and immutable trial ID.

Evaluate candidates against a frozen transparent baseline. Report both predictive and economic metrics. Do not rank models on predictive metrics alone.

## Required robustness checks
1. Point-in-time feature availability audit.
2. Purged/embargoed validation with corrected forward-label overlap.
3. Immutable candidate-level OOS prediction/return matrix.
4. Complete trial ledger including discarded/failed trials.
5. Cost grid: reference, 1.5x, 2x and 3x.
6. Execution-lag perturbation.
7. Predefined regime/subperiod analysis.
8. Null/placebo workflow with the same search process.
9. Seed stability for stochastic candidates.
10. Benchmark comparison using the same portfolio and cost engine.

## Promotion rule
No candidate is promoted unless its incremental **net** OOS utility over the frozen baseline survives the pre-specified cost grid, leakage audit, null calibration, multiple-testing correction, and robustness perturbations. A better forecast metric without better net OOS economics is a negative result for the trading objective.

## Current blocker
The repository does not yet contain the immutable candidate-level OOS prediction/position/realized-return/cost matrix required to execute this test. Historical model-performance claims therefore remain untrusted until that artifact exists.
