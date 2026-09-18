# H66 — Capacity and Market-Impact Robustness

## Status

Pre-registered hypothesis; numerical evaluation requires frozen signals, position targets, and liquidity/volume data.

## Motivation

A strategy can survive spread/commission/slippage assumptions while still being non-scalable because market impact increases with order size. Almgren & Chriss (2001) frame execution as a trade-off between volatility risk and temporary/permanent market impact. Frazzini, Israel & Moskowitz use live institutional executions to show that trading costs vary materially with trade size, security characteristics, time, and exchange, and that capacity differs substantially across strategies.

## Hypothesis

H66 tests whether candidate strategy performance remains economically viable as capital increases and participation in available liquidity rises.

**Prediction:** if an apparent edge is genuine and sufficiently liquid, net risk-adjusted performance should degrade gradually as capital increases. A strategy whose edge disappears under modest participation rates is not capacity-robust even if its small-size backtest is attractive.

## Required experiment

For every candidate that reaches the execution-validity stage, replay the identical OOS signal path at capital multipliers:

`0.25x, 0.5x, 1x, 2x, 5x, 10x`

Estimate costs using a size-sensitive impact model. At minimum report:

- spread cost;
- explicit fees/commissions;
- slippage;
- temporary impact;
- permanent-impact sensitivity;
- participation rate / ADV or available-volume share;
- turnover;
- implementation shortfall;
- net CAGR/return;
- net Sharpe and Sortino;
- maximum drawdown;
- break-even capital / capacity;
- cost as a fraction of gross alpha.

## Adversarial tests

1. Multiply estimated impact by `0.5x, 1x, 2x`.
2. Impose liquidity droughts by increasing impact during the worst-liquidity quantiles.
3. Cap participation at conservative levels and record unfilled quantity rather than assuming complete execution.
4. Delay fills by one additional execution interval.
5. Re-run after removing the most liquid 10% and least liquid 10% of observations where applicable.

## Leakage / selection controls

- All liquidity inputs must satisfy `available_time <= decision_time`.
- Impact parameters must be estimated only from the development/training window.
- No capital level may be selected after observing untouched confirmation results.
- Retain all capacity curves, including failures.
- Apply the same OOS splits and execution assumptions to every candidate in the family.
- Apply DSR/PBO and family-level SPA/Reality Check after the candidate family has been evaluated.

## Pass criteria

No single capital level is sufficient. A candidate can only be described as capacity-robust if:

1. net performance remains positive under baseline and adverse impact assumptions across a pre-specified capital range;
2. the strategy does not require implausibly high market participation;
3. profitability is not concentrated entirely in the most liquid observations;
4. the result survives the project's multiple-testing and OOS gates.

Failure to pass H66 does **not** imply the signal is statistically false; it means the signal is not demonstrated to be scalable under the tested execution assumptions.

## Key references

- Almgren, R. & Chriss, N. (2001), *Optimal Execution of Portfolio Transactions*, Journal of Risk, 3, 5–39. https://doi.org/10.21314/JOR.2001.041
- Frazzini, A., Israel, R. & Moskowitz, T. J. (2012/2014), *Trading Costs of Asset Pricing Anomalies*.
- Frazzini, A., Israel, R. & Moskowitz, T. J. (2018), *Trading Costs*.
