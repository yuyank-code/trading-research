# H158 — Point-in-Time Lineage vs Ordinary Historical Backtest

Date registered: 2026-09-22

## Hypothesis

A strict point-in-time feature/data lineage pipeline will produce materially different candidate rankings and/or weaker apparent performance than an ordinary historical-data pipeline for at least some ML trading candidates, because ordinary datasets can contain publication revisions, restated values, or derived information that was not available at the decision timestamp.

## Controlled comparison

A. Ordinary historical-data pipeline.

B. Point-in-time reconstructed pipeline with explicit availability timestamps.

Hold fixed:
- universe definition;
- labels and horizon;
- model class and hyperparameter search space;
- portfolio construction;
- execution delay;
- commission/spread/slippage/impact assumptions;
- train/test dates.

Change only information availability enforcement.

## Required validation

- Purge the full forward-label interval.
- Apply an embargo after each training window where labels overlap the validation/test interval.
- Audit every feature dependency against its decision-time availability timestamp.
- Freeze universe membership as-of each decision date.
- Run final OOS exactly once after model selection.

## Decision criteria

The PIT pipeline becomes the authoritative result. The ordinary pipeline is retained only as a diagnostic. A model cannot be promoted because it performs better under the ordinary pipeline.

If PIT performance is materially lower, classify the gap as a leakage/data-vintage finding and investigate the affected feature families before any model redesign.

If rankings remain stable and economic performance survives realistic costs, that is positive evidence of temporal robustness—not proof of alpha by itself.

## Overfitting controls

Count all variants searched across feature sets, horizons, models, seeds, execution rules and cost assumptions. Apply the project's search-budget-aware PBO/DSR framework. Include a null-data workflow using the identical selection procedure.
