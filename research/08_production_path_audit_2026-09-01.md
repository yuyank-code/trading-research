# Research Update 08 — Production Path Audit

Date: 2026-09-01

## Status

This pass found a concrete implementation defect in the project's purported authoritative model-selection path. No performance claim is made.

## Finding

`bitcoin-ml-trading/production_research.py` creates a six-bar forward-return label:

`future_return[t] = Close[t+6] / Close[t] - 1`

Its walk-forward routine then uses every row before `test_start` as training data. The final training observations therefore have labels whose information interval extends into the beginning of the test period. This is label-overlap leakage.

The file's module documentation calls it the "leakage-safe final research engine", but the implementation does not actually purge overlapping label intervals. The discrepancy is now tracked as GitHub issue #2 in the model repository.

## Why this matters

Chronological ordering alone is insufficient when targets span future time. A model can be trained at time `t` on a target that uses information observed after the test-period prediction timestamp. This can inflate OOS evidence even though there is no random shuffling.

The literature reinforces the need to control both backtest leakage and research selection. Bailey et al. show that even apparently strong backtests can be selected from a search process with high probability of overfitting; the DSR adjusts observed Sharpe for selection bias and non-normality. citeturn0search0turn0search7 The newer BTC-USDT walk-forward study is also directly relevant: it reports that transaction costs can eliminate naive hourly ML trading performance and that cost-aware execution filters can materially change results. citeturn0academia24

## Required correction

For each observation store:

- `prediction_time`
- `label_end_time`
- model/data version

For each test fold, remove every training observation for which `label_end_time >= test_start` (with timestamp boundary semantics explicitly documented). Then apply an explicit embargo if required by the dependence structure.

The fixed six-bar horizon can use a six-bar cutoff only after verifying that the data is truly regular hourly data and that the label interval is exactly six hours. Event-time purging is preferred.

## Regression tests to add

1. Assert no training label interval intersects the test prediction interval.
2. Assert the last training label end precedes the first test prediction timestamp.
3. Assert purging behaves correctly when timestamps are missing or irregular.
4. Assert embargo is independently applied rather than hidden inside the purge.
5. Freeze a synthetic toy dataset where the unpurged implementation can be shown to leak and the corrected implementation cannot.

## New hypotheses

### H25 — Purge materially changes model evidence

Compare the old chronological split with the corrected event-time purge. Any meaningful degradation in predictive or trading metrics is evidence that the old result was partially leakage-driven.

### H26 — Cost-aware execution must be evaluated only after leakage correction

A cost-aware policy cannot rescue invalid predictive evidence. Execution-policy experiments are only admissible after corrected OOS predictions are frozen.

### H27 — Simpler models remain the default until leakage-corrected evidence proves otherwise

Do not promote RF/HGB/neural complexity until it demonstrates incremental OOS value over logistic regression under the same corrected folds and search budget.

## Current conclusion

The highest-value action is to fix the authoritative walk-forward implementation and rerun it. Existing results from the unpurged production path are not admissible as final evidence. This is a failure of the implementation, not evidence that the trading hypothesis itself is false.

### Sources

- Bailey, Borwein, López de Prado & Zhu, *The Probability of Backtest Overfitting*.
- Bailey & López de Prado, *The Deflated Sharpe Ratio*.
- Bysik & Ślepaczuk (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*.
