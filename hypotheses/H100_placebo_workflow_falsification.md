# H100 — Placebo-Workflow Falsification

## Claim

A trading research workflow should not produce statistically significant OOS evidence when run against zero-predictability or microstructure-placebo data. If it does, the workflow is generating spurious predictability through leakage, adaptive search, implementation artifacts, or inference failure.

## Motivation

Recent 2026 research on spurious predictability argues that adaptive specification search can generate significant walk-forward backtests even under martingale-difference nulls, and proposes falsification audits using synthetic zero-predictability and microstructure-placebo reference classes. This complements, rather than replaces, DSR/PBO: multiplicity correction cannot repair an invalid information set or a systematically biased workflow.

## Test

Freeze the complete research pipeline and run it unchanged on:

1. **Zero-alpha synthetic returns** with matched dependence/volatility structure.
2. **Feature-shuffled placebos** preserving marginal distributions but destroying predictive alignment.
3. **Timestamp-preserving target permutations** that preserve label frequency and temporal structure while removing predictability.
4. **Real-market control data** where the candidate signal is constructed from information unavailable to the target by design.

The workflow must use the same search budget, feature transforms, purging/embargo, model fitting, execution simulator, costs, seed ledger, confirmation protocol and selection-aware inference as the real experiment.

## Primary outcome

Measure the false-discovery rate of the complete workflow: fraction of placebo searches that pass the same promotion gates used for real candidates.

Secondary outcomes: maximum placebo Sharpe, maximum placebo net return, DSR/PBO behavior, cost-break-even distribution, and sensitivity to search intensity.

## Falsification

H100 fails if the frozen workflow generates materially positive or statistically significant placebo evidence at a rate inconsistent with its nominal error control. Any failure blocks interpretation of real-market model results until the cause is isolated.

## Promotion rule

No candidate is promoted unless the complete workflow passes the placebo audit. Passing is a prerequisite, not evidence of alpha.
