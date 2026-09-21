# H133 — Volatility Channel vs Directional Alpha

## Hypothesis
A point-in-time volatility forecast may provide more stable incremental OOS economic value through risk scaling/exposure control than a similarly complex model attempting to forecast next-period signed returns. Any apparent volatility advantage must beat a simple realized-volatility scaler and matched-noise placebo under identical execution and selection controls.

## Falsification
Reject H133 if the volatility-forecast arm does not improve net OOS utility over the unscaled and realized-volatility baselines, or if its advantage disappears against the matched-noise placebo, cost stress, lag stress, or regime slices.

## Experimental arms
A. Unscaled directional baseline
B. Simple realized-volatility scaling
C. ML volatility-forecast scaling
D. Matched-noise volatility placebo
E. Strong non-ML risk-control baseline

The directional signal is frozen across A-D so the experiment isolates the value of the volatility channel.

## Required controls
- point-in-time data and reporting lags;
- fold-isolated preprocessing;
- purge/embargo matched to forward horizons;
- nested calibration of volatility-target parameters;
- immutable final OOS;
- identical execution and cost engine;
- commission, spread, slippage, market impact and borrow/funding;
- 1x / 1.5x / 2x cost stress;
- execution-lag perturbation;
- crash/regime and tail slices;
- complete research-trial ledger;
- DSR/PBO/SPA or equivalent selection-aware inference;
- row-level prediction -> position -> execution -> turnover -> gross P&L -> cost -> net P&L artifact.

## Promotion criterion
Promote only if C produces statistically and economically meaningful incremental net OOS utility over B and A, remains stable across cost models and regimes, and survives placebo and selection-aware tests. Lower volatility or higher standalone Sharpe is insufficient.

## Status
OPEN. No numerical result yet.
