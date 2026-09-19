# H79 — Capacity and Market-Impact Robustness

## Status
Pre-registered research hypothesis. No promotion claim.

## Motivation
A strategy can remain statistically attractive after spread/commission/slippage assumptions while still being economically unusable once position size grows. Trading costs are not necessarily constant in trade size: empirical OTC and bond-market evidence shows execution costs vary with client type, market conditions, and trade size, while theory predicts transaction costs can alter equilibrium volatility and the willingness to trade.

## Hypothesis
For any candidate strategy that survives the existing causal OOS stack, net performance should degrade smoothly as capital/exposure increases under a realistic market-impact model. A robust strategy should retain positive expected net utility over a non-trivial capacity range rather than only at an arbitrarily small notional.

## Falsification
Reject capacity robustness if any of the following occurs:
- profitability disappears at modest multiples of the baseline position size;
- the result depends on an unrealistically flat cost-per-dollar assumption;
- performance is dominated by a small number of high-impact trades;
- capacity conclusions reverse under reasonable impact parameter perturbations;
- a matched random strategy has comparable capacity-adjusted performance.

## Pre-registered experiment
Keep features, labels, model family, hyperparameters, signal thresholds, holding periods, validation folds, embargo, and final confirmation set frozen. Vary only execution scale and impact assumptions.

Test size multipliers: 0.25x, 0.5x, 1x, 2x, 4x, 8x baseline notional, subject to available liquidity.

For each scale report:
- gross and net annualized return;
- net Sharpe and Sortino;
- maximum drawdown and tail loss statistics;
- turnover;
- implementation shortfall;
- break-even spread/slippage;
- cost as a fraction of gross PnL;
- utilization/capacity constraints;
- fold-level OOS stability.

Run the complete statistical gate at the strategy specification level: DSR/PBO, SPA/Reality Check, Model Confidence Set, seed/period stability, and synthetic-zero-alpha controls.

## Leakage controls
- All liquidity/volume fields must be point-in-time available.
- Do not use future realized volume or future spread observations to determine today's executable size.
- Capacity parameters must be fixed before touching the confirmation block.
- Any trade that exceeds the defined participation/liquidity limit must be rejected or mechanically clipped according to the pre-registered rule.

## Interpretation
Capacity is a robustness dimension, not an optimization target. If the strategy only works at negligible capital, record the result as economically fragile even if statistical tests are favorable.

## Evidence standard
No candidate is promoted from this test alone. A capacity result is useful only after the corrected forward-label validation issue and frozen candidate-level OOS prediction/return matrix are available.
