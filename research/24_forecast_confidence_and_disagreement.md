# Research 24 — Forecast Confidence and Model Disagreement

## Date
2026-09-19

## Question
Can uncertainty or disagreement among otherwise fixed forecasts improve the conversion of predictions into economically viable trades?

## Literature

### Bali, Kelly, Mörke & Rahman (2026) — Machine Forecast Disagreement
Published in *The Review of Financial Studies* (corrected proof, April 2026). The authors model investors as heterogeneous machine-learning specifications and use dispersion across their forecasts as a measure of disagreement. They report a strong relation between disagreement and future stock returns and interpret the result through mispricing, short-sale costs, and limits to arbitrage. This is cross-sectional equity evidence, not direct evidence for FX.

### Allena (2026) — Confident Risk Premiums and Investments Using Machine Learning Uncertainties
Published in *The Review of Financial Studies*, Volume 39, Issue 5. The paper constructs ex-ante confidence intervals for forecasts and reports improved out-of-sample performance when investment is concentrated in forecasts with greater precision. The project should treat this as motivation for an economic filter, not as a result to import into another asset class.

### Zhang, Zhu & Linnainmaa (2025) — Man versus Machine Learning Revisited
Published in *The Review of Financial Studies*, Volume 38, Issue 12. The authors show that a prominent ML trading result was affected by look-ahead bias and that simpler linear models can remain competitive after correction. This is directly relevant to H73: confidence must be computed causally and cannot rescue a leaky predictor.

### Duarte et al. (2026) — Too Good to Be True: Look-Ahead Bias in Empirical Options Research
Published in *The Review of Financial Studies* in June 2026. The paper documents that apparently exceptional strategy performance can arise from using information unavailable at portfolio formation. This reinforces the requirement that confidence estimates, calibration parameters, ensemble weights, and any filtering thresholds use only information available at the decision timestamp.

## Translation to the FX project

The literature suggests two related but distinct mechanisms:
1. **forecast precision:** trade more aggressively when estimated uncertainty is lower;
2. **forecast agreement:** trade when independently trained models give similar directions/magnitudes.

The project should not assume either mechanism transfers from equities to FX. H73 therefore tests both as narrowly scoped filters around a frozen predictor.

## Testable design

- Freeze the predictor and all original features.
- Generate out-of-sample predictions without refitting on future observations.
- Construct confidence/disagreement measures only from models trained on information available at each timestamp.
- Compare always-trade versus confidence-filtered and agreement-filtered variants.
- Include a matched-count random filter as a placebo.
- Use purging/embargo for overlapping forward labels.
- Reserve an untouched confirmation period.
- Apply the project's full execution-cost, capacity, null-workflow, DSR/PBO, SPA/Reality Check and Model Confidence Set gates.

## Important limitation

No numerical claim is made in this research note. The repository currently requires the frozen candidate-level OOS prediction/return matrix and corrected validation artifacts before H73 can be evaluated honestly. The literature provides a testable mechanism, not evidence that this project's FX strategy has alpha.

## Sources
- Bali, T. G., Kelly, B., Mörke, M., & Rahman, J. (2026), *Machine Forecast Disagreement*, The Review of Financial Studies, DOI: 10.1093/rfs/hhag042.
- Allena, R. (2026), *Confident Risk Premiums and Investments Using Machine Learning Uncertainties*, The Review of Financial Studies 39(5), 1463–1505, DOI: 10.1093/rfs/hhaf087.
- Zhang, Y., Zhu, Y., & Linnainmaa, J. T. (2025), *Man versus Machine Learning Revisited*, The Review of Financial Studies 38(12), 3768–3790, DOI: 10.1093/rfs/hhaf066.
- Duarte, J., Jones, C. S., Khorram, M., Mo, H., & Wang, J. L. (2026), *Too Good to Be True: Look-Ahead Bias in Empirical Options Research*, The Review of Financial Studies, DOI: 10.1093/rfs/hhag061.
