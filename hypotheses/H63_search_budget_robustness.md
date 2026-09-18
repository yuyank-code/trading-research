# H63 — Search-Budget / Research-Process Robustness

## Status

Pre-registered hypothesis. No model promotion and no profitability claim.

## Motivation

A trading research process can overfit even when individual backtests use leakage-safe time splits. If researchers increase the number of candidate strategies, parameter combinations, horizons, filters, or execution variants and retain the best result, the reported winner inherits selection bias. The Deflated Sharpe Ratio (DSR) was introduced specifically to correct performance inflation from multiple testing and non-normal returns (Bailey & López de Prado, 2014).

Recent work also demonstrates that an apparently strong trading result can survive conventional statistical corrections when the underlying information set is causally contaminated; therefore causal leakage gates must remain upstream of search-budget corrections.

## Hypothesis

If apparent trading alpha is primarily search luck rather than persistent signal, increasing the research search budget will increase the best development/in-sample Sharpe faster than it improves untouched out-of-sample performance. OOS rank stability should deteriorate or remain weak, while DSR/PBO/SPA evidence should fail to improve proportionally.

## Search budgets

Run the identical discovery workflow at pre-declared budgets:

- 10 candidates
- 25 candidates
- 50 candidates
- 100 candidates
- 250 candidates
- 500 candidates

A candidate means a complete strategy specification, including model, feature set, hyperparameters, threshold, holding horizon, sizing rule, and execution policy. All attempted candidates must remain in the registry, including failures.

## Information boundary

Every run must satisfy:

`event_time -> available_time -> decision_time -> order_time -> fill_time`

and `available_time <= decision_time` for every feature and execution input. Preprocessing must be fitted only inside the permitted training window. Label-overlap purge and embargo must be applied before model fitting.

## Evaluation protocol

1. Freeze the data snapshot and feature definitions.
2. Freeze the search-budget schedule before looking at results.
3. Use the same development, validation, and untouched confirmation periods for every budget.
4. Use purged/embargoed walk-forward or CPCV where label structure requires it.
5. Apply explicit fees, spread, slippage, latency and market-impact assumptions.
6. Stress execution costs by +25%, +50%, and +100%.
7. Record gross and net Sharpe, Sortino, max drawdown, turnover, trade count, hit rate, expected return per trade, and break-even cost.
8. Measure OOS rank correlation between development selection and confirmation performance.
9. Compute DSR using the complete trial history; estimate PBO where applicable.
10. Apply family-level Reality Check / SPA when the candidate return series permit it.
11. Run the identical discovery workflow on synthetic zero-alpha data to measure the false-discovery rate of the research process itself.
12. Do not use the confirmation period to tune any parameter or choose among budgets.

## Primary diagnostics

The key comparison is not simply the highest Sharpe. Report, by search budget:

- best development Sharpe;
- median development Sharpe;
- selected candidate net OOS Sharpe;
- median candidate net OOS Sharpe;
- OOS rank correlation;
- DSR;
- PBO;
- SPA / Reality Check result;
- break-even transaction cost;
- turnover and capacity proxies;
- performance under adverse cost stress.

## Falsification criteria

H63 is falsified if larger search budgets produce a statistically credible and economically meaningful improvement in untouched OOS performance that remains stable across cost stress, regimes, seeds, and multiple-testing corrections.

The research process is considered search-overfit if best development Sharpe rises materially with budget while selected OOS performance does not, OOS rank correlation is weak, or null-data runs frequently produce apparently strong winners.

## Promotion rule

No candidate is promoted from H63 alone. Promotion requires all upstream causal/leakage gates plus cost-aware OOS evidence, family-level multiple-testing controls, stability diagnostics, and an untouched confirmation result.

## Literature

- Bailey, D. H. & López de Prado, M. (2014), *The Deflated Sharpe Ratio: Correcting for Selection Bias, Backtest Overfitting, and Non-Normality*, Journal of Portfolio Management 40(5), 94–107. DOI: 10.3905/jpm.2014.40.5.094.
- Bailey, D. H. & López de Prado, M. (2021), *How “Backtest Overfitting” in Finance Leads to False Discoveries*, Significance.
- Gençay, E. (2026), *What survives honest evaluation? Leakage-safe, search-aware assessment of LLM-driven trading strategy discovery*, arXiv:2608.27734. Use as recent methodological evidence, not as established consensus.
