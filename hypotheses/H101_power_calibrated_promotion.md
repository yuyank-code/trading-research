# H101 — Power-Calibrated Promotion Thresholds

## Claim

A candidate should not be promoted merely because its OOS estimate clears a statistical significance threshold. Promotion should also require that the confirmation sample has adequate power to distinguish the candidate's estimated net edge from economically irrelevant performance.

## Motivation

Recent 2026 strategy-discovery research emphasizes that credible certification of moderate edges can require substantially larger samples than naive Sharpe/significance rules imply. Large-scale financial ML benchmarks also increasingly report breakeven transaction costs, tail risk, and seed robustness rather than Sharpe alone. This suggests that an apparently significant result can still be too imprecise to support deployment.

## Test

For each frozen candidate and transparent baseline, pre-specify an economically meaningful minimum effect size in net annualized Sharpe/utility and estimate the effective confirmation-sample size after accounting for serial dependence and overlapping positions.

Evaluate:

1. power under planted small, medium, and null effects;
2. confidence-interval width for the candidate-minus-baseline net return/utility difference;
3. sensitivity to autocorrelation and volatility clustering;
4. power after realistic transaction costs, slippage, impact and turnover;
5. false-promotion rate when the true incremental effect is below the minimum economic threshold.

The power calculation itself must be frozen before confirmation results are inspected.

## Primary outcome

Probability that the promotion procedure correctly rejects candidates whose true incremental net edge is below the minimum economically meaningful threshold, while retaining adequate power for the pre-specified target effect.

## Falsification

H101 fails if the promotion gate frequently certifies economically trivial or negative incremental effects, or if its claimed power materially exceeds empirical power in controlled planted-effect experiments.

## Promotion rule

Promotion requires both statistical evidence and a confidence interval/power result consistent with a practically meaningful incremental net edge. Statistical significance alone is insufficient.
