# H121 — Design-Perturbation Stability of Candidate Ranking

**Date:** 2026-09-21  
**Status:** preregistered hypothesis; numerical execution pending immutable OOS artifacts

## Hypothesis

A genuinely useful trading signal should retain a meaningful portion of its net out-of-sample advantage when reasonable, pre-specified research-design choices are perturbed without allowing re-selection on the final test period.

The alternative is that apparent alpha is primarily a consequence of one favorable training window, portfolio construction rule, rebalance frequency, or execution assumption.

## Literature motivation

Lalwani et al. (2025/2026) evaluate 5,376 ML portfolios and report large variation from research-design choices including training-window length, data filters, and portfolio construction; nonstandard errors can be much larger than conventional standard errors, and only about one-third of portfolios remain significant after transaction costs. This motivates treating design sensitivity as part of the evidence rather than an implementation detail.

Kim (2026) reports a statistical-economic disconnect across hundreds of cryptocurrency strategy variants and shows that net Sharpe deteriorates with trading frequency. A 2026 large-scale deep-learning benchmark evaluates OOS performance together with significance, tail risk, break-even transaction costs, random-seed robustness and computational efficiency. These findings support a design-robustness gate rather than a single best-specification backtest.

## Controlled experiment

Freeze the candidate model and all learned parameters from the training/validation protocol. Evaluate the same candidate under a small, pre-declared perturbation grid:

1. training history: baseline / shorter / longer where feasible;
2. rebalance frequency: baseline / slower;
3. portfolio construction: baseline / volatility-scaled or capped alternative;
4. universe filter: baseline / stricter liquidity floor;
5. execution lag: baseline / one additional bar;
6. cost model: flat / liquidity-conditioned / 1.5x variable cost.

No final-period tuning is permitted. The perturbation grid is fixed before inspecting final OOS results.

## Primary test

Measure whether the candidate's **net OOS utility advantage over the frozen baseline** remains positive across the pre-specified perturbation grid.

Report:

- fraction of perturbations with positive incremental utility;
- median and worst-case incremental utility;
- rank correlation of candidate ordering across perturbations;
- turnover and gross-to-net decay;
- maximum drawdown and tail loss;
- break-even one-way cost;
- seed dispersion where stochastic models are used.

## Promotion rule

A candidate cannot be promoted solely because it wins the baseline specification. It must satisfy the project's existing leakage, null, multiple-testing and cost gates and must show non-fragile economics across the pre-specified perturbation set.

The perturbation analysis is diagnostic, not permission to optimize on the final OOS period.

## Leakage controls

All preprocessing, scaling, liquidity thresholds, feature selection, hyperparameters and cost calibration remain fit only within each training/validation window. Any forward-looking liquidity or realized-volatility measure is excluded unless it is explicitly available at the decision timestamp.

The immutable artifact chain must link decision timestamp -> feature snapshot -> model version -> prediction -> position -> turnover -> realized return -> cost components -> net return.

## Falsification outcomes

- **Robust:** positive incremental utility in most perturbations and no severe single-assumption dependency.
- **Fragile:** baseline winner collapses under one or more plausible pre-specified changes.
- **Rejected:** candidate loses to the frozen baseline after costs across most perturbations.

No numerical alpha claim is valid until corrected forward-label-overlap validation and immutable candidate-level OOS artifacts are available.

## Sources

- Lalwani, V. et al. (2026), *Empirical Asset Pricing via Machine Learning: The Role of Research Design Choices*, European Financial Management, DOI: 10.1111/eufm.70033.
- Kim, J. (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, SSRN 6508779.
- Saly-Kaufmann, A., Wood, K., Calliess, J.P. & Zohren, S. (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*, arXiv:2603.01820.
