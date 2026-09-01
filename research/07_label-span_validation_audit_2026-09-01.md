# Research Update 07 — Label-Span Audit and Validation Gate

Date: 2026-09-01

## Status

This pass produced a validation finding and a pipeline gate, but no economic performance claim. The repository currently contains the research record and validation requirements, but the default branch does not expose the executable dataset/backtest implementation needed to independently reproduce the promised frozen-OOS execution-policy experiment from this repository alone. Therefore no new Sharpe, return, or profitability number is reported.

## Literature update

Recent technical reproductions and implementations reinforce a precise point: purging must be defined from the actual information interval of each label, while embargo is a separate control for residual serial dependence. A fixed row-count gap is only valid when sampling frequency and event horizon are fixed and equivalent. Event-time/evaluation-time pairs are the safer abstraction.

Sources reviewed:
- López de Prado, *Advances in Financial Machine Learning* (2018), chapters on cross-validation and backtest overfitting.
- Recent purged-CV implementations and empirical reproductions emphasizing explicit prediction/evaluation timestamps and label intervals.

## Pipeline audit result

The research record correctly identifies the earlier forward-label overlap problem. The current repository state does not contain enough executable artifacts/data to verify that the corrected implementation is actually producing the intended OOS predictions. This is now a hard reproducibility gate.

A model cannot be promoted until the following artifacts are present and independently runnable:

1. Point-in-time input data manifest with source, retrieval time, and timezone.
2. Feature-generation code with lookback windows documented.
3. Per-row `prediction_time` and `label_end_time` (or event end time).
4. A split function that purges by interval overlap, not only by row count.
5. Explicit embargo duration and rationale.
6. Frozen OOS prediction file with model/version identifier and hash.
7. Execution-policy simulator with fees, spread/slippage, and turnover accounting.
8. Trial registry containing every tested model/policy/threshold and failed trial.
9. Deterministic environment/dependency specification.
10. Final untouched OOS designation that cannot be used for tuning.

## Testable hypotheses added

### H21 — Event-time purge equivalence

For fixed-horizon labels, an event-time interval purge must produce the same or stricter train/test separation as the existing horizon-based cutoff. Any disagreement must be explained before results are accepted.

### H22 — Execution robustness across cost assumptions

A policy should retain positive net expectancy across a predeclared conservative cost/slippage grid. A single favorable cost assumption is insufficient.

### H23 — Fold consistency

Economic value should not depend on one walk-forward fold. Report the distribution of fold-level net Sharpe/return and the fraction of profitable folds.

### H24 — Prediction-policy separation

With predictions frozen, execution-policy improvements must survive without retraining. If performance changes only when the predictive model is reselected, the evidence is attributed to model-selection effects rather than execution policy.

## Locked acceptance protocol

1. Generate predictions strictly OOS using event-time purging.
2. Freeze predictions and hash the artifact.
3. Apply only the predeclared execution policies from Update 06.
4. Evaluate a predeclared cost/slippage grid.
5. Produce fold-level and pooled metrics.
6. Keep final OOS untouched until all policy decisions are frozen.
7. Run search-aware diagnostics after the complete trial registry is assembled.
8. Reject any result that cannot be reproduced from the recorded data/code/version manifest.

## Failure / limitation

No new backtest number is reported in this pass. Claiming one without an independently reproducible executable pipeline would violate the project's own research standard and risk turning a methodological improvement into unsupported performance evidence.

## Current conclusion

The project has a stronger validation specification, but the next bottleneck is reproducibility rather than another model family. The highest-value engineering task is to expose and run the corrected data → label-span → purged OOS prediction → frozen execution pipeline, then measure the execution-policy hypotheses under realistic costs.
