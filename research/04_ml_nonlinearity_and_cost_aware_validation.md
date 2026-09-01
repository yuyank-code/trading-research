# Research Update 04 — Nonlinearity, Costs, and Validation

Date: 2026-09-01

## New literature

### Gu, Kelly & Xiu (2020), *Empirical Asset Pricing via Machine Learning*

The paper compares linear models, dimension reduction, boosted trees, random forests and neural networks for asset-pricing prediction. Its important implication for this project is not that deep models are automatically superior, but that nonlinear interactions can contain incremental information beyond linear specifications. The authors identify momentum, liquidity and volatility among dominant signals. Source: NBER Working Paper 25398 and the published *Review of Financial Studies* article, DOI 10.1093/rfs/hhaa009.

### Hsu & Kuan (2005), *Reexamining the Profitability of Technical Analysis with Data Snooping Checks*

The study explicitly applies White's Reality Check and Hansen's SPA to a broad universe of technical rules. It demonstrates why technical-rule profitability has to be evaluated jointly with the search over rules and with transaction costs. Its findings vary by market maturity, reinforcing the need for market-specific replication rather than assuming a published technical anomaly transfers unchanged.

### Holden & Holden (2013), *Optimal rebalancing of portfolios with transaction costs*

The theoretical result is directly relevant to implementation: proportional transaction costs create a no-trade region, and optimal behavior is not equivalent to continuously forcing the portfolio back to a target. This motivates testing turnover-control policies as part of the strategy rather than treating costs as a simple after-the-fact deduction.

## New testable hypotheses

### H13 — Nonlinear incremental value

A tree/boosting model should only be promoted if it improves untouched OOS economic performance relative to a frozen linear benchmark after costs, not merely predictive metrics in the training/validation search.

### H14 — Interaction stability

If nonlinear gains are genuine, the same broad interactions should recur across independent chronological folds rather than appearing in only one regime.

### H15 — Cost-aware signal threshold

The minimum prediction confidence required to trade should increase when estimated execution costs rise. A signal that is profitable only under optimistic costs is not robust.

### H16 — No-trade band

Reducing unnecessary turnover through a no-trade/partial-adjustment rule should improve net risk-adjusted performance when gross signal strength is insufficient to overcome implementation costs.

## Pipeline changes required

1. Freeze a linear benchmark before nonlinear model selection.
2. Record every model/feature/threshold/cost configuration in the trial registry.
3. Use event-aware purging based on the actual label horizon.
4. Apply an embargo after test windows when serial dependence or label overlap warrants it.
5. Keep one untouched final OOS period unavailable to all selection decisions.
6. Report gross and net performance under a cost grid rather than a single optimistic cost assumption.
7. Compare predictive metrics (log loss/Brier/AUC) separately from economic metrics (net return, Sharpe, drawdown, turnover, profit factor).
8. Apply search-aware inference such as SPA/Reality Check and DSR/PBO-style diagnostics before calling a selected strategy robust.

## Important finding

The literature supports testing nonlinear interactions, but it does not justify simply replacing the current model with a tree or neural network. The correct experiment is an incremental-value test against a frozen benchmark with a controlled search budget.

## Current failure/risk

The project still lacks a demonstrated, independently validated economic edge after the complete search history is accounted for. Until the stricter validation layer is executed on the actual candidate outputs, no model should be labeled production-ready.

## Sources

- Gu, Kelly & Xiu (2020), NBER WP 25398 / *Review of Financial Studies* 33(5), 2223–2273. DOI: 10.1093/rfs/hhaa009.
- Hsu & Kuan (2005), *Journal of Financial Econometrics* 3(4), 606–628. DOI: 10.1093/jjfinec/nbi026.
- Holden & Holden (2013), *Stochastics* 85(3), 371–394. DOI: 10.1080/17442508.2011.651219.
