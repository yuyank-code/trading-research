# Research 94 — Predict the Tradable Edge, Not the Gross Return

Date: 2026-09-22

## Research question

Does training/selection against an explicit estimate of net tradable return improve genuine OOS performance versus predicting the underlying gross return and applying transaction costs only after the forecast is converted into trades?

## Literature evidence

A 2026 walk-forward BTC study reports a disconnect between directional/model performance and economic performance after transaction costs. Its selected configurations benefited more from a cost-aware execution filter than from marginal architecture changes; naive sign trading became uneconomic under a 10-bps cost assumption. The study also reports that descriptive XGBoost superiority over neural alternatives was not statistically established. This is arXiv/preprint evidence and should be treated as hypothesis-generating rather than definitive.

A 2026 benchmark of deep learning for financial time series evaluates breakeven transaction costs, downside risk and seed robustness in addition to Sharpe, reinforcing the point that the economically relevant target is not gross prediction accuracy alone.

A 2026 NBER real-time asset-pricing benchmark further shows why the target and information set must be aligned with the actual decision timestamp: historical models can otherwise inherit look-ahead from information that was unavailable when the trade would have been made.

## Hypothesis

H145: Explicitly cost-aware prediction/selection improves net OOS utility relative to an otherwise identical gross-return prediction pipeline.

## Falsification design

Compare, with identical PIT data, folds, search budget, model class and execution simulator:

1. Gross-return target + ex-post costs.
2. Net-return target using only point-in-time cost estimates available at decision time.
3. Gross-return target + cost-aware trade threshold.
4. Matched-noise cost feature placebo.

The cost-aware target must not use realized future spread/slippage or future volume. Cost estimates are lagged or forecast from information available before the decision.

## Acceptance criteria

Promotion requires improvement in median outer-OOS net utility, not just gross Sharpe, and survival of 1x/1.5x/2x cost stress, execution-lag stress, liquidity buckets, seed dispersion, and placebo tests. Any improvement that disappears when the cost input is replaced by matched noise is rejected as non-informational.

## Failure conditions

Reject the hypothesis if cost-aware training only reduces turnover without improving risk-adjusted net OOS utility, if gains depend on a single seed/fold, or if cost features leak future realized execution conditions.

## Status

Protocol only. No numerical result is promoted until corrected purged/embargoed validation and the immutable prediction-to-net-P&L ledger are operational.
