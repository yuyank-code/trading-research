# H166 — Uncertainty Shrinkage vs Cost Gate

**Status:** Registered
**Date:** 2026-09-23

## Hypothesis

For the same frozen point-in-time-safe forecast, an uncertainty-aware position-sizing/abstention rule will improve paired net out-of-sample decision utility relative to both the raw signal and a cost-only threshold, without relying on final-holdout tuning.

## Design

Use one frozen candidate model and one frozen benchmark. Compare:

- **A:** raw forecast-to-position rule;
- **B:** cost-only trade threshold;
- **C:** uncertainty-aware shrinkage/abstention;
- **D:** joint uncertainty + cost rule.

The model, feature set, universe, decision timestamps, execution lag, portfolio construction and research search budget are fixed before comparison.

## Validation requirements

- point-in-time information availability;
- corrected forward-label overlap;
- purging and embargo appropriate to the label horizon;
- immutable final OOS holdout;
- realistic commissions, spread, slippage and impact;
- 1x / 1.5x / 2x cost stress;
- seed aggregation for stochastic models;
- paired candidate-minus-baseline inference;
- complete trial accounting and search adjustment;
- turnover and capacity reporting.

## Primary endpoint

Paired net OOS decision utility versus the frozen baseline on common timestamps.

Secondary endpoints: turnover, drawdown, cost breakeven, stability across regimes/seeds, and calibration of forecast uncertainty.

## Falsification

Reject H166 if uncertainty-aware variants do not improve net OOS utility, only win at one cost level, require holdout tuning, lose to the cost-only gate after search adjustment, or materially increase implementation sensitivity.

## Rationale

Forecast uncertainty can make the trading decision more conservative when expected economic value is small relative to uncertainty and friction. This tests whether that information is economically useful rather than assuming higher predictive accuracy translates into trading alpha.
