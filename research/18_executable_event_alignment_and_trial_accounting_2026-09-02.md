# Run 18 — Executable-event alignment and trial accounting

Date: 2026-09-02

## Meaningful finding

The current production engine is leakage-aware at the fixed six-bar label boundary, but the supervised target and the economic trade event are not identical.

`production_research.py` constructs `future_return = Close[t+6] / Close[t] - 1`, while `signal_backtest()` enters at `Open[t+1]` and exits from the following bar's high/low/close with stop/target rules. This is not itself direct look-ahead leakage, but it creates target/execution mismatch: the classifier is optimized for one return interval while the backtest monetizes another.

## Required experiment before final performance claims

1. Freeze an explicit event definition: signal time, executable entry time, and executable exit/horizon.
2. Generate the supervised label from that executable event.
3. Represent each label as an event interval `[t_start, t_end]` and purge training observations whose label intervals overlap the test event interval.
4. Add a separate embargo parameter and test its sensitivity.
5. Generate immutable OOS predictions before any threshold/cost selection.
6. Run the predefined 0.5x–3x fee/slippage grid without changing predictions.
7. Keep a complete trial registry and estimate effective trial count for DSR.
8. Use CPCV/CSCV as a robustness diagnostic, followed by one untouched final holdout.

## Literature update

Bailey & López de Prado (2014) show that selecting the best of many backtests creates selection bias and motivate the Deflated Sharpe Ratio to adjust for multiple testing and non-normal returns.

A 2024 Knowledge-Based Systems comparison reports CPCV as more robust than conventional walk-forward evaluation for reducing PBO and improving DSR diagnostics in controlled financial experiments, while noting computational and generalization limitations.

A May 19, 2026 BTC-USDT study using roughly 70,000 hourly observations reports that naive sign-based ML strategies are vulnerable to 10-bps transaction costs, while a forecast-magnitude cost filter can reduce turnover and recover profitability in selected configurations; the study does not establish formal model-family dominance.

## Research hypotheses

- H35: An executable-event label produces better calibration and more stable OOS trading returns than the current close-to-close label.
- H36: The apparent edge survives after event-time purging plus embargo.
- H37: Cost-aware abstention retains positive expectancy at 1x–3x stressed costs without retuning predictions.
- H38: The selected policy survives effective-trial-count/DSR adjustment and an untouched final holdout.

## Status

No profitability claim is promoted. Issue #7 tracks the target/execution alignment repair.
