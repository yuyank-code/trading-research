# H114 — Selective Abstention / Cost-Gated Trading

## Status
Preregistered hypothesis; no OOS result yet.

## Motivation
Recent 2026 research reports that forecast quality and net trading performance can diverge sharply once transaction costs are included, and that cost-aware execution filters can outperform always-trade rules in selected settings. A separate 2026 selective-ML preprint proposes abstaining when a model does not beat a transparent fallback benchmark by a calibrated margin.

## Hypothesis
A candidate signal converted into a **predictable selective trading rule** — trade only when expected incremental utility over a frozen fallback exceeds a pre-specified cost/risk threshold, otherwise hold the fallback — will improve net OOS utility relative to the same model traded every period, without increasing model-selection leakage.

## Primary comparison
1. Always-trade candidate.
2. Cost-gated candidate + frozen fallback.
3. Frozen fallback alone.

All three use identical data, timestamps, features, model fits, execution assumptions, costs, and OOS periods.

## Gate definition
At decision time t, estimate signal utility only from information available through t. Trade only if the forecasted incremental utility exceeds:

`estimated round-trip friction + safety margin`

The safety margin and calibration window are fixed before OOS evaluation. No OOS threshold tuning is permitted.

## Required controls
- point-in-time data;
- fold-isolated preprocessing;
- purge/embargo for overlapping labels;
- execution lag consistent with information availability;
- commissions, spread, slippage and market-impact assumptions;
- turnover and capacity accounting;
- complete trial ledger including failed gates/configurations;
- placebo/synthetic-null gate test;
- DSR/PBO/SPA or equivalent multiple-testing controls where search occurs.

## Success criterion
The selective rule must improve **net OOS utility** over always-trade while retaining positive benchmark-relative performance across pre-specified cost-stress and subperiod tests. A reduction in turnover alone is not sufficient.

## Failure criteria
Reject H114 if the improvement disappears under realistic cost stress, is confined to one OOS period, requires OOS threshold tuning, or is reproduced by placebo signals.

## Evidence boundary
This hypothesis is motivated by recent literature, not established by it. No candidate is promoted until immutable candidate-level OOS predictions, positions, realized returns and cost components are available.
