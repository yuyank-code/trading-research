# H115 — Null-Environment Falsification Before Promotion

## Hypothesis
A candidate research pipeline that reports significant out-of-sample trading evidence should also remain statistically well-calibrated when run on synthetic or placebo data with no exploitable predictability.

## Motivation
Adaptive specification search can manufacture apparently significant backtests even when the data-generating process contains no predictive structure. A 2026 study, *Spurious Predictability in Financial Machine Learning*, proposes testing complete predictive workflows against synthetic zero-predictability reference classes and microstructure placebos, then measuring selection-induced inflation on disjoint walk-forward realizations. This is a useful complement to ordinary leakage checks because a workflow can be causally ordered yet still overfit through adaptive search.

## Falsifiable prediction
Under null data, the full research workflow should not produce a materially elevated rate of apparently successful promoted candidates after applying the project's multiplicity controls. If it does, the workflow is not adequately calibrated.

## Experimental design

1. Freeze the production pipeline, candidate family, feature-generation rules, validation geometry, cost model, promotion criteria, and search ledger.
2. Generate multiple synthetic reference classes with no predictable target component, preserving relevant dependence properties such as volatility clustering and cross-sectional/time-series structure where feasible.
3. Add microstructure placebo tests where the target is deliberately decoupled from tradable information.
4. Run the *entire* search process, not a reduced diagnostic subset.
5. Record every trial, including failures and discarded candidates.
6. Apply the same purging/embargo, OOS evaluation, cost model, DSR/PBO/SPA-style controls, and promotion gates used for real data.
7. Compare the null distribution of maximum and promoted net performance with the corresponding real-data distribution.

## Primary metrics
- fraction of null trials passing each gate;
- maximum null Sharpe / utility;
- false-promotion rate;
- selection inflation: best-search result minus independent OOS result;
- calibration of reported p-values / confidence measures;
- ranking stability under independent null seeds.

## Promotion rule
No candidate may be promoted solely because it passes real-data OOS tests. The research workflow must first pass the null-environment calibration audit.

## Status
Proposed; numerical test not yet executed. Immutable candidate-level OOS prediction/return artifacts and corrected forward-label-overlap validation remain prerequisites for production candidate evaluation.
