# Trading Research Map

## Status

This is the master map of the theoretical research program. It is intentionally broader than any single trading strategy.

## Research sequence

1. Mathematical/statistical foundations
2. Market microstructure and price formation
3. Asset pricing and factor models
4. Return-predictability effects
5. Statistical arbitrage
6. Volatility and derivatives
7. Macro and cross-asset relationships
8. Behavioral finance
9. Portfolio construction and risk
10. Execution, liquidity and capacity
11. Machine learning and nonlinear models
12. Deep learning, sequence models and transformers
13. Reinforcement learning
14. Causal inference
15. Backtesting, leakage, multiple testing and replication
16. Data engineering and point-in-time information
17. Cross-market replication and regime stability

## Current theoretical conclusions

### Evidence-backed principles

- A gross backtest is not sufficient evidence of an exploitable edge.
- Transaction costs, turnover, liquidity, slippage, borrow and capacity must be modeled before declaring economic viability.
- Complexity should neither be automatically rejected nor automatically preferred; incremental genuinely out-of-sample value must justify it.
- Momentum, reversal, liquidity and volatility repeatedly appear in empirical asset-pricing/return-prediction research, but their strength is conditional and can suffer crashes or decay.
- Weak theoretical signals may be statistically difficult to exploit reliably because estimation error can dominate the signal.
- Historical anomalies are not guaranteed to be stationary; changes in information processing can alter their profitability.
- Cross-sectional prediction and time-series prediction are different problems and should be benchmarked separately.
- Simple interaction/sorting strategies are important benchmarks for sophisticated ML.
- Multiple testing and research selection can create apparently impressive but false discoveries.
- Forward-label overlap must be purged from training data; an embargo may also be needed.
- Fundamental and alternative data require point-in-time availability timestamps, not merely observation dates.

## Main hypotheses accumulated so far

- **H1:** Signal profitability is conditional on liquidity and market state.
- **H2:** No-trade bands or partial portfolio adjustment can improve net performance by reducing unnecessary turnover.
- **H3:** A small set of economically motivated nonlinear interactions can add OOS information beyond a linear factor model.
- **H4:** There is a signal-strength/complexity point where adding weak predictors increases estimation noise faster than information.
- **H5:** Information-processing-dependent anomalies decay as information becomes faster and cheaper to process.
- **H6:** Partial adjustment toward a target portfolio can outperform full immediate rebalancing after costs.
- **H7:** Relative-return prediction can be more learnable than absolute-return prediction in some cross-sectional settings.
- **H8:** Nonlinear ML should only be accepted when it provides incremental OOS value beyond strong linear and simple-interaction benchmarks.

## Model ladder

Naive benchmark → classical time series → linear factors → Ridge/Elastic Net → simple interactions → tree models → boosting → regularized neural networks → high-dimensional factor models → sequence models → transformers → theory-guided ML → direct portfolio optimization → RL where justified.

## Validation gates

Leakage audit → point-in-time data audit → purged/embargoed chronological validation → untouched OOS test → transaction costs/slippage → turnover/liquidity/capacity → parameter/regime robustness → multiple-testing/PBO/DSR analysis → replication.

## Important project failure already discovered

An earlier walk-forward implementation used a six-bar forward-return label but did not sufficiently purge training observations at the test boundary. Training labels could therefore overlap the subsequent test period. Older model results must not be treated as validated evidence until rerun with label-aware purging.
