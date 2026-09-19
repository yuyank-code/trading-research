# Research 32 — Forecast Calibration and Economic Value

## Literature synthesis

Calibration is distinct from discrimination: a predictor may rank outcomes well while its stated probabilities or forecast magnitudes are systematically mis-scaled. Honest calibration assessment provides finite-sample confidence bands for calibration curves rather than relying only on point estimates. See Dimitriadis et al., *Biometrika* (2023), "Honest calibration assessment for binary outcome predictions".

In asset-pricing research, confidence around machine-learning forecasts has recently been linked to investment selection. Allena, *Review of Financial Studies* 39(5), 2026, "Confident Risk Premiums and Investments Using Machine Learning Uncertainties," reports that selecting observations with more precise forecasts improved out-of-sample investment results across model classes. This is equity evidence, not FX evidence, so it is treated only as motivation for a mechanism test.

Broader time-series predictability research also supports forecast combination and shrinkage as ways to control overfitting in large predictor sets. Rapach and Zhou's review emphasizes that OOS predictability requires methods that guard against overfitting when information sets are large and noisy.

## Project-specific implication

The trading project should not assume that a better classifier or ranker automatically produces better position sizing. If the downstream trading rule interprets forecast magnitude as expected return, a calibration layer can either improve capital allocation or create another overfitting channel.

## Testable prediction

Conditional on an identical frozen predictor, if raw forecast magnitude is miscalibrated, an OOS-fitted low-complexity calibration map should improve net utility by concentrating exposure where realized returns justify the forecast magnitude and reducing exposure where the model is overconfident. The improvement must survive costs and null calibration controls.

## Required controls

- chronological train/validation/confirmation separation;
- purging and embargo based on the longest label horizon;
- calibration fit only inside the training side of each fold;
- no confirmation-driven recalibration;
- identical transaction-cost and impact model across variants;
- placebo calibration on shuffled/null forecasts;
- DSR/PBO and search-budget accounting;
- SPA/Reality Check and Model Confidence Set;
- regime and subperiod stability;
- adverse cost and capacity stress;
- immutable candidate-level OOS predictions and returns.

## Current conclusion

No evidence of an economic effect has been established yet. This research adds a targeted hypothesis while preserving the project's current conclusion that historical model results remain unpromoted until the corrected forward-label validation and frozen candidate-level OOS artifact exist.
