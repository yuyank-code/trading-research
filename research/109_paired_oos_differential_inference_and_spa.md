# Research 109 — Paired OOS Differential Inference and Search-Aware Model Comparison

Date: 2026-09-22

## Core question

Can a candidate model demonstrate incremental economic value over a frozen baseline after accounting for dependence, transaction costs, and the full candidate search?

## Literature update

White, Sullivan and Timmermann's Reality Check established that selecting the best rule from a large family creates data-snooping bias and that the bootstrap should evaluate the full rule universe. Hansen's Superior Predictive Ability framework was designed to provide a less conservative comparison while still addressing data snooping. Stepwise SPA extends this logic to large predictive-model families. These methods are not substitutes for point-in-time data, OOS separation, or a complete research ledger; they only address the statistical consequences of a declared candidate universe.

Recent 2026 work reinforces the economic side: large ML asset-pricing experiments find that research-design choices materially change returns, while transaction-cost-aware BTC walk-forward studies find that prediction improvements can disappear after realistic frictions. Realistic market-impact experiments also show that changing the cost model can change model rankings.

## New protocol

The project should report paired net-return differences against frozen baselines, rather than ranking candidates by standalone Sharpe. The primary statistic is the mean/utility difference per decision period, with dependence-aware block/bootstrap inference. Secondary evidence includes SPA/Reality Check-style search adjustment over the declared candidate family.

The candidate family must include every model that was actually evaluated, including discarded architectures, feature sets, horizons, seeds, thresholds and execution variants. If the registry is incomplete, the result is BLOCKED rather than treated as a clean statistical test.

## Required controls

- point-in-time information availability;
- purge/embargo for overlapping labels;
- identical timestamps, universe, portfolio construction and execution assumptions;
- baseline, 1.5x and 2x transaction-cost scenarios;
- liquidity-conditioned costs when available;
- turnover-matched placebo;
- untouched final holdout;
- block/bootstrap or another dependence-aware confidence procedure;
- full-trial accounting before any selection-adjusted test;
- predefined regime/subperiod analysis.

## Interpretation

A statistically positive candidate-vs-baseline difference is not sufficient for promotion. It must also remain economically positive under cost stress and pass the project's leakage and search-budget gates. A failure of the paired test is a meaningful negative result even when the candidate has an attractive standalone Sharpe.

## Status

Methodology upgrade. No model performance claim is made by this research note.
