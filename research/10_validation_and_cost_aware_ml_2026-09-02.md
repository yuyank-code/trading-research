# Validation and cost-aware ML update — 2026-09-02

## Source-code finding

A fresh audit of `bitcoin-ml-trading/production_research.py` found that its reference docstring claimed leakage-safe validation, but the walk-forward implementation trained on `x.iloc[:start]`. Because the target is a 6-hour forward return, the final six training labels can overlap the first OOS period.

This was corrected in commit `11461d115264414eb136a70d02812e65d95ace22`: every fold now uses `train_end = start - horizon_bars`, with `HORIZON_BARS = 6`. `research_v2.py` already used the same horizon purge.

## Literature update

1. Bailey & López de Prado (2014), *The Deflated Sharpe Ratio*: multiple testing and non-normal returns inflate apparent Sharpe; model selection must account for the research trial count. DOI 10.3905/jpm.2014.40.5.094.
2. Bailey, Borwein, López de Prado & Zhu (2017), *The Probability of Backtest Overfitting*: selection among many alternatives can make the best historical strategy systematically unreliable OOS.
3. Bysik & Ślepaczuk (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs*: ~70,000 hourly BTC-USDT observations and 27 walk-forward folds; naive sign trading loses its edge at 10 bps in their setup, while forecast-magnitude/cost-aware filtering reduces turnover and restores profitability in selected configurations. Model dominance was not statistically established.
4. Huang, Wang & Jiang (2026), *Research on Machine Learning High-Frequency Trading Strategies Under Transaction Cost*: reports a large disconnect between predictive metrics and net trading results, and argues that transaction-cost filtering can matter more than incremental deep-model complexity. Treat as supporting evidence, not as proof of our edge.

## Testable hypotheses

- H30: correcting the production path's label purge changes results materially; if it does not, that is reassuring but must be demonstrated with frozen artifacts.
- H31: cost-aware abstention adds net OOS value without changing the frozen predictions.
- H32: the value of cost-aware filtering survives a predeclared fee/slippage grid.
- H33: candidate performance is stable across walk-forward folds rather than concentrated in a small number of periods.
- H34: search-adjusted evidence remains credible after counting all tested model/feature/threshold variants.

## Current status

No new profitability claim is made in this note. The production validation defect was corrected, but a numerical result is not promoted until the corrected pipeline is executed on the project's data and produces reproducible OOS prediction, trade, equity, fold, and cost-grid artifacts.

## Required evidence gate

A candidate must have: point-in-time features; horizon/event-time purge; no future-derived execution variables; frozen OOS predictions; next-bar execution; explicit fees/spread/slippage assumptions; fold-level metrics; cost sensitivity; and a complete trial registry for DSR/PBO interpretation.
