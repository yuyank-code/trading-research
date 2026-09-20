# H108 — Uncertainty-Aware Signal Selection

## Hypothesis

For a fixed return-forecasting model, restricting positions to forecasts with sufficiently high ex-ante precision can improve **net out-of-sample utility after costs** versus trading the same forecasts without an uncertainty gate.

## Motivation

Allena (2026), *Confident Risk Premiums and Investments Using Machine Learning Uncertainties*, reports that confidence-aware long-short strategies can improve out-of-sample returns and Sharpe ratios across model classes. The result motivates a test, but is not treated as evidence of transferable alpha.

## Falsifiable prediction

On a completely frozen confirmation sample, an uncertainty-aware policy must improve the preregistered primary metric (net risk-adjusted return / utility) relative to the same model with no uncertainty gate. The improvement must survive realistic trading costs and multiple-testing adjustment.

A null result, deterioration after costs, or benefit confined to a single regime/seed falsifies the hypothesis for the project.

## Experimental arms

1. Baseline model: trade all eligible forecasts.
2. Confidence gate: trade only observations whose ex-ante forecast interval/uncertainty meets the frozen precision criterion.
3. Transparent fallback: baseline benchmark with identical execution and costs.

## Controls

- Point-in-time features and labels.
- Purging/embargo for overlapping labels.
- Model-selection timestamps recorded separately from data timestamps.
- Immutable candidate-level OOS predictions and realized returns.
- Identical spread, commission, slippage, impact, borrow and turnover assumptions across arms.
- Seed ledger and full search-budget accounting.
- Placebo forecasts processed through the identical gate.
- DSR/PBO or equivalent multiplicity correction.
- Confirmation threshold frozen before confirmation results are inspected.

## Primary outcome

Incremental **net** OOS economic value of the confidence gate versus the no-gate baseline, with confidence intervals and break-even cost analysis.

## Failure criteria

Reject H108 if the confidence gate:

- only improves gross returns;
- loses its advantage under realistic costs;
- requires post-hoc threshold tuning on confirmation data;
- fails placebo controls;
- or produces an advantage that is not robust across seeds/regimes.

## Status

Protocol only. No alpha claim until the immutable OOS prediction/return matrix and corrected label-overlap validation are available.
