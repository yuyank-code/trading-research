# H40 — Horizon/execution alignment

## Question
Does explicitly matching the supervised label horizon to the executable holding/event horizon improve the stability of the model's economic signal after realistic costs?

## Current mismatch
The production reference model predicts `Close[t+6] / Close[t] - 1`, while the current backtest enters at `t+1` and usually exits within the `t+1` bar. The current six-bar purge prevents direct label overlap but does not resolve this economic target/execution mismatch.

## Test
Compare, under the same data snapshot, features, model family, walk-forward schedule, cost assumptions, and untouched final holdout:

1. six-bar label + six-bar executable event;
2. one-bar label + one-bar executable event;
3. six-bar triple-barrier label + matching triple-barrier execution.

Use event-time purging and a predeclared embargo. Freeze model selection on development OOS before opening the final holdout.

## Primary outcomes
- net expectancy by confidence bin;
- monotonicity of confidence-bin net returns;
- net Sharpe and maximum drawdown;
- trade count and turnover;
- survival across cost-stress levels;
- CPCV/PBO and DSR diagnostics where applicable.

## Falsification
H40 is rejected if horizon-matched variants do not improve stability/monotonicity relative to the current mismatch, or if any apparent improvement disappears after costs and search-adjusted validation.

## Status
**Open.** No profitability claim is attached to this hypothesis yet.
