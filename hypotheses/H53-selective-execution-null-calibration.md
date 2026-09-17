# H53 — Selective execution with null-calibrated abstention

Date: 2026-09-18

## Motivation

Recent 2026 evidence continues to show that predictive metrics can remain attractive while net trading performance disappears after spread, fees, and slippage. Kim (2026) reports this statistical-economic disconnect across 340 crypto ML strategy variants; Bysik & Ślepaczuk (2026) similarly find naive directional execution fails under tested 10 bps costs while cost-aware forecast filtering can rescue selected configurations. These results motivate testing the execution rule separately from the predictor, without changing the model during evaluation.

## Hypothesis

A frozen predictive model can improve net out-of-sample performance by abstaining when forecast edge is insufficient to cover expected execution friction, provided the abstention threshold is calibrated only on prior data and its false-deployment rate is controlled against a null.

## Experimental design

1. Freeze model predictions and feature timestamps before execution-policy evaluation.
2. Compare: always-trade baseline; cost-threshold abstention; volatility-conditioned abstention; combined gate.
3. Estimate expected round-trip friction from fees + spread + slippage + latency stress. Do not use future realized costs.
4. Calibrate thresholds only inside the development portion of each rolling split.
5. Evaluate each frozen policy on the subsequent OOS block.
6. Repeat under reference cost, +25%, +50%, and +100% adverse friction.
7. Run the identical policy-selection procedure on realistic zero-alpha null data to estimate false-deployment frequency.
8. Record every threshold/policy trial in the multiplicity ledger; apply DSR/PBO or an equivalent selection adjustment after the family is frozen.
9. Report net return, Sharpe/PSR, maximum drawdown, turnover, trade count, hit rate, average edge per trade, break-even cost, and fraction of OOS periods abstaining.
10. Keep the final confirmation period untouched until all policy choices and statistical gates are frozen.

## Falsification criteria

Reject H53 if the cost-aware gate does not improve net OOS performance versus the always-trade baseline across the pre-specified cost scenarios, or if its advantage disappears under null calibration / selection adjustment.

A positive result in only one cost assumption or one walk-forward path is insufficient.

## Literature

- Jaewook Kim (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, SSRN 6508779.
- Andrei Bysik & Robert Ślepaczuk (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*, arXiv:2606.00060.
- Arian, Norouzi Mobarekeh & Seco (2024), *Backtest overfitting in the machine learning era: A comparison of out-of-sample testing methods in a synthetic controlled environment*, Knowledge-Based Systems 305, 112477.
- Bailey, Borwein, López de Prado & Zhu (2017), *The Probability of Backtest Overfitting*.

## Status

OPEN. No empirical result is claimed by this document. The connected repository does not currently expose a frozen data-backed OOS prediction artifact sufficient to execute this experiment reproducibly.