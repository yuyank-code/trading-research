# Research 54 — Benchmark-Relative Incremental Alpha

## Date

2026-09-20

## Objective

Determine whether a candidate ML trading signal contains economically meaningful information beyond transparent systematic benchmarks, rather than merely rediscovering known factor exposures.

## Literature synthesis

### Gu, Kelly & Xiu (2020), Review of Financial Studies

Their asset-pricing framework uses machine learning to estimate the nonlinear relationship between firm characteristics and expected returns. The broader lesson for this project is that strong predictive models do not automatically imply novel tradable alpha: the relevant object is the out-of-sample economic payoff after portfolio formation and implementation.

### Interacting Anomalies, Review of Asset Pricing Studies

The study directly compares a simple recursively selected out-of-sample anomaly strategy with published ML anomaly strategies. The reported correlation between strategies and the reduction in alpha after adding the ML strategy as a benchmark show why raw strategy returns are insufficient for attribution. This motivates testing incremental alpha against strong, frozen benchmarks.

### Microstructure in the Machine Age, Review of Financial Studies

Microstructure variables can have substantial explanatory power without necessarily having equivalent predictive power. The distinction reinforces the need to evaluate realized OOS trading performance rather than in-sample feature importance or contemporaneous fit.

### Thousands of Alpha Tests, Review of Financial Studies

Large-scale alpha research requires explicit multiple-testing control. A benchmark-comparison layer must therefore be included in the research ledger rather than treated as an after-the-fact robustness check.

### 2026 evidence on predictive versus trading performance

A 2026 working paper evaluating 1,100 U.S. equity mutual funds reports high contemporaneous out-of-sample explanatory power from ML models but no forward trading strategy surviving multiple-testing adjustment. This is directly relevant to the project's distinction between explaining returns and predicting investable returns.

## New testable implication

A candidate should be considered more credible if its net OOS return remains economically meaningful after neutralizing or attributing exposure to frozen transparent benchmarks. Conversely, a candidate whose apparent performance disappears after benchmark controls has not demonstrated independent alpha.

## Experiment design

The experiment will use a frozen prediction stream and construct three return series:

- candidate portfolio;
- transparent baseline;
- candidate residual/benchmark-adjusted component.

The benchmark model is estimated recursively using only data available at each decision time. No full-sample factor loadings are permitted.

The same OOS dates, transaction-cost model, slippage model, impact assumptions, borrow assumptions, turnover limits and capacity constraints are used throughout.

The experiment must preserve a complete candidate-by-date matrix so benchmark adjustment cannot be performed only on the selected winner.

## Required statistical checks

- corrected forward-label-overlap validation;
- purged/embargoed OOS splits;
- placebo and null-workflow tests;
- complete seed and trial ledger;
- Deflated Sharpe Ratio;
- Probability of Backtest Overfitting;
- SPA / Reality Check where applicable;
- Model Confidence Set where applicable;
- power and minimum-detectable-edge analysis;
- cost and latency frontier;
- regime/subperiod stability;
- benchmark sensitivity fixed before confirmation.

## Expected outcomes

### Positive

Residual net OOS performance remains economically material across confirmation windows and survives multiplicity, cost and placebo gates.

### Negative

The candidate's apparent edge is substantially absorbed by transparent benchmark exposures or vanishes after implementation costs.

### Inconclusive

Results depend materially on benchmark choice, confirmation window or execution assumptions without a pre-specified economic explanation.

## Current conclusion

No numerical conclusion is available in this run. The repository still requires the immutable candidate-level OOS prediction/return matrix and corrected forward-label-overlap validation before historical model results can be promoted.

## Sources

- Gu, Kelly & Xiu (2020), Factors That Fit the Time Series and Cross-Section of Stock Returns, Review of Financial Studies.
- Interacting Anomalies, Review of Asset Pricing Studies.
- Zhang & coauthors (2021), Microstructure in the Machine Age, Review of Financial Studies.
- Harvey, Liu & Zhu (2020), Thousands of Alpha Tests, Review of Financial Studies.
- Mazibas (2026), Explaining versus Predicting Mutual Fund Returns: Machine Learning, Factor Attribution, and Market Efficiency, SSRN working paper.
