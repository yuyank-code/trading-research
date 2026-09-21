# Research 89 — Stochastic Training Multiplicity and Reproducible OOS Evidence

Date: 2026-09-21

## Question

When a trading model is stochastic (random initialization, minibatch order, stochastic optimizer, RL exploration, hyperparameter search), does a single fitted model provide materially different evidence from the distribution of independently trained models?

## Literature

1. Gradzki (2026), *Unstable Gains: Multiplicity-Aware Evaluation of Financial Deep Reinforcement Learning*, Journal of Finance and Data Science. The paper argues that single-run DRL comparisons can overstate economic gains because performance varies materially across random seeds and model selection creates a winner's-curse effect. The useful methodological implication is to treat the training procedure as a stochastic experiment, not a single deterministic backtest.
2. Li, Mulvey & Fabozzi (2026), *Smart Trading Rule: A Modular Machine Learning Framework for Portfolio Optimization with Transaction Costs*, Journal of Financial Data Science 8(2), 145–175. The study separates portfolio prediction/allocation from cost-aware execution, supporting the use of a fixed execution layer when comparing model-training variants.
3. Abbade & Costa (2026), *Realistic Market Impact Modeling for Reinforcement Learning Trading Environments*. The authors show that nonlinear market-impact assumptions can materially change both absolute performance and relative algorithm rankings, so seed robustness must be evaluated under the same cost model rather than gross returns alone.
4. Harvey, Liu & Zhu (2016), *... and the Cross-Section of Expected Returns*, Review of Financial Studies. The broader lesson is that repeated model discovery creates a multiple-testing problem; apparent significance must be discounted for the number and dependence of trials.

## Research interpretation

A stochastic model family creates two multiplicity layers:

- search multiplicity across architectures, features, windows and objectives;
- optimization multiplicity across random seeds for the same specification.

Therefore, reporting the best seed is invalid model selection unless the seed itself was pre-specified. The proper object is a distribution of OOS outcomes for a locked specification.

## Proposed protocol

For every promoted candidate:

- lock architecture, feature set, window, objective and execution rule before the final OOS;
- train at least 10 independent seeds for development stability checks and preferably 20 for high-variance models;
- report median, interquartile range, 10th/90th percentiles and worst seed;
- report the fraction of seeds beating the strong baseline on net OOS utility;
- keep final OOS untouched until the specification and seed-count rule are frozen;
- apply the same commission, spread, slippage, impact, borrow and capacity assumptions to every seed;
- include 1x/1.5x/2x cost stress and execution-lag stress;
- treat seed selection as a trial and never cherry-pick the best seed for the headline result.

## Key principle

A model that wins only on its best seed is not robust evidence. A model whose OOS distribution shifts upward relative to the baseline across independent seeds is materially stronger evidence.

## Status

Hypothesis-generating. No claim of alpha is made until the corrected OOS runner and immutable execution ledger are available.
