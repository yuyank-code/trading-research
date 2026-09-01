# Research Update 06 — Execution Policy, Search-Adjusted Validation, and a Hard Stop on Contaminated Results

Date: 2026-09-01

## Status

This pass does **not** promote a trading model. The main result is a tighter experimental boundary: older walk-forward results affected by forward-label overlap must remain excluded from evidence, and the next experiment should hold predictions fixed while testing execution policies.

## Literature update

### Bailey, Borwein, López de Prado & Zhu — backtest overfitting / PBO

Backtest overfitting can arise after relatively small numbers of alternative configurations. The Probability of Backtest Overfitting (PBO) framework uses combinatorially symmetric cross-validation to estimate how often the selected in-sample winner fails out of sample. This supports treating the complete experiment history as part of the statistical evidence, not just the final winning curve.

Sources: SSRN 2308659; SSRN 2326253.

### Bailey & López de Prado — Deflated Sharpe Ratio

The DSR adjusts the observed Sharpe for selection effects from multiple testing and for non-normal returns. Therefore an apparently high net Sharpe is not sufficient evidence when the project has searched across models, features, thresholds, horizons, and execution rules.

Source: SSRN 2460551.

### López de Prado — Optimal Trading Rules Without Backtesting

A useful methodological implication is to avoid unnecessary backtest calibration of trading-rule parameters. Where possible, execution rules should be derived from economic assumptions or estimated quantities rather than optimized against the final historical P&L.

Source: SSRN 2502613.

### Aparicio & López de Prado — Model Confidence Set and backtest overfitting

Model-selection procedures themselves can be unreliable under multiple testing and low signal-to-noise conditions. This reinforces the decision to compare a small, predeclared model set rather than continuously adding candidates after seeing results.

Source: SSRN 3044740.

### López de Prado — Market microstructure and ML

Microstructure variables can have predictive value out of sample, but their usefulness is tightly connected to execution and data quality. For this project, any future order-book or trade-flow feature must be timestamped at the information-availability boundary and evaluated with explicit spread/impact assumptions.

Source: SSRN 3193702.

## Critical implementation finding

The project README correctly records that a previous walk-forward implementation suffered from forward-label overlap. Until the corrected implementation is independently executed and audited, historical `final_*` performance from the contaminated path must not be used for model selection or claims of profitability.

The repository research standard already requires point-in-time data, prevention of label-overlap leakage, purged/embargoed validation, realistic trading costs, and preservation of failures.

## New hypotheses

### H17 — Cost-aware abstention

Given identical frozen OOS predictions, a policy that abstains when predicted edge does not exceed an execution-cost hurdle should have better net risk-adjusted performance than always trading the same directional threshold.

### H18 — Volatility-scaled cost hurdle

A fixed cost hurdle may be insufficient because effective execution cost and adverse selection vary with volatility. A hurdle scaled by contemporaneous volatility should reduce low-edge/high-cost trades without materially reducing high-edge trades.

### H19 — Turnover-control value

For the same frozen predictions, a no-trade band or partial-adjustment policy should improve net performance when signal changes are small relative to estimated execution costs.

### H20 — Search-adjusted survival

A candidate that survives the fixed OOS protocol but fails after accounting for the full search history should be classified as a research failure, not a marginal success.

## Next experiment — locked design

1. Generate strictly OOS predictions with event-aware label purging.
2. Freeze those predictions before evaluating execution policies.
3. Compare only four predeclared policies: baseline threshold, cost hurdle, volatility-scaled hurdle, and no-trade/partial-adjustment.
4. Evaluate a predeclared cost/slippage grid rather than selecting one favorable assumption.
5. Report gross return, net return, Sharpe, max drawdown, turnover, trade count, hit rate, and profit factor.
6. Evaluate fold-by-fold consistency rather than only the pooled equity curve.
7. Keep the final OOS segment untouched until all policy decisions are frozen.
8. Apply search-aware diagnostics (DSR/PBO/SPA or equivalent) using the complete trial registry.

## What would count as a robust result

A policy is not promoted because it has the highest Sharpe. It must:

- remain profitable after conservative costs,
- avoid dependence on a single fold/regime,
- retain performance across a neighborhood of cost assumptions,
- use a small predeclared search space,
- show no leakage,
- and remain credible after search-adjusted inference.

## Current conclusion

The strongest result this pass is methodological rather than economic: **execution-policy selection must be separated from prediction-model selection**. Using one frozen prediction stream allows us to test whether economic value comes from trading less selectively rather than from adding model complexity.

No new trading edge is established.
