# H119 — Volatility-Gated Execution Under Cost Stress

## Hypothesis
A predictive trading model's net OOS utility can improve if execution is gated by a pre-specified, point-in-time volatility/friction condition, but only if the gate survives null calibration, cost stress, and untouched OOS evaluation.

## Motivation
Recent 2026 evidence reports that an always-on FX forecasting strategy can have weak or negative net economics despite acceptable forecast error, while a volatility-gated policy reduced trade switches and improved net OOS performance in one EUR/USD experiment. This is a preprint result and is treated as hypothesis-generating, not as established alpha.

## Test design
Compare, using the same frozen predictions and execution engine:
1. Always-trade candidate.
2. Volatility-gated candidate.
3. Cost-threshold gate based only on forecast magnitude versus estimated all-in friction.
4. Frozen fallback / no-signal benchmark.
5. Identical gates applied to placebo predictions.

All gates must be calibrated only inside training/validation windows. The final OOS window is never used to choose the gate threshold.

## Required controls
- Point-in-time features and cost estimates.
- Purging/embargo for overlapping labels.
- Immutable candidate-level OOS prediction, position, turnover, realized return and cost records.
- Commission, spread, slippage and impact modeled separately.
- 1.0x, 1.5x and 2.0x cost stress.
- Execution-lag perturbation.
- Predefined regime/subperiod analysis.
- Complete trial ledger, including failed/aborted/discarded gates.
- Null/placebo search calibration.
- DSR/PBO/other multiple-testing controls where applicable.

## Promotion criterion
Do not promote on gross return or prediction loss. Require incremental **net OOS utility** over the frozen fallback, survival under 1.5x cost stress, no material degradation in the worst predefined regime, and a placebo false-promotion rate consistent with the null calibration.

## Falsification
Reject H119 if the gated strategy does not improve net OOS utility over always-trade/fallback after realistic costs, if the improvement disappears under modest cost stress, or if placebo gates frequently generate comparable improvements.
