# H106 — Multi-run Seed Stability as a Promotion Gate

## Hypothesis
For stochastic/non-convex trading learners, a candidate's economic advantage must persist across independent training seeds. A single favorable seed should not qualify for promotion.

## Motivation
Recent 2026 evidence shows financial deep-reinforcement-learning Sharpe ratios and algorithm rankings can vary materially across random seeds; multiplicity-aware evaluation can eliminate apparent outperformance. The finding is broader than DRL: any stochastic learner should be evaluated as a distribution of learned policies, not one fitted policy.

## Pre-registered test
1. Freeze dataset snapshot, feature graph, target, split schedule, execution simulator, costs, slippage, impact and capacity assumptions.
2. Freeze model architecture and hyperparameters before seed evaluation.
3. Train at least 20 independent seeds where computationally feasible.
4. Preserve every seed's OOS predictions, trades and net returns.
5. Report median, mean, dispersion, lower quantiles and probability of beating the transparent baseline.
6. Apply multiplicity-aware inference across seeds and candidate models.
7. Compare the candidate's seed distribution with baseline uncertainty, not only its best seed.

## Promotion criterion
Promotion requires that the pre-registered economic edge is positive for the seed distribution and not attributable to a small number of favorable seeds. A best-seed result alone is explicitly insufficient.

## Failure test
A candidate fails if materially positive performance is concentrated in a small minority of seeds, if seed rankings are unstable, or if the apparent advantage disappears after seed-level multiplicity correction.

## Required artifacts
- immutable seed manifest;
- candidate-level OOS prediction/return matrix;
- per-seed net-return series;
- cost/slippage assumptions;
- seed-level statistical report;
- baseline comparison;
- promotion decision.

## Status
Design committed. Numerical execution remains blocked until the immutable candidate-level OOS prediction/return matrix and corrected forward-label-overlap validation are available.
