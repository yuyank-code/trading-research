# Research Update 05 — Uncertainty and Search-Adjusted Validation

Date: 2026-09-01

## Literature update

Liao, Ma, Neuhierl & Schilling (2025), *The Uncertainty of Machine Learning Predictions in Asset Pricing*, develops confidence intervals for neural-network return forecasts and reports improved out-of-sample performance when forecast uncertainty is incorporated into investment decisions. This motivates testing uncertainty as a separate decision variable rather than automatically increasing model complexity.

Bailey & López de Prado (2014), *The Deflated Sharpe Ratio*, shows that reported Sharpe ratios are inflated by multiple testing and non-normal returns. Bailey, Borwein, López de Prado & Zhu (2017), *The Probability of Backtest Overfitting*, develops CSCV/PBO to quantify the probability that an apparently strong backtest is an overfit selection.

## New testable hypotheses

H13 — Forecast uncertainty contains incremental economic information after conditioning on predicted direction.

H14 — Calibrated probabilities are more useful for trade selection than raw classifier probabilities.

H15 — Uncertainty-adjusted sizing/filtering survives realistic fees and slippage better than fixed sizing.

H16 — Model value is regime-dependent; apparent aggregate OOS performance should decompose consistently across volatility/liquidity regimes.

## Controlled experiment design

Use the same frozen OOS predictions for all decision-policy comparisons:

1. fixed size / direction-only;
2. uncertainty threshold filter;
3. uncertainty-adjusted size;
4. probability-calibrated filter;
5. calibrated probability + uncertainty policy.

Do not retrain the predictive model between policy comparisons. This isolates decision-policy value from model-selection value.

Evaluate at minimum with fee/slippage grids rather than one optimistic assumption. Record turnover, trade count, win rate, expectancy, profit factor, max drawdown, Sharpe/Sortino, and performance degradation as costs rise.

## Leakage and overfitting controls

- All uncertainty/calibration parameters must be selected only inside the training/validation period.
- The final OOS interval remains untouched until the policy is frozen.
- Event-aware purge/embargo is required when forecast labels overlap.
- Every candidate policy and failed experiment enters the trial registry.
- DSR/PBO/CSCV analysis must include the search history when interpreting the eventual winner.

## Current conclusion

No new trading edge is established by the literature alone. The useful result is a narrowly testable hypothesis: uncertainty may be valuable as a trade-selection/sizing signal, but only if its incremental OOS benefit survives costs and search adjustment.

The next valid experiment is therefore a frozen-prediction policy comparison, not another unrestricted model search.

## Sources

- Bailey & López de Prado (2014), Journal of Portfolio Management: https://doi.org/10.3905/jpm.2014.40.5.094
- Bailey, Borwein, López de Prado & Zhu (2017), Journal of Computational Finance: https://doi.org/10.21314/JCF.2016.322
- Liao, Ma, Neuhierl & Schilling (2025), SSRN: https://doi.org/10.2139/ssrn.5160731
