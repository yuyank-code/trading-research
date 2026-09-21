# Research 75 — Uncertainty-Adjusted Selection

## Evidence reviewed

A January 2026 working paper by Liu, Luo, Wang, and Zhang, *Uncertainty-Adjusted Sorting for Asset Pricing with Machine Learning*, proposes replacing point-prediction sorting with uncertainty-adjusted prediction bounds. Across U.S. equity panels and multiple ML models, the authors report improved portfolio performance, with the main channel being lower volatility; gains are strongest for flexible ML models. The paper also reports robustness to partial or misspecified uncertainty information.

This is a working paper/preprint, so the result is treated as hypothesis-generating rather than established evidence.

A July 2026 NBER working paper by Koijen and Levy provides an independent methodological warning: historical AI backtests can suffer look-ahead bias, and their real-time benchmark restricts every signal to information available at the announcement time. This supports treating information availability and timestamp discipline as first-class evaluation constraints.

A 2026 BTC walk-forward study provides complementary economic evidence: naive sign trading loses profitability once 10-bps transaction costs are imposed, while cost-aware forecast filtering can restore profitability in selected configurations. The authors do not establish formal statistical dominance of XGBoost, so the result is not used as evidence for a specific model class.

## Research implication

The project should test whether forecast uncertainty contains useful information for **trade selection**, not whether a more complicated model has a higher in-sample predictive score.

The key economic comparison is:

**point forecast -> portfolio** versus **uncertainty-adjusted forecast -> portfolio**, with identical timestamps, candidate universe, execution, and cost assumptions.

## Failure condition

If the uncertainty-adjusted method improves gross returns but loses its advantage after costs, lag stress, or selection-aware inference, the hypothesis is rejected. If the advantage appears only after tuning uncertainty thresholds on the final OOS sample, it is rejected as leakage/selection bias.

## Sources

- Liu, Luo, Wang, Zhang (2026), *Uncertainty-Adjusted Sorting for Asset Pricing with Machine Learning*.
- Koijen & Levy (2026), NBER Working Paper 35431, *Assessing the Benefits of Optimized Agentic AI Systems for Asset Pricing*.
- Bysik & Ślepaczuk (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*.
