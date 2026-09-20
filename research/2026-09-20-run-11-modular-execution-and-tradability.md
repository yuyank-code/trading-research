# Research 52 — Modular execution, tradability, and incremental value

## Date
2026-09-20

## Literature update

A March 2026 peer-reviewed Journal of Financial Data Science paper, *Smart Trading Rule: A Modular Machine Learning Framework for Portfolio Optimization with Transaction Costs* (Li, Mulvey, Fabozzi), proposes separating portfolio optimization from transaction-cost management. The authors report higher returns/Sharpe and lower turnover across XGBoost/LSTM settings, framing the execution layer as an implicit regularizer.

Two additional 2026 results sharpen the caution:

- A large daily-futures benchmark evaluates OOS performance together with statistical significance, downside/tail risk, break-even transaction costs, seed robustness and compute efficiency rather than predictive error alone.
- A BTC walk-forward study using roughly 70,000 hourly observations reports that sign-based ML strategies fail at 10 bps, while cost-aware forecast thresholds can restore profitability for selected configurations; however, bootstrap evidence does not establish formal dominance of XGBoost over neural alternatives.

A separate 2026 live-deployment study reports a disconnect between strong walk-forward prediction metrics and near-random live trading performance, reinforcing that forecast quality and tradability are distinct quantities.

## Research implication

The project should explicitly isolate the economic contribution of the execution layer. A forecast cannot receive credit for gains caused by turnover control, portfolio construction, or cost-aware trade selection unless those components are evaluated independently against matched baselines.

## Test protocol

- Freeze OOS forecasts before execution-rule tuning.
- Compare modular execution, integrated decision rules, and transparent baseline under identical costs.
- Preserve every execution-rule trial in the committed ledger.
- Use purged/embargoed walk-forward validation and the corrected label-overlap contract.
- Stress spread, slippage, impact, latency and capacity.
- Evaluate net utility, turnover, drawdown, break-even costs and incremental value versus baseline.
- Run placebo forecasts through the same execution search to estimate false improvements.

## Finding

No numerical alpha finding is claimed in this run. The connected repository contains research protocols and hypotheses but not the immutable candidate-level OOS prediction/return matrix required for defensible model-performance confirmation. The README explicitly identifies corrected forward-label-overlap validation as a prerequisite for trusting older model results.

## Decision

Register H102. Do not promote any candidate on the basis of the modular-execution literature alone. Numerical testing remains blocked pending the required OOS artifacts.
