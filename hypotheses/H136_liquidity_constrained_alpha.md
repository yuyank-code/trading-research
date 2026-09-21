# H136 — Liquidity-Constrained Alpha

## Hypothesis

A candidate trading signal that appears profitable in an unrestricted universe will show materially lower and more unstable net OOS performance when evaluated under a pre-declared, point-in-time tradability constraint. If the candidate retains incremental utility after liquidity filtering and liquidity-conditioned execution costs, the evidence for genuine alpha is stronger.

## Controlled comparison

- A: original candidate universe
- B: pre-declared liquidity-constrained universe
- C: liquidity-constrained strong baseline
- D: matched-noise/placebo signal under the same liquidity rules

The candidate model, features, timestamps, training procedure, and research/search budget are held fixed.

## Leakage controls

- liquidity features lagged to the decision timestamp;
- no full-sample ranks or future ADV;
- purged/embargoed validation for overlapping labels;
- all preprocessing fitted within training folds;
- final OOS remains untouched until the complete specification is frozen.

## Execution model

Apply spread, slippage and market impact as functions of liquidity/participation where data permit. Also run 1.5x and 2x cost stress and execution-lag perturbations.

## Promotion rule

Do not promote on gross Sharpe. Require positive incremental final-OOS net utility versus the strong liquidity-constrained baseline, stability across liquidity buckets and cost stresses, and no material placebo advantage.

## Current status

Design only. Numerical OOS evidence is not yet available because the repository still requires the corrected forward-label-overlap validation and immutable prediction-to-net-return artifact.
