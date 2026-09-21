# Research 96 — Cost-Aware Multiwindow Ensembles in Nonstationary FX

Date: 2026-09-22

## Question

Can a small, pre-specified ensemble of causal models operating at different lookback horizons improve net out-of-sample performance without creating an additional model-selection overfitting layer?

## Literature signal

Grigoriev, Musaev & Grigorieva (2026), *Cost-Aware Multiwindow Ensemble Decision Support for Nonstationary Foreign Exchange Markets*, evaluates transparent multiwindow experts on one-minute quotes for 16 major FX pairs using nonoverlapping walk-forward blocks. The supervisory layer weights experts using recent cost-aware utility and applies volatility/holding constraints. The paper is useful primarily as a protocol idea: time-scale diversity should be evaluated jointly with trading utility, rather than selecting one forecasting horizon by in-sample predictive accuracy.

Related 2026 evidence on ML trading under costs reports a large prediction-to-trading gap: complex models can improve forecasts while net returns deteriorate once turnover, spread and slippage are included. A separate BTC walk-forward study similarly finds naive sign trading fails at 10 bps and that cost-aware filtering can matter more than marginal architecture changes.

## Interpretation

The result is hypothesis-generating, not evidence that multiwindow ensembles produce transferable alpha. The main risk is that a meta-layer can become a second hyperparameter search over windows, weights and thresholds.

## Research design implication

Treat horizon count, weighting rule, and execution threshold as part of the research budget. The final OOS must be locked before any tuning. Any adaptive weighting must use only the immediately preceding training/meta window.

## Sources

- Grigoriev, D., Musaev, A., & Grigorieva, A. (2026). Cost-Aware Multiwindow Ensemble Decision Support for Nonstationary Foreign Exchange Markets. Complexity, 2026, 1155228. https://doi.org/10.1155/cplx/1155228
- Bysik, A., & Ślepaczuk, R. (2026). Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting. arXiv:2606.00060.
- Lalwani, V., Jindal, V., et al. (2026). Empirical Asset Pricing via Machine Learning: The Role of Research Design Choices. European Financial Management. https://doi.org/10.1111/eufm.70033

## Status

Literature-supported hypothesis. No alpha claim.
