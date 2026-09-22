# Research 104 — Validation Budget and Track-Record Sufficiency

Date: 2026-09-22

## Research question

How should the project prevent a large model/strategy search from converting limited historical data into apparently strong but non-replicable out-of-sample performance?

## Literature evidence

1. Bailey & López de Prado (2014), *The Deflated Sharpe Ratio*, formalizes the need to correct Sharpe ratios for multiple testing and non-normal returns. A backtest selected from many trials has an inflated apparent Sharpe unless the search history is accounted for.
2. Jacquier, Muhle-Karbe & Mulligan (2025), *In-Sample and Out-of-Sample Sharpe Ratios for Linear Predictive Models*, shows that OOS replication deteriorates with strategy complexity, many weak signals, and limited training data, while additional training observations improve replication.
3. Santoni, Jouanne & Scullin (2026), *Equity Strategy Backtesting: Luck or Edge?*, proposes combining DSR, PBO, Superior Predictive Ability and minimum-track-record diagnostics. Importantly, its own unseen-market test did not establish a significant forward relationship for its composite score; therefore it should be treated as a validation/reporting framework, not a predictive edge.
4. Kim (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, reports substantial false positives from AUC-only validation and large transaction-cost erosion. The work motivates CPCV/PBO and economic validation, but is treated as preliminary because it is a 2026 posted manuscript rather than established consensus.
5. Saly-Kaufmann et al. (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*, evaluates models using OOS risk-adjusted returns, tail risk, breakeven transaction costs, seed robustness and computational efficiency rather than prediction metrics alone.

## Project implication

The project should track a **validation budget** as a first-class research object. Every model family, feature set, horizon, cost assumption and execution rule tried before the final holdout increases the effective number of trials, even if the individual variants are highly correlated.

The final OOS period must remain untouched until the research protocol is frozen. The project should also record the number of candidate variants actually inspected, not only the number ultimately reported.

## Proposed promotion gate

A candidate is not promoted unless all of the following are satisfied:

- point-in-time data and feature timestamps pass the leakage audit;
- forward labels are purged from training around each validation boundary and an embargo is applied where required;
- model selection occurs only inside the research/training period;
- final OOS is evaluated exactly once after protocol freeze;
- net returns include commission, spread, slippage, impact, borrow/funding where applicable, and turnover/capacity constraints;
- performance remains economically positive under pre-specified 1x, 1.5x and 2x cost stress;
- results are stable across seeds and reasonable regime partitions;
- multiplicity is reported and DSR/PBO or an appropriate family-wise/SPA-style test is applied;
- minimum track-record requirements are reported rather than inferred from a single Sharpe estimate;
- a null/placebo workflow using the same search budget does not reproduce the claimed effect.

## New hypothesis

**H155 — Search-budget-aware validation improves the reliability of model promotion.**

Compare the existing promotion workflow with a workflow that explicitly records effective trial count, reserves the final holdout, applies CPCV/PBO/DSR and enforces a minimum-track-record check. The test is not whether the stricter workflow produces higher returns; it is whether it reduces false discoveries on synthetic/null data while retaining known injected signals.

## Falsification criteria

The stricter gate fails as a methodology if, on synthetic data with known zero predictability, its false-positive rate is not materially below the less-controlled workflow, or if it systematically rejects injected signals that are strong enough to meet the pre-specified economic and statistical thresholds.

## Status

No trading alpha is claimed by this research note. It is a validation-protocol hypothesis only.
