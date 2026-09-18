# H56 — Stateful preprocessing leakage sentinel

## Status
Proposed research gate; no empirical result claimed.

## Hypothesis
A financial ML pipeline can appear to have strong OOS performance while leaking future information through stateful preprocessing (normalization, imputation, rolling transforms, resampling, feature selection, or label construction). An explicit leakage-injection sentinel should reliably detect the resulting performance inflation.

## Motivation
Recent controlled research reports that forward contamination in rolling feature normalization can materially inflate Sharpe ratios while preserving the appearance of rigorous validation. This makes preprocessing an auditable part of the temporal information boundary rather than a preprocessing detail.

## Test design
1. Define the information-available timestamp for every raw field and derived feature.
2. For each stateful transform, fit parameters separately inside each training fold only.
3. Apply frozen transform state to validation/OOS observations without refitting on them.
4. Build a deliberately leaked sentinel variant that uses future observations in at least one transform.
5. Verify the sentinel produces measurable performance inflation relative to the clean pipeline on controlled data.
6. Verify the audit fails the leaked pipeline and passes the clean pipeline.
7. Test rolling statistics, normalization, imputation, feature selection, resampling, and label construction independently.
8. Run the same audit on null data so a leakage detector cannot depend on real alpha.

## Primary metrics
- Clean-vs-leaked OOS Sharpe delta
- Clean-vs-leaked OOS return delta
- Leakage detector true-positive rate
- Leakage detector false-positive rate on clean pipelines
- Earliest timestamp at which future information becomes observable
- Number of affected rows/features

## Falsification
Reject H56 if the intentionally leaked pipeline does not trigger the audit, or if the clean pipeline is frequently flagged without a reproducible temporal violation.

## Promotion rule
No trading model may enter final confirmation until the complete feature/preprocessing graph passes the leakage sentinel with auditable timestamps and fold-local state.
