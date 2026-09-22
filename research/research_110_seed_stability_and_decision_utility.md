# Research 110 — Seed Stability and Decision Utility

Date: 2026-09-22

## New literature

Recent 2026 work on financial deep reinforcement learning reports that single-run results can give a false impression of stable economic outperformance: Sharpe and alpha can vary materially across independent random seeds, with apparent gains disappearing after uncertainty is aggregated across runs. This is directly relevant to any stochastic learner or stochastic hyperparameter search.

A 2026 Smart Predict-then-Optimize paper argues that improvements in point forecasts need not translate into better portfolio decisions once costs and constraints are included; it motivates evaluating the downstream decision objective rather than prediction error alone.

A 2026 BTC walk-forward study likewise finds a prediction-to-trading disconnect: naive sign strategies collapse under 10 bps of costs, while cost-aware signal filtering can materially improve net outcomes, but model dominance is not statistically established.

## Research implication

For this project, one frozen candidate specification is not a sufficient unit of evidence if training or selection is stochastic. The unit of evidence should be the distribution of paired OOS incremental utility across independent seeds, with the final untouched OOS period evaluated only after the specification is frozen.

## Proposed protocol

For each candidate:

1. Freeze data lineage, splits, feature set, hyperparameter search space, execution model and promotion threshold.
2. Run at least 10 independent training/selection seeds when the algorithm is stochastic.
3. Record paired net OOS utility versus the same frozen baseline on identical timestamps.
4. Report median, mean, dispersion, lower quantiles and worst seed; do not select the best seed.
5. Apply dependence-aware inference to the seed-aggregated paired differential.
6. Repeat under baseline, 1.5x and 2x cost assumptions and execution-delay stress.
7. Treat seed instability as a failure mode even if the pooled mean is positive.
8. Preserve every seed artifact so post-hoc seed selection is impossible.

## Important limitation

This is a validation hypothesis, not evidence of profitable alpha. The repository's PIT and forward-label-overlap requirements remain prerequisites for trusting historical OOS results.
