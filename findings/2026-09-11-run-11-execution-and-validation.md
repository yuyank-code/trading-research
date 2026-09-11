# Run 11 — Execution and Validation Findings

Date: 2026-09-11

## Meaningful progress

A fresh audit of `bitcoin-ml-trading/production_research.py` confirms the current engine has deterministic cost stress, explicit fee/slippage attribution, trial registration, and an intrabar-ambiguity flag. The current walk-forward training excludes the final six label-horizon bars from each training fold, preventing direct label overlap across the fold boundary.

The remaining major issue is execution/target alignment: the supervised label is a six-bar forward close event, while the trading simulator enters on the next bar and resolves the position from that next bar's OHLC (or that bar's close if neither barrier is reached). This means the model is being trained to answer a six-bar question while the simulator monetizes a predominantly one-bar path. This must be tested explicitly rather than assumed equivalent.

## H51 — Prediction/execution horizon invariance

Test whether the economic result survives explicit alignment between the supervised event and the executable holding period.

Compare, using frozen OOS predictions and identical feature information:

1. 1-bar forward-close target + 1-bar execution;
2. 6-bar forward-close target + 6-bar execution;
3. event/triple-barrier target + matching barrier execution;
4. the current 6-bar-label/next-bar execution configuration as a diagnostic baseline only.

Promotion requires the qualitative conclusion to survive the aligned alternatives; a result existing only in the diagnostic mismatch is not evidence of robust alpha.

## H52 — Intrabar ambiguity bounds

For trades where the same OHLC bar touches both stop and target, report stop-first, target-first, exclusion, and lower-timeframe reconstruction where available. Do not treat one arbitrary ordering as ground truth.

## Literature update

Recent 2026 evidence strengthens the project’s existing validation hierarchy:

- Kim (2026), *Beyond Accuracy*, reports 340 crypto ML strategy variants and identifies directional bias, statistical/economic disconnect, and transaction-cost omission as recurring failure modes. The paper argues for fixed-order statistical and economic gates and reports substantial cost erosion in its experiments.
- Bysik & Ślepaczuk (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs*, evaluates roughly 70,000 hourly BTC observations in 27 walk-forward folds. Naive sign strategies fail under 10 bps in tested settings; a cost-aware forecast filter rescues selected configurations, but bootstrap evidence does not establish formal model dominance.
- Pindza (2026), *Microstructure alpha: hierarchical learning and cross-asset transfer in cryptocurrency markets*, uses purged walk-forward validation on more than three million minute observations. The paper reports that boosted models overfit under leakage controls and that no strategy survives realistic exchange fees in its tested retail-fee setting.
- Arian, Norouzi Mobarekeh & Seco (2024), *Backtest overfitting in the machine learning era*, finds CPCV superior to conventional OOS procedures in its controlled experiments, with lower PBO and stronger DSR statistics.

These are evidence for validation design, not evidence that the project has profitable alpha.

## Current verdict

No new profitability claim is promoted. The repository still does not contain a frozen, data-backed `outputs/final_model_report.json` generated from the actual unified dataset, so numerical OOS performance cannot be honestly recomputed from the connected repository alone.

The next decisive experiment is therefore an execution-horizon invariance test on a frozen OOS prediction set, followed by nested benchmark tests, cost stress, intrabar bounds, and multiple-testing correction before any untouched holdout claim.
