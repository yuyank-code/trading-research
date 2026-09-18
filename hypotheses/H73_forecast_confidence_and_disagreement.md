# H73 — Forecast Confidence / Disagreement as a Trading Filter

## Status
Pre-registered hypothesis. No empirical result is claimed yet.

## Motivation
Recent financial ML literature suggests that the dispersion/precision of model forecasts can contain information beyond the point forecast itself. The useful question for this project is narrower: can forecast confidence improve the *economic conversion* of an already-frozen FX signal without changing the underlying predictor or increasing the research search space excessively?

## Hypothesis
Conditional on a frozen point forecast, trades taken only when forecast uncertainty is low (or when independent model forecasts agree) will have a higher net risk-adjusted return and/or lower turnover than trading every signal, after realistic execution costs.

## Falsifiable predictions
1. Confidence-filtered positions have higher net OOS Sharpe than the always-trade baseline, or materially lower drawdown at statistically indistinguishable Sharpe.
2. The result survives purging/embargo, untouched confirmation data, and realistic spread/slippage/impact assumptions.
3. The result remains directionally stable across chronological folds rather than being concentrated in one regime.
4. A matched-count random filter does not reproduce the observed improvement.
5. The confidence filter does not require retuning thresholds on the confirmation set.

## Experimental design

### Baseline
- Freeze the existing predictor and its point forecasts.
- Baseline position rule is unchanged.
- No new predictive features are added for the first test.

### Confidence constructions
Evaluate only a small pre-declared family:
- ensemble forecast dispersion across independently trained models;
- calibrated predictive residual/interval width where available;
- absolute forecast magnitude only as a simple control, not as a confidence proxy unless pre-declared.

### Validation
- Purged chronological walk-forward validation.
- Embargo any period needed to remove overlapping label information.
- Preserve one completely untouched confirmation block.
- Keep every tested threshold/candidate in the research ledger.

### Economic evaluation
For each candidate:
- gross and net return;
- Sharpe and Sortino;
- maximum drawdown and tail loss;
- turnover and trade count;
- break-even transaction cost;
- fixed and liquidity/size-conditioned execution costs;
- +25%, +50%, +100% adverse-cost stress;
- delayed and partial-fill stress where market data support it.

### Multiple-testing controls
- Search budget recorded before running the experiment.
- Deflated Sharpe Ratio and Probability of Backtest Overfitting.
- SPA / Reality Check at the family level.
- Model Confidence Set where candidate-level OOS return series are available.
- Synthetic zero-alpha controls using the same selection process.

## Failure conditions
Reject H73 if the apparent benefit:
- disappears after realistic costs;
- disappears on the untouched confirmation period;
- is reproduced by the matched-count placebo;
- is driven by a single fold/regime;
- requires post-hoc threshold selection;
- or fails the project's leakage/multiple-testing gates.

## Literature connection
Bali, Kelly, Mörke and Rahman (2026), *Machine Forecast Disagreement*, document a robust association between dispersion across machine forecasts and future stock returns, interpreted through heterogeneous beliefs and limits to arbitrage. Allena (2026), *Confident Risk Premiums and Investments Using Machine Learning Uncertainties*, reports improved out-of-sample investment performance when positions are restricted to forecasts with greater precision. These are not evidence that the same mechanism works in FX; they motivate a controlled, falsifiable test only.

## Decision rule
No promotion is allowed from H73 alone. Any surviving result must beat the frozen baseline under the same OOS periods, costs, search budget, and statistical controls. If the evidence is economically small or statistically indistinguishable, retain the simpler always-trade rule.
