# H68 — Liquidity-conditioned execution costs

## Status
Pre-registered hypothesis. No promotion claim.

## Motivation
A single fixed spread/slippage assumption can be misleading in FX because transaction costs vary with liquidity, trade size, volatility, and market conditions. Recent FX microstructure evidence finds heterogeneous transaction costs and size-dependent effects, while current ML trading studies show that modest frictions can erase gross alpha.

## Hypothesis
For a fixed signal and position-sizing policy, an execution model whose costs are conditioned on observable pre-trade liquidity/volatility variables will produce more realistic and more conservative OOS performance than a constant-cost model. Strategies whose apparent edge survives the conditional-cost model should exhibit materially greater robustness than strategies that survive only the constant-cost assumption.

## Pre-registered test
1. Freeze the signal/model before execution-cost calibration.
2. Define all cost inputs using only information available before the order decision.
3. Compare three execution models: constant bps; volatility-conditioned bps; liquidity/size-conditioned impact.
4. Evaluate identical OOS trades under all three models.
5. Stress each model by +25%, +50%, and +100% adverse cost multipliers.
6. Report net return, Sharpe, Sortino, max drawdown, turnover, implementation shortfall, break-even cost, and fraction of gross PnL consumed by costs.
7. Stratify results by volatility/liquidity regime without selecting regimes after seeing OOS results.
8. Repeat with delayed fills and partial-fill assumptions where data permit.

## Falsification criteria
Reject the hypothesis if conditional costs do not improve realism relative to constant costs, or if the strategy's OOS conclusion changes materially only because of an arbitrarily chosen cost specification.

## Leakage controls
- Cost features must satisfy available_time <= decision_time.
- No future spread, future volatility, or future liquidity may enter the execution estimate.
- Calibration of cost coefficients must occur only inside development data.
- Final confirmation data remain untouched until the protocol is frozen.

## Promotion gate
A candidate cannot be promoted because it survives one favorable cost model. It must survive the pre-registered cost-model family and adverse-cost stress, with multiple-testing adjustments applied to the full candidate family.
