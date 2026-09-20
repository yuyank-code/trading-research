# Research 67 — Validation Architecture and Information Scaling

## Date
2026-09-20

## Literature

1. Kim (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*. The study reports systematic failures from directional bias, statistical-economic disconnect, and omitted transaction costs across 340 strategy variants. It reports that a permutation test can pass while CPCV and economic tests fail, and that net Sharpe declines with trading frequency.
2. Kohn et al. (2026), *Neural-Network Volatility Forecasting*, Journal of Financial Econometrics. Across more than 10,000 stocks, sample-size scaling produced larger gains than model-size scaling or architectural changes within the studied specifications.
3. Allena (2026), *Confident Risk Premiums and Investments Using Machine Learning Uncertainties*, Review of Financial Studies. Restricting positions to forecasts with higher ex-ante precision improved OOS risk-premium strategies across model classes.
4. Kelly et al. (2026 revision), *Artificial Intelligence Asset Pricing Models*. Large-scale transformer structures can reduce pricing errors, but this is asset-pricing evidence rather than proof of tradable alpha.
5. Linnainmaa & Roberts, *The History of the Cross Section of Stock Returns*. Many reported anomalies weaken materially OOS, motivating strict temporal validation and selection controls.

## Synthesis

The literature now supports a stronger separation of three questions:

1. Does the model predict?
2. Does the prediction survive leakage-safe OOS validation?
3. Does the resulting portfolio create incremental net utility after execution costs?

A fourth question should be added before promotion: does the result remain credible when the amount of information available for training is varied without increasing model complexity?

## New research direction

The project should prioritize information scaling before architecture scaling. For a frozen candidate architecture, compare expanding training histories against larger model variants under identical validation geometry. The primary outcome is net OOS utility and ranking stability, not training fit.

## Guardrails

- All preprocessing fit inside each training fold.
- Forward-label overlap explicitly purged.
- Embargo applied where horizon overlap can transmit information.
- Complete trial ledger includes failed/discarded searches.
- Costs include spread, commission, slippage and impact; stress at predefined multiples.
- Candidate selection occurs only on development folds; final OOS is untouched.
- Null/placebo runs use the same search workflow.

## Status

No new alpha claim is made. The repository still requires immutable candidate-level OOS prediction/position/return/cost artifacts before historical performance can be promoted.
