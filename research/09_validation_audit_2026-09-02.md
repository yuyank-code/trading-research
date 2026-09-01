# Validation audit — 2026-09-02

## Meaningful finding

A fresh source-code audit shows that the repository's two research engines are **not equivalent**. `research_v2.py` explicitly purges the training set by `horizon_bars` (`train_end = start - horizon_bars`). However, the current `production_research.py` walk-forward implementation still uses `tr = x.iloc[:start]` with no horizon purge.

Because the label at time t uses `Close[t+6]`, training rows immediately before each test boundary can have labels whose information window overlaps the OOS period. Therefore `production_research.py` remains invalid for final model selection until its walk-forward training cutoff is changed to an event-time purge.

This corrects an earlier assumption that the production path was already purged. The executable code is authoritative; research notes are not evidence.

## Required fix

For each test start `start`, exclude every training event whose `label_end_time >= test_start`. For the current fixed 6-hour target this is equivalent to `train_end = start - horizon_bars`, but the production implementation should preferably use explicit `prediction_time` and `label_end_time` columns so variable/event horizons cannot silently break the rule.

Add regression tests that assert:

1. max(training label_end_time) < min(test prediction_time)
2. no training event interval intersects a test event interval
3. embargo, if used, is applied after the purge
4. the exact fold boundaries are persisted with every prediction artifact

## Additional research result

Recent 2026 BTC-USDT work independently reports that naive hourly ML signals can lose their apparent profitability after realistic transaction costs, while cost-aware forecast-magnitude filtering can materially reduce turnover and recover profitability in selected configurations. This supports testing execution filters only after the prediction pipeline is clean; it does **not** establish an edge for this project.

## New hypotheses

- H30: Event-time purging produces identical or stricter validation than the fixed six-row purge.
- H31: After purging, any apparent model advantage remains across walk-forward folds rather than only in pooled results.
- H32: Cost-aware abstention adds value using frozen predictions, not predictions re-optimized for the policy.
- H33: The eventual selected configuration survives DSR/PBO-style selection adjustment over the complete recorded search.

## Literature

Bailey & López de Prado (2014), *The Deflated Sharpe Ratio*, documents selection bias and non-normality corrections for large-scale backtest searches. Bailey et al. (2017), *The Probability of Backtest Overfitting*, motivates CSCV/PBO-style checks. A 2026 BTC-USDT walk-forward study reports that 10-bps frictions can erase naive sign-based ML profitability and that cost-aware filtering can materially change the result.
