# Research 56 — Multi-run Seed Stability and Winner's Curse in Stochastic Trading Models

## Literature
A 2026 Journal of Finance and Data Science study, *Unstable Gains: Multiplicity-Aware Evaluation of Financial Deep Reinforcement Learning*, reproduces financial DRL experiments across independent training runs and finds substantial Sharpe variation across random seeds. Apparent algorithmic outperformance frequently weakens or disappears under permutation testing and family-wise error correction. The paper argues that stochastic financial learners should be evaluated as distributions over learned policies rather than as deterministic backtests.

A 2026 large-scale benchmark of deep learning for financial time series likewise includes robustness to random seed selection, statistical significance, downside/tail risk and break-even transaction-cost analysis rather than reporting only a single Sharpe ratio.

## Implication for this project
Seed variation is not a cosmetic reproducibility check. It is another multiplicity dimension. Selecting the best checkpoint/seed can create a winner's-curse effect even when the dataset split is perfectly chronological.

## Testable implication
If a candidate's edge is structural, its net OOS advantage should remain detectable across a pre-registered distribution of independent seeds. If it exists only in a small subset of seeds, the evidence should be downgraded or rejected.

## Protocol added as H106
- freeze all non-seed choices before seed evaluation;
- run a pre-registered seed count (target >=20 where feasible);
- retain every seed's OOS predictions and net returns;
- evaluate the full seed distribution;
- correct for multiplicity;
- compare against the same baseline under the same seeds/splits;
- do not promote based on the maximum seed result.

## Interaction with existing controls
Seed-level analysis complements, rather than replaces, point-in-time controls, label-overlap checks, purged/embargoed OOS testing, realistic execution costs, search-budget accounting, placebo workflows, benchmark-relative alpha, and power calibration.

## Current evidence
No new alpha is claimed. The repository's existing numerical-validation blocker remains in force: corrected forward-label-overlap validation and an immutable candidate-level OOS prediction/return matrix are required before candidate performance can be trusted.
