# Research 81 — Complexity Budget vs Search Budget

Date: 2026-09-21

## Question
Does additional model complexity improve genuine out-of-sample trading utility, or is the apparent gain mostly the result of a larger adaptive search space?

## New literature

- Didisheim, Ke, Kelly & Malamud, *Complexity in Factor Pricing Models* (NBER WP 31689): theory and empirical evidence that, in their asset-pricing setting, expected OOS performance can improve with model parameterization; very large factor models can outperform simpler alternatives. This is important negative evidence against the blanket rule that more complexity is always harmful.
- Didisheim et al., *APT or AIPT? The Surprising Dominance of Large Factor Models* (NBER WP 33012, revised 2025): reports strong OOS performance for high-dimensional nonlinear factor models. Treat as domain-specific evidence, not proof that arbitrary trading-model complexity is beneficial.
- Kelly et al., *Artificial Intelligence Asset Pricing Models* (NBER WP 33351, revised June 2026): transformer-based SDF architecture reduces pricing errors relative to prior ML models, motivating a controlled test of richer cross-asset representations.
- Santoni, Jouanne & Scullin, *MinervaScore* (arXiv, Aug. 2026): emphasizes that post-selection robustness must account for DSR, PBO, SPA, track-record length and regime stability; their preregistered unseen-market test did not find a significant forward relationship for the score itself. This is useful evidence that validation layers should be treated as auditing tools, not alpha generators.

## Research interpretation

The relevant distinction is not simply simple-vs-complex. There are two separate degrees of freedom:

1. **Model capacity** — number/structure of parameters, interactions, factors or representation dimensions.
2. **Search capacity** — number of architectures, hyperparameters, features, windows, objectives and execution rules tried before selecting the reported model.

A complex model with a tightly pre-specified architecture can have fewer effective research degrees of freedom than a simple model chosen after a large adaptive search.

## Proposed controlled experiment

Compare low-, medium-, and high-capacity candidate classes under an identical research budget and identical information timestamps. For each class:

- pre-register the candidate grid;
- keep the final OOS period untouched;
- use purged/embargoed folds when labels overlap;
- record every attempted configuration, including failures;
- use the same portfolio construction and execution engine;
- evaluate commission, spread, slippage, nonlinear impact and borrow/funding;
- repeat at 1x, 1.5x and 2x cost;
- compare against strong non-ML baselines and matched-noise searches;
- apply selection-aware inference to the winner, not only standalone Sharpe.

## Decision rule

A higher-capacity class is promoted only if its selected candidate shows incremental net OOS utility over the best lower-capacity class after accounting for the complete search budget and all execution stresses. If the gain disappears after search adjustment, classify it as search inflation rather than model-capacity alpha.

## Current status

No numerical conclusion is claimed. The repository still lacks the immutable row-level OOS accounting artifact required for candidate promotion, and the known forward-label-overlap validation issue must be resolved before historical candidate results are trusted.

## Sources

- NBER WP 31689: https://www.nber.org/papers/w31689
- NBER WP 33012: https://www.nber.org/papers/w33012
- NBER WP 33351: https://www.nber.org/papers/w33351
- arXiv 2608.23808: https://arxiv.org/abs/2608.23808
