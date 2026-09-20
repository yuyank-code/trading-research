# H102 — Modular execution layer must add incremental net value

## Claim
A model-agnostic execution/portfolio layer that converts frozen forecasts into trades may improve net performance by reducing turnover and execution drag, but it should only be credited with value if it improves out-of-sample net utility versus an integrated baseline under identical forecasts, costs, and search budgets.

## Motivation
A March 2026 peer-reviewed Journal of Financial Data Science article proposes a modular "smart trading rule" that separates portfolio optimization from transaction-cost management and reports improved returns, Sharpe and turnover across XGBoost/LSTM experiments. This is promising but architecture-level gains are vulnerable to tuning and implementation effects.

## Falsifiable prediction
Given the same frozen OOS forecasts and identical execution assumptions, a pre-registered modular execution rule will produce higher net utility and/or lower turnover than a matched integrated decision rule in a statistically meaningful fraction of OOS periods. If the advantage disappears after search/multiplicity adjustment or realistic cost stress, H102 is rejected.

## Experimental design
1. Freeze model forecasts before execution-rule tuning.
2. Compare modular execution, integrated thresholding, and a transparent no-ML/frozen baseline.
3. Use purged/embargoed walk-forward evaluation.
4. Apply identical commissions, spread, slippage, market impact, borrow and capacity assumptions.
5. Keep execution-rule search in the committed trial ledger.
6. Evaluate net Sharpe, certainty-equivalent return, turnover, drawdown, cost breakeven and incremental return versus baseline.
7. Stress execution latency and costs; do not optimize on the final confirmation period.
8. Run the same workflow on placebo forecasts to measure false improvement.

## Promotion criterion
H102 cannot promote a strategy unless the modular layer's incremental benefit survives the frozen confirmation period, realistic cost frontier, placebo control, and multiplicity-aware inference.

## Status
Hypothesis registered; numerical test blocked until the immutable candidate-level OOS prediction/return matrix and corrected forward-label-overlap validation are available.
