# Research 61 — Research-Design Perturbation and Economic Robustness

## Date
2026-09-20

## Literature

### 1. Lalwani & Jindal (2025/2026), European Financial Management
"Empirical Asset Pricing via Machine Learning: The Role of Research Design Choices"

The study evaluates 5,376 ML portfolios across seven models and eight research-design choices. Reported nonstandard errors can be up to five times conventional standard errors, and only about one-third of portfolios remain significant after transaction costs. The result is directly relevant to model research because choices such as training-window length, filters and portfolio construction are themselves sources of variation that can be mistaken for model skill.

Source: https://onlinelibrary.wiley.com/doi/10.1111/eufm.70033

### 2. Jo & Kim (2026), Financial Analysts Journal
"Rethinking Variable Importance in Machine Learning: An Economic Perspective on Empirical Asset Pricing"

The paper finds that in-sample variable importance can overfit and provide poor guidance, while economically constrained, out-of-sample evaluation is more informative. It also finds that microcaps can dominate apparent returns because they are costly to trade, illustrating why economic restrictions must be part of inference rather than a post-hoc adjustment.

Source: https://doi.org/10.1080/0015198X.2026.2621646

### 3. Grigoriev, Musaev & Grigorieva (2026), Complexity
"Cost-Aware Multiwindow Ensemble Decision Support for Nonstationary Foreign Exchange Markets"

The paper uses nonoverlapping walk-forward testing and selects aggregation/execution rules using cost-aware utility. Its design supports testing whether time-scale diversity and cost-aware selection improve net performance without treating gross predictive accuracy as sufficient evidence.

Source: https://onlinelibrary.wiley.com/doi/10.1155/cplx/1155228

### 4. Arian, Norouzi Mobarekeh & Seco (2024), Knowledge-Based Systems
"Backtest overfitting in the machine learning era: A comparison of out-of-sample testing methods in a synthetic controlled environment"

Controlled experiments report advantages for combinatorial purged cross-validation in reducing backtest overfitting relative to conventional approaches, especially under financial-data features such as nonstationarity and autocorrelation.

Source: https://doi.org/10.1016/j.knosys.2024.112477

## Research question

How much of candidate performance survives reasonable changes to research-design choices when the model, economic objective, and information set are otherwise held fixed?

## New principle

A candidate should not receive promotion credit merely because one arbitrary implementation choice produced a favorable result. Research-design choices must either be frozen ex ante or treated as explicit search dimensions and counted in the multiple-testing budget.

## Proposed perturbation battery

For every frozen candidate, evaluate a preregistered set of design perturbations:

1. training-window length;
2. rebalance/holding frequency;
3. feature normalization method, always fit only on available training data;
4. portfolio construction rule;
5. risk scaling rule;
6. execution lag convention;
7. transaction-cost/slippage stress level;
8. regime/subperiod partition.

The candidate is not allowed to choose the most favorable perturbation after seeing OOS results. All perturbations are recorded, including failures.

## Required outputs

For each candidate and perturbation:

- immutable OOS prediction artifact;
- timestamp and information-availability timestamp;
- realized gross return;
- turnover;
- spread/slippage/commission/impact components;
- net return;
- drawdown and downside metrics;
- benchmark-relative alpha;
- break-even cost;
- seed identifier;
- exact research-design configuration hash.

## Promotion implication

A candidate can only be considered robust if its economic conclusion is stable across the preregistered perturbation battery. A single favorable configuration is treated as a research-selection result, not robust evidence.

No alpha claim is made by this document.
