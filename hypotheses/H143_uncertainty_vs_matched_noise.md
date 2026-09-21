# H143 — Uncertainty Information vs Matched Noise and Smoothing

## Claim
Any economic benefit attributed to predictive uncertainty must exceed both a variance-matched random-noise control and a turnover/exposure-matched smoothing policy.

## Motivation
Recent 2026 evidence is mixed: one preprint reports gains from uncertainty-adjusted sorting, while a June 2026 controlled portfolio-optimization study finds calibrated uncertainty often fails to improve OOS certainty-equivalent performance and can be functionally equivalent to matched-variance noise. This creates a direct falsification test.

## Arms
- A: point-forecast policy
- B: calibrated uncertainty-aware policy
- C: variance-matched random-noise policy
- D: point-forecast policy with matched turnover/exposure smoothing
- E: strong non-ML baseline

## Locked controls
Same universe, timestamps, features, label horizon, folds, model family/capacity where applicable, training budget, portfolio constraints, final OOS period, and execution simulator.

## Primary outcome
Incremental net OOS certainty-equivalent utility of B versus A, C, and D.

## Required audits
- exact point-in-time information availability;
- corrected purged/embargoed label-overlap validation;
- uncertainty calibration fit only inside training/validation;
- final OOS remains untouched;
- all seeds and attempted configurations retained;
- complete prediction → position → execution → cost → net-P&L ledger;
- selection-aware inference and placebo accounting.

## Stress tests
1x, 1.5x, and 2x costs; execution delay; liquidity/capacity constraints; crash/OOD periods; seed dispersion; uncertainty-decile stability.

## Falsification
Reject the claim if uncertainty fails to beat either matched-noise or smoothing controls, if the gain disappears under modest cost stress, or if it is concentrated in one seed/regime.

## Promotion gate
No promotion until forward-label-overlap validation is corrected and the immutable execution ledger is available.
