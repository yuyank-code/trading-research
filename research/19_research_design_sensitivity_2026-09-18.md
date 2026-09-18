# Research 19 — Research-design sensitivity and economic significance

**Date:** 2026-09-18

## New literature evidence

A 2026 European Financial Management study, *Empirical Asset Pricing via Machine Learning: The Role of Research Design Choices*, evaluates 5,376 portfolios generated from combinations of model and research-design choices. It reports that choices such as training-window length, data filters and portfolio construction materially affect strategy returns, and that nonstandard errors can be much larger than conventional standard errors. The practical implication is that the research protocol itself creates a multiple-testing/search problem.

A separate 2026 benchmark of deep-learning financial time series evaluates models on daily futures across commodities, equity indices, bonds and FX and emphasizes out-of-sample risk-adjusted returns, downside/tail risk, break-even transaction costs, random-seed robustness and computational efficiency. This reinforces that a single average Sharpe is inadequate as a promotion criterion.

A 2026 BTC walk-forward study using roughly 70,000 hourly observations finds that naive sign-based ML trading fails at 10 bps transaction costs, while a forecast-magnitude execution filter can reduce turnover and recover profitability in selected configurations. The paper does not establish formal dominance of XGBoost over neural alternatives, illustrating the distinction between descriptive ranking and statistical evidence.

Older but foundational evidence from Hsu and Kuan (2005) applies White's Reality Check and Hansen's SPA to a broad universe of technical rules. Their work demonstrates why family-level data-snooping corrections matter when many rules are searched.

## Research decision

The project should treat **research-design choices as searched hypotheses**, not as fixed implementation details. H61 therefore pre-registers a design-neighborhood test covering training windows, retraining frequency, horizon alignment, normalization, rebalance timing, universe filters, sizing and execution assumptions.

The final confirmation period must remain untouched until the design is frozen.

## Empirical status

No candidate model is promoted in this note. The repository does not currently contain the frozen market-data/prediction artifacts and complete trial matrix required for a numerical H61 run. We therefore report the methodological finding rather than fabricate OOS statistics.

## Promotion principle

The relevant question is not: "Which design produced the highest Sharpe?"

It is: "Does the economic edge remain present across a reasonable, pre-registered neighborhood of designs after costs, leakage controls and family-level multiple-testing correction?"
