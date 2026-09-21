# Research 86 — Economic Feature Pruning vs Full Feature Sets

## Question
Can removing weak or economically redundant predictors improve out-of-sample trading performance without becoming another source of data snooping?

## Evidence

Jo and Kim (Financial Analysts Journal, 2026) show that in-sample variable importance is an unreliable guide to economic value. Their out-of-sample analysis finds that some predictors have negative economic importance and that removing such predictors can improve risk-adjusted portfolio performance. They also emphasize that microcaps can dominate apparent ML gains, reinforcing the need to evaluate feature value under realistic economic restrictions.

Lalwani, Meshram and Jindal (European Financial Management, 2026) show that research-design choices themselves create large dispersion in ML portfolio returns across thousands of specifications. This means feature selection must be treated as a research choice and charged against the same selection budget as model architecture, window length and portfolio construction.

Chen, Cheng, Liu and Tang (NBER WP 34713, 2026) provide complementary evidence that economic structure can regularize flexible ML systems and improve generalization, particularly under unstable conditions.

## Implication for the project

Feature importance should not be used as a post-hoc explanation of a selected model. If feature pruning is tested, the pruning rule must be learned inside the training/validation layer and frozen before the outer OOS period.

## Proposed controlled comparison

1. Full pre-specified feature set.
2. Economically grouped feature set with pre-declared redundant groups removed.
3. Validation-only feature pruning using a fixed rule.
4. Matched-budget random feature pruning placebo.

All arms use identical timestamps, target definition, walk-forward folds, portfolio construction and execution model.

## Required controls

- Point-in-time feature availability and source timestamps.
- Purged/embargoed folds where labels overlap.
- No feature pruning using outer-test observations.
- Complete trial accounting for every pruning rule tried.
- Commission, spread, slippage, market impact, borrow and capacity where applicable.
- 1x, 1.5x and 2x cost stress.
- Execution-lag stress.
- Regime and tail-period slices.
- Final untouched OOS evaluation.
- Selection-aware inference and comparison with the strong non-ML baseline.

## Decision rule

Feature pruning is promoted only if it improves net final-OOS utility relative to the full-feature baseline while remaining stable across cost assumptions and materially outperforming the matched random-pruning placebo. A reduction in in-sample importance or validation error alone is not evidence of economic value.

## Current evidence status

No numerical result is claimed yet. The repository's corrected forward-label-overlap validation and immutable prediction-to-execution artifact remain prerequisites for trusting candidate-level OOS performance.
