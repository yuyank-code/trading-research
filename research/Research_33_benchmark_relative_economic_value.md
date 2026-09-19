# Research 33 — Benchmark-Relative Net Economic Value

## Why this matters

The project has accumulated many robustness dimensions—leakage, embargo, holding period, capacity, abstention and calibration. A remaining risk is **benchmark insufficiency**: a candidate may look attractive in isolation while failing to demonstrate that the model adds value over a transparent, implementable alternative.

Recent work makes this a live concern. Gencçay (2026) reports that leakage-safe, search-aware evaluation can reject strategies that look successful under less disciplined search, while certifying simple passive benchmarks under identical realistic costs. A 2026 large-scale financial deep-learning benchmark similarly evaluates models on OOS risk-adjusted performance, statistical significance, tail risk, break-even transaction costs, seed robustness and computational efficiency. citeturn0search13turn0academia36

The 2025 *Review of Financial Studies* re-evaluation of ML trading evidence is an additional warning: look-ahead correction can erase an apparently strong alpha result. citeturn0search5

## Research question

Does the candidate model add statistically credible **net economic value relative to a pre-specified transparent benchmark**, using the same causal information set and execution assumptions?

## Testable protocol

1. Freeze the candidate family, feature set, benchmark definitions, execution assumptions and search budget.
2. Correct the known forward-label overlap issue before numerical confirmation.
3. Build an immutable candidate-level OOS matrix containing predictions, positions, gross returns, costs, net returns and benchmark returns.
4. Compare every candidate against the same fixed benchmark dates and tradability mask.
5. Use realistic commissions, spread, slippage, nonlinear impact, turnover and capacity assumptions.
6. Keep the confirmation set untouched by model or benchmark tuning.
7. Report paired candidate-minus-benchmark returns, net Sharpe/Sortino, drawdown, tail losses and break-even costs.
8. Apply DSR/PBO, SPA/Reality Check and MCS across the entire searched candidate family.
9. Repeat under adverse execution-cost stress and across meaningful subperiods/regimes.
10. Run matched-count random and synthetic zero-alpha controls to determine whether the observed benchmark-relative improvement is distinguishable from selection luck.

## Pre-specified benchmark family

- zero-return/cash baseline;
- passive instrument benchmark where applicable;
- simple lagged-return or moving-average rule where appropriate;
- simple cost-aware sign/magnitude rule using only information available at the decision time.

The benchmark family itself is not allowed to expand after confirmation begins.

## Decision rule

**Promote only if** a candidate demonstrates positive benchmark-relative net economic value on untouched confirmation, survives realistic adverse-cost assumptions, remains directionally stable across subperiods, and survives the project's multiple-testing and placebo controls.

**Reject if** the candidate only has positive absolute returns, if the advantage disappears after costs, if it is concentrated in one period, or if comparable placebo candidates obtain similar benchmark-relative gains.

## Current status

No numerical result is claimed. The repository's README states that corrected validation is required because of previously identified forward-label overlap and that older model results should not yet be treated as trustworthy. The frozen candidate-level OOS prediction/return matrix is also not yet present. fileciteturn1file0

## Sources

- Gencçay (2026), *What survives honest evaluation? Leakage-safe, search-aware assessment of LLM-driven trading strategy discovery*.
- Saly-Kaufmann, Wood, Peter-Calliess & Zohren (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*.
- Zhang, Zhu & Linnainmaa (2025), *Man versus Machine Learning Revisited*, *Review of Financial Studies*.
