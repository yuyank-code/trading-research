# H97 — Signal Decay / Cost Frontier

**Status:** proposed robustness gate

## Claim to test

A candidate signal should retain economically meaningful incremental value versus a frozen baseline across a pre-registered execution-cost frontier and should degrade plausibly under execution latency. If performance depends on an arbitrarily favorable friction assumption or same-bar timing, it is not robust evidence.

## Falsification

Reject H97 if the candidate:
- loses its incremental net value at realistic cost assumptions;
- collapses under a small, economically plausible execution delay;
- has an implausibly non-monotone cost response that indicates implementation/timing artifacts;
- only survives in a selected seed/configuration or against an uncalibrated baseline;
- fails matched null-search comparison.

## Required controls

- immutable OOS prediction/return matrix;
- corrected forward-label-overlap checks;
- purged/embargoed walk-forward and CPCV where appropriate;
- realistic spread, commission, slippage and impact;
- break-even transaction cost;
- committed trial/seed ledger;
- DSR/PBO and SPA/Reality Check/MCS;
- zero-alpha and microstructure placebo workflow audits;
- identical execution layer for candidate and baseline.

## Primary output

A cost-vs-net-performance frontier and latency-vs-net-performance frontier, with incremental performance over the frozen baseline and uncertainty intervals. No model is promoted on gross performance alone.
