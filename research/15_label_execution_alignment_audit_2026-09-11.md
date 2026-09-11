# Run 15 — Label/execution alignment audit (2026-09-11)

## Scope
Audit the current production reference engine for alignment between the supervised prediction target and the event actually monetized by the backtest. Cross-check against recent 2026 literature emphasizing horizon-matched execution and cost-aware validation.

## Verified implementation finding

The current reference engine in `bitcoin-ml-trading/production_research.py` trains on a 6-bar forward-close label:

`future_return[t] = Close[t+6] / Close[t] - 1`

The walk-forward purge correctly removes the final six training rows before each test fold, so the previously identified direct label-overlap leakage is not the active defect in this file.

However, the execution event is materially different from the prediction event. `signal_backtest()` receives the prediction at timestamp `t`, enters at the next bar `t+1`, and then resolves the trade using only that next bar's OHLC: stop, target, or `t+1` close. Thus the model is optimized/evaluated on a six-bar forward return while the monetized trade generally has a one-bar holding horizon.

This is not automatically look-ahead leakage, but it is a target/execution mismatch. It makes the economic interpretation of the reported backtest ambiguous: a model can predict the six-bar direction correctly while the next bar reverses, or predict the next bar correctly while failing to predict the six-bar outcome. The backtest therefore does not currently test the economic proposition represented by the label.

## Why this matters

Recent crypto/financial ML work increasingly couples prediction horizon, execution horizon, and holding/rebalancing period. A 2026 cryptocurrency confidence-threshold study explicitly specifies a 10-hour prediction/execution horizon, while recent horizon research argues that label horizon and inference/holding horizon should be treated as distinct experimental dimensions rather than silently substituted. These studies are not evidence that any particular horizon is profitable here; they support making the horizon relationship explicit and testable.

The current engine also computes `expected_gross` from the same stop/target geometry used by the one-bar execution simulator. That means the trade filter is economically tied to the one-bar path, while the classifier target is six bars. This further entangles model-selection and execution assumptions.

## Required redesign

Introduce an explicit event schema for every signal:

- `signal_time`
- `entry_time`
- `event_end_time`
- `label_horizon`
- `holding_horizon`
- `exit_rule`
- `cost_model_version`

Then test at least these predeclared variants without selecting the winner on the final holdout:

1. **Matched 6-bar target / 6-bar holding** — enter at `t+1`, exit at `t+6` subject to a clearly specified barrier rule.
2. **One-bar target / one-bar holding** — redefine the label to the executable next-bar return and retain the current execution horizon.
3. **Triple-barrier event target** — label by first hit of stop/target or the six-bar vertical barrier; execute with the same event definition.

Each variant must have its own purging based on the actual event end time, not a hard-coded global `HORIZON_BARS` assumption.

## Validation consequences

The current six-bar purge is sufficient for the current six-bar label, but a generalized event-time implementation is required once holding periods and barrier exits vary. For CPCV or any overlapping-event validation, purge by event interval and apply a predeclared embargo. Feature availability must remain point-in-time independent of the label/event horizon.

The final comparison must report gross return, each cost component, turnover/trade count, maximum drawdown, Sharpe/Sortino, and performance by confidence bin. No horizon variant should be promoted because it has the highest development OOS Sharpe alone.

## New hypothesis

**H40 — Horizon/execution alignment:** After leakage-safe OOS validation and identical cost assumptions, a model evaluated with a label horizon matched to its executable holding/event horizon will produce more stable signal-to-net-return monotonicity than the current mismatched six-bar-label/one-bar-execution design.

This is a falsifiable pipeline hypothesis, not an assertion that matched horizons will be more profitable.

## Literature evidence

- Kim (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, reports that conventional predictive validation can produce false positives and emphasizes CPCV/PBO plus economic gates; the paper studies 340 strategy variants and reports large transaction-cost erosion. cite not embedded in repo; see source URL in research log.
- A 2025/2026 cryptocurrency ML study explicitly evaluates a 10-hour prediction horizon with a corresponding execution horizon, illustrating the value of making the economic horizon explicit.
- Song, Liu & Chen (ICML 2026), *The Label Horizon Paradox*, treats training-label horizon and inference target as distinct quantities and provides an open-source backtest framework. The project documentation emphasizes that execution timing and prediction horizon should be represented explicitly rather than assumed equivalent.

## Decision

Do **not** promote any existing profitability metric as evidence for a six-bar predictive trading edge until the event definition is aligned. The next implementation milestone is an event-based label/execution layer followed by matched-horizon OOS comparison under the existing strict validation and cost framework.
