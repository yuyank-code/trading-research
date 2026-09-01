# Research Update 05 — Forecast Uncertainty and Evaluation Discipline

Date: 2026-09-01

## New literature

### 1. Forecast uncertainty in ML asset pricing
Liao, Ma, Neuhierl and Schilling (2025) explicitly model uncertainty in neural-network expected-return forecasts and report that uncertainty-aware portfolio construction can improve out-of-sample performance. This motivates testing whether the trading system should use forecast uncertainty as a position-size/trade-filter input rather than treating model probability as exact.

Source: SSRN, *The Uncertainty of Machine Learning Predictions in Asset Pricing*.

### 2. Macro-event conditional prediction
Liao, Ma, Ding and Jiang (2024) find that separating macro-announcement days from regular days can improve ML return forecasting. For BTC, the directly transferable hypothesis is not the equity result itself; it is that information regimes may change predictive relationships. We should therefore test event/regime-conditioned performance only with timestamps available ex ante.

### 3. Backtest-overfitting methodology
Bailey et al. show that trying more strategy configurations increases the probability of selecting an overfit winner. DSR adjusts for multiple testing and non-normality; PBO/CSCV estimates the probability that the selected backtest is overfit. These remain mandatory gates.

### 4. Sharpe-ratio uncertainty
Lo (2002/2003) shows that Sharpe-ratio inference is affected by serial correlation and that naive annualization can be materially misleading. Our reporting therefore must derive Sharpe from appropriately aggregated returns and avoid assuming IID observations.

## New testable hypotheses

### H13 — Uncertainty-aware sizing
Given the same directional probability, do lower-uncertainty predictions produce better net outcomes than high-uncertainty predictions? Test by freezing the prediction model and comparing: fixed size, uncertainty-shrunk size, and uncertainty-based trade filtering.

### H14 — Calibration before thresholding
Does probability calibration improve net trading performance versus using raw model probabilities? Compare raw probabilities with calibration fit strictly inside the training/validation window. The final OOS set remains untouched.

### H15 — Regime-conditioned model value
Do candidate models retain incremental OOS value across volatility/liquidity regimes, or is performance concentrated in one historical state? Regimes must be defined using information available at the signal timestamp.

### H16 — Cost-aware ranking
Does the model with the best predictive metric remain the best model after fees, slippage, turnover and trade-selection rules? Model selection must use net economic metrics only inside the training/validation process; the final OOS period cannot determine the winner.

## Pipeline changes required

1. Add probability calibration as an explicit validation stage.
2. Record calibration error (Brier/log loss) separately from trading performance.
3. Record prediction uncertainty and test it without allowing future outcomes into sizing decisions.
4. Add regime-stratified OOS reports.
5. Report Sharpe with serial-correlation-aware interpretation; do not treat daily observations as automatically independent.
6. Keep the final OOS period completely untouched until all model, threshold, calibration and cost decisions are frozen.

## Current project conclusion

No new profitable edge has been established by this literature. The strongest actionable idea is to test whether **forecast uncertainty contains useful information about trade quality**. This is a lower-risk research extension because it can be evaluated on the existing prediction pipeline without adding a large new feature search.

## Failure/guardrail

Do not use uncertainty as a new optimization dimension until the existing search history is registered. Otherwise uncertainty thresholds become another source of multiple-testing bias. Any uncertainty-based improvement must survive the same OOS, cost, purge/embargo and search-adjusted evaluation gates.

## References

- Liao, Y., Ma, X., Neuhierl, A., Schilling, L. (2025), *The Uncertainty of Machine Learning Predictions in Asset Pricing*.
- Liao, C., Ma, T., Ding, H., Jiang, F. (2024), *Macroeconomic Announcement and Machine Learning for Asset Pricing*.
- Bailey, D. H., Borwein, J., López de Prado, M., Zhu, Q. J. (2015), *The Probability of Backtest Overfitting*.
- Bailey, D. H., López de Prado, M. (2014), *The Deflated Sharpe Ratio*.
- Lo, A. W. (2002/2003), *The Statistics of Sharpe Ratios*.
