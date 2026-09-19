# H96 — Feature-Transform Causality Invariance

## Date
2026-09-20

## Question
Can the research pipeline prove that every fitted feature transformation is causal, and that candidate performance is invariant to replacing global/contaminated transforms with train-window-only transforms?

## Motivation
Recent 2026 controlled leakage research reports that forward contamination in rolling feature normalization can inflate annualized Sharpe dramatically while preserving the appearance of out-of-sample testing. Separately, recent LLM-driven strategy research reports that a deliberately leaky oracle can survive Deflated Sharpe Ratio and Probability of Backtest Overfitting corrections. These results imply that statistical correction cannot substitute for structural information-availability controls.

## Falsifiable hypothesis
A clean, causally fitted feature pipeline will produce materially similar OOS conclusions when independently reconstructed from train-window-only transforms, while deliberately contaminated transforms will be detected by structural audits and fail promotion regardless of their performance.

## Required test
1. Construct a canonical train-only transform path for scaling, ranking, imputation, feature selection, dimensionality reduction and target encoding.
2. Construct matched adversarial fixtures with future observations allowed into each transform, one contamination mechanism at a time.
3. Run both paths through identical purged/embargoed walk-forward evaluation.
4. Compare feature artifacts, timestamps, fitted-state hashes and predictions—not just P&L.
5. Require the contaminated fixture to fail before performance metrics are interpreted.
6. Require the clean path to reproduce identical results under deterministic reruns.
7. Store an immutable candidate-level OOS prediction/return matrix for every accepted experiment.

## Acceptance criteria
- Zero future timestamps in any fitted-state artifact.
- Every fitted transform records its training interval.
- Contaminated fixtures are rejected automatically.
- Clean reruns are bitwise/reproducibly equivalent where the implementation permits.
- No model may be promoted based on a performance statistic from a fixture that has not passed the structural audit.

## Relationship to existing gates
H96 strengthens H88's adversarial leakage testing by targeting feature-state contamination specifically. It also precedes H94's multiplicity accounting and H95's incremental-value test: statistical gates are meaningful only after information availability has been established.

## Current status
Hypothesis recorded. No alpha claim is made; implementation and empirical validation remain required.

## Sources
- Bhand, K. (2026), *The Illusion of Alpha: Quantifying Hidden Data Leakage in Financial Machine Learning*, DOI:10.21203/rs.3.rs-9180656/v1.
- Gençay, E. (2026), *What survives honest evaluation? Leakage-safe, search-aware assessment of LLM-driven trading strategy discovery*, arXiv:2608.27734.
