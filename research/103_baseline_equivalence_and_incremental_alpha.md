# Research 103 — Baseline Equivalence and Incremental Alpha

Date: 2026-09-22

## Literature signal

Recent 2026 evidence strengthens a recurring concern in financial ML: a sophisticated predictive model can add little incremental economic value once portfolio construction, covariance regularization, and shrinkage are controlled. A 2026 leak-free, cost-aware large-cap US equity benchmark reported an MLP Sharpe of 0.96 versus 0.94 for a no-ML Black-Litterman prior, while the MLP incurred more than three times cumulative transaction costs; an equal-weight portfolio was also close to both. This is a preprint/working-paper result, so it is treated as evidence to test rather than as settled fact.

A separate 2026 study of 5,376 ML portfolios finds that training windows, filters, and portfolio construction choices generate large performance dispersion, reinforcing the need to distinguish model alpha from research-design and portfolio-construction effects.

A 2026 deep-learning futures benchmark provides a useful positive control: models should be evaluated on OOS Sharpe together with tail/downside risk, breakeven transaction costs, seed robustness, and computational cost.

## Research implication

Before adding another architecture, isolate the incremental contribution of the forecast. A model should beat a strong no-ML/risk-only baseline under the same universe, covariance estimator, optimizer, rebalance schedule, and execution model.

## Experimental design

Compare, using identical PIT data and portfolio construction:

1. Equal-weight baseline.
2. Risk/shrinkage-only baseline.
3. Linear forecast.
4. Nonlinear ML forecast.
5. Nonlinear ML forecast with cost-aware deployment.

Selection must occur only inside the training/validation history. The final OOS period remains untouched.

## Promotion criteria

A candidate is promoted only if its incremental net OOS utility over the strongest baseline survives:

- purged/embargoed validation where label horizons overlap;
- point-in-time feature availability;
- commissions, spread, slippage, impact, borrow and capacity assumptions where applicable;
- 1x, 1.5x and 2x cost stress;
- execution-delay stress;
- multiple seeds;
- multiple-testing correction / PBO or an equivalent selection-control procedure;
- null/placebo workflow.

Do not credit a model for improvements that can be reproduced by lowering turnover, leverage, or volatility through the portfolio layer alone.

## Status

Protocol change only. No model is promoted from historical results until the repository's forward-label-overlap validation issue is corrected and rerun under the locked protocol.

## Sources

- Bengoechea Pardo (2026), *On the Limits of Low-Frequency OHLCV Signals in Machine Learning-Driven Portfolio Optimization: A Cost-Aware, Leak-Free Benchmark on Large-Cap US Equities*, SSRN 6952859.
- Lalwani, Meshram & Jindal (2026), *Empirical Asset Pricing via Machine Learning: The Role of Research Design Choices*, European Financial Management, DOI 10.1111/eufm.70033.
- Saly-Kaufmann, Wood, Calliess & Zohren (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*, arXiv:2603.01820.
