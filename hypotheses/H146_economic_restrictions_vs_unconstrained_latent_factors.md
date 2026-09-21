# H146 — Economic Restrictions vs Unconstrained Latent Factors

Date: 2026-09-22

## Hypothesis

Economically motivated restrictions on learned latent factors improve genuine out-of-sample trading utility by reducing unstable factor estimation, rather than merely improving in-sample fit or acting as an exposure/turnover shrinker.

## Controlled arms

1. Strong linear/shrinkage factor baseline.
2. Unconstrained nonlinear latent-factor model.
3. Economically restricted nonlinear latent-factor model.
4. Restricted model with the economic targets permuted within the training sample (restriction placebo).
5. Exposure/turnover-matched shrinkage control.

## Falsification criteria

The hypothesis is rejected if the restricted model's apparent improvement disappears under any of:

- untouched final OOS;
- purged/embargoed validation;
- point-in-time feature construction;
- restriction-target permutation;
- exposure/turnover matching;
- 1x/1.5x/2x transaction-cost stress;
- execution-lag stress;
- seed robustness;
- regime/tail breakdown;
- search-aware multiple-testing correction.

## Leakage controls

Economic targets, factor labels, normalization parameters and any macro state used to constrain the representation must be timestamped by their earliest tradable availability. Revised macro/fundamental values cannot be substituted for the historical information set.

## Promotion gate

Promotion requires a pre-specified improvement in net OOS utility over both the unconstrained model and strong shrinkage baseline, with the placebo unable to reproduce the effect. A reduction in turnover or volatility alone is insufficient evidence of predictive information.

## Current status

Protocol only. No numerical OOS result is promoted until the repository's corrected forward-label-overlap validation and immutable prediction-to-net-P&L ledger are operational.
