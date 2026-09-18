# H69 — Volatility-normalized sizing and regime robustness

## Question
Does volatility-normalized position sizing improve out-of-sample robustness of a fixed predictive signal without merely shifting risk into high-volatility periods?

## Motivation
The 2026 large-scale financial time-series benchmark emphasizes risk-adjusted OOS performance, downside/tail risk, break-even transaction costs, and robustness across random seeds rather than prediction accuracy alone. Recent macro portfolio research also motivates explicitly robust objectives across adverse historical windows. These findings motivate testing risk normalization as a separate, low-complexity intervention before adding model complexity.

## Hypothesis
For a frozen signal and identical execution rules, sizing by a causal ex-ante volatility estimate will reduce tail risk and improve the stability of net risk-adjusted returns versus unscaled sizing, without requiring post-hoc tuning of the volatility lookback.

## Pre-registered comparison
1. Unit-risk / unscaled baseline.
2. Volatility targeting using causal rolling realized volatility.
3. Volatility targeting with a fixed conservative floor/cap.

The volatility estimator is fit only from information available at the decision timestamp. No future observations may enter the estimate.

## Validation
- Outer untouched OOS confirmation period.
- Purged/embargoed folds where labels overlap.
- All sizing parameters locked before the outer test.
- Evaluate across multiple market regimes, not only aggregate performance.

## Costs and execution
Apply the same spread, commission, slippage and liquidity-conditioned market-impact model to every sizing rule. Include +25%, +50%, and +100% adverse execution-cost stress.

## Metrics
- Net Sharpe and Sortino.
- Maximum drawdown and expected shortfall.
- Volatility of monthly/quarterly performance.
- Turnover and average participation.
- Break-even transaction cost.
- OOS rank persistence across folds/regimes.
- DSR, PBO and family-level SPA/Reality Check where the candidate family permits.

## Falsification
H69 fails if volatility normalization:
- only improves the development sample;
- requires different parameters by regime after seeing OOS results;
- increases tail loss or implementation shortfall materially;
- loses its advantage under modest adverse cost stress;
- or cannot beat a simple risk-matched baseline on untouched OOS data.

## Status
Pre-registered hypothesis. No profitability claim until frozen OOS data and predictions are available.
