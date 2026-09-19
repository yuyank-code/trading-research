# H81 — Forecast Calibration Has Incremental Economic Value

## Status
Pre-registered; not yet passed.

## Motivation
The project has tested signal magnitude, disagreement, and abstention, but has not isolated whether the *calibration* of a model's forecast is economically useful. A model can rank observations correctly while producing forecast magnitudes that are systematically too extreme or too conservative. If position sizing or execution thresholds use forecast magnitude, calibration errors can directly translate into turnover and cost.

Recent literature emphasizes calibration/confidence as distinct from discrimination and finds that uncertainty-aware investment rules can improve out-of-sample results. The project will test this mechanism without importing equity-market results into FX.

## Hypothesis
For a fixed predictor and fixed information set, an OOS-calibrated forecast-to-return mapping will produce better net economic utility than the raw model score when both are subjected to the same execution and multiple-testing controls.

## Null
Calibration provides no incremental economic value over the raw score after realistic transaction costs and execution rules.

## Design
1. Freeze the underlying feature set, model family, training procedure, and candidate search budget.
2. Generate strictly chronological, purged/embargoed validation predictions.
3. Fit calibration only inside each training/validation fold; never fit calibration parameters on confirmation data.
4. Compare raw-score sizing with pre-registered calibration methods: affine/isotonic where appropriate, with a minimal parameter budget.
5. Evaluate directional discrimination separately from calibration: rank IC/AUC where applicable, calibration error, Brier/log loss for probabilistic targets, and economic utility.
6. Convert forecasts to positions using identical risk and execution rules.
7. Apply realistic spread, commission, slippage and nonlinear impact assumptions.
8. Test on an untouched confirmation block that has never influenced calibration, threshold, model, or cost selection.
9. Run matched-complexity placebo calibration on shuffled/null forecasts to estimate false discovery from the calibration search itself.
10. Apply DSR/PBO, SPA/Reality Check, Model Confidence Set, embargo sensitivity, holding-period sensitivity, capacity stress, and the existing synthetic-zero-alpha workflow.

## Pass criteria
A calibration variant may only be promoted if its incremental *net* improvement survives the full validation stack, is stable across confirmation subperiods, and is not reproduced by matched-complexity null forecasts. If raw and calibrated models are statistically indistinguishable, retain the simpler raw specification.

## Failure conditions
- Calibration is fit using any future observation or confirmation outcome.
- Economic improvement disappears under modest adverse costs.
- Improvement occurs only in one confirmation regime.
- Calibration complexity materially increases search exposure without surviving multiple-testing controls.
- Null forecasts receive similar gains.

## Key implementation artifact
`candidate_oos_predictions.parquet` (or equivalent immutable candidate-level OOS prediction matrix) must exist before numerical promotion.
