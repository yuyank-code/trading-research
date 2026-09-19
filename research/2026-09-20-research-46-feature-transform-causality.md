# Research 46 — Feature-Transform Causality and Structural Leakage

## Date
2026-09-20

## Research question
How can the pipeline demonstrate that feature transformations are information-available at the decision timestamp, rather than merely relying on statistical tests that can be fooled by leakage?

## New literature evidence

### Bhand (2026) — hidden feature leakage
A controlled study reports that a 16-day forward contamination in rolling feature normalization can increase annualized Sharpe from roughly 0.15–0.57 in clean estimation to roughly 1.15–2.84 under leaked estimation across tested classifiers. The exact magnitudes are study-specific, but the methodological result is the important part: leakage in a transformation layer can create a large apparent edge without changing the outward form of an OOS experiment.

### Gençay (2026) — structural leakage can survive statistical correction
A recent leakage-safe, search-aware strategy-discovery study reports a deliberately leaky oracle with Sharpe 35 that still survives DSR and PBO testing. Its implication is stronger than a generic warning: statistical overfitting controls cannot certify a strategy whose information set is structurally invalid.

### Saly-Kaufmann et al. (2026) — economic evaluation remains necessary
A large financial time-series benchmark evaluates OOS risk-adjusted performance together with transaction-cost break-even, tail risk and seed robustness. This supports keeping structural leakage checks ahead of economic scoring while retaining cost-aware evaluation after the structural gates pass.

### Arian et al. (2024) — CPCV is useful but not sufficient
Controlled synthetic experiments report CPCV as superior to conventional OOS methods for reducing backtest-overfitting risk. CPCV therefore remains a downstream statistical gate, not a substitute for causal feature construction.

## Pipeline change
The project should add a dedicated feature-state audit with the following invariant:

**Every fitted transformation must have a recorded training interval ending no later than the prediction timestamp.**

The audit should cover scaling, rolling normalization, imputation, ranking, feature selection, dimensionality reduction, target encoding and any learned preprocessing state.

For each artifact, persist:
- decision timestamp;
- earliest/latest observation used to fit the transform;
- transform configuration hash;
- fitted-state hash;
- source-data snapshot/hash;
- candidate/trial identifier.

Adversarial fixtures should deliberately inject future observations into each transform. The pipeline must reject these fixtures before calculating or interpreting trading performance.

## Testable outcome
The clean train-only pipeline should be reproducible and economically evaluated normally. The contaminated variants should fail structural validation even if their backtest Sharpe improves.

This creates a strict ordering:

**information availability → label-overlap safety → OOS validation → execution costs → multiplicity correction → economic comparison.**

## Current finding
This run produced a meaningful methodological result, not a trading result: the strongest recent evidence reinforces that leakage detection must be a first-class structural gate. No candidate model is promoted and no new alpha claim is made.

## Sources
- Bhand, K. (2026), *The Illusion of Alpha: Quantifying Hidden Data Leakage in Financial Machine Learning*, DOI:10.21203/rs.3.rs-9180656/v1.
- Gençay, E. (2026), *What survives honest evaluation? Leakage-safe, search-aware assessment of LLM-driven trading strategy discovery*, arXiv:2608.27734.
- Saly-Kaufmann, A., Wood, K., Calliess, J. P. & Zohren, S. (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*, arXiv:2603.01820.
- Arian, H., Norouzi Mobarekeh, D. & Seco, L. (2024), *Backtest overfitting in the machine learning era: A comparison of out-of-sample testing methods in a synthetic controlled environment*, Knowledge-Based Systems 305, 112477. DOI:10.1016/j.knosys.2024.112477.
