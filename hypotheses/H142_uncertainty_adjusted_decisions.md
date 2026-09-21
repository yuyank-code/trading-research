# H142 — Uncertainty-Adjusted Decisions vs Point Forecasts

## Claim
If a trading model's predictive uncertainty contains useful information, incorporating uncertainty into position selection/sizing should improve net out-of-sample economic utility versus using point predictions alone.

## Null
Uncertainty carries no incremental tradable information once the point forecast, volatility, liquidity, and execution costs are controlled for.

## Arms
- A: point prediction strategy
- B: uncertainty-adjusted strategy
- C: confidence threshold based on expected edge minus uncertainty and expected cost
- D: random-confidence placebo
- E: strong non-ML baseline

## Locked controls
Same data, universe, timestamps, training folds, label horizon, model family, research budget, portfolio constraints, execution simulator, and final OOS period.

## Required audits
1. Point-in-time information availability.
2. Purge all training samples whose label windows overlap each test window.
3. Embargo after test windows.
4. Fit uncertainty calibration only inside training/validation.
5. Never select the best seed or confidence rule using final OOS.
6. Preserve every attempted configuration in the trial ledger.
7. Include label-shuffled and random-confidence placebos.

## Primary outcome
Incremental net OOS utility versus Arm A after all explicit and implicit trading costs.

## Secondary outcomes
Breakeven cost, turnover, drawdown, downside deviation, tail losses, seed dispersion, regime stability, and performance by uncertainty decile.

## Stress tests
Baseline cost, 1.5x cost, 2x cost, execution delay, liquidity/capacity constraints, and adverse-volatility regimes.

## Falsification
Reject H142 if the uncertainty-aware method does not beat point-estimate trading after costs, if gains disappear under modest cost stress, if the result is driven by a single seed/regime, or if the random-confidence placebo performs similarly.

## Promotion gate
No promotion without corrected forward-label-overlap validation and an immutable prediction-to-execution ledger.
