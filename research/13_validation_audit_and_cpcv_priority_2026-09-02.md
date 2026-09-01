# Research 13 — Validation audit and CPCV priority (2026-09-02)

## Executive result

This pass found no defensible new trading-edge result. It found a reproducibility defect in the validation layer and a stronger methodological priority: once the fixed-horizon purge is verified, the next validation upgrade should be event-time purge + embargo and a selection-aware OOS design (CPCV/CSCV or nested OOS), not more model families.

## Implementation audit

The current `bitcoin-ml-trading/production_research.py` explicitly uses `HORIZON_BARS=6` and sets `train_end = start - horizon_bars` before each walk-forward fold. This fixes the previously identified direct six-bar label-overlap mechanism. The file also states that future returns are targets only and that the execution rule uses probability, stop/target geometry and estimated costs.

However, the validation layer has two concrete defects:

1. `validation.py::validate_predictions()` drops duplicate `Date` rows before calculating `duplicate_dates`. The resulting diagnostic is therefore always zero. This weakens a core data-integrity check.
2. `validation.py::stress_costs()` passes a `StressConfig` object to `backtest_fn(pred, cfg)`, while the authoritative `signal_backtest()` API accepts scalar `fee_bps` and `slip_bps` arguments. The advertised stress helper is therefore not currently compatible with the authoritative execution function.

These were recorded as GitHub issue #3. No cost-stress result produced through this helper should be promoted until the interface is corrected and tested.

## Literature update

Arian, Norouzi Mobarekeh & Seco (Knowledge-Based Systems, 2024) compare OOS validation procedures under synthetic financial environments and report CPCV as materially stronger than conventional walk-forward approaches on PBO/DSR diagnostics. This is useful evidence for prioritizing combinatorial validation when the project begins selecting among many candidate policies.

Aparicio & López de Prado (Algorithmic Finance, 2018) show that model-selection procedures themselves can be vulnerable to multiple testing. Bailey, Borwein, López de Prado & Zhu's PBO/CSCV framework formalizes the probability that the backtest winner is an overfit selection.

Bysik & Ślepaczuk (arXiv, May 19 2026) evaluate hourly BTC-USDT ML forecasting under transaction costs and find that naive sign trading can lose its edge at 10 bps, while a forecast-magnitude cost filter reduces turnover and restores profitability in selected configurations. They do not establish statistically significant dominance of one model family. This supports testing execution policy with frozen predictions rather than escalating model complexity.

## Testable hypotheses

- H35: the validation layer reports duplicate timestamps correctly and rejects duplicated prediction rows.
- H36: the cost-stress grid produces identical results whether invoked directly or through the validation wrapper.
- H37: event-time purge + explicit embargo does not materially improve raw predictive metrics but reduces false confidence in policy selection.
- H38: CPCV/CSCV produces a materially wider distribution of OOS outcomes than one walk-forward path; a strategy that survives only one favorable path should be rejected.
- H39: cost-aware abstention remains beneficial when predictions are frozen before execution-policy selection.
- H40: any candidate selected from the development set loses less performance on the untouched holdout than an unconstrained winner chosen from the entire OOS history.

## Next experiment gate

Do not add new predictors until these are complete:

1. Fix validation issue #3 and add regression tests.
2. Add explicit `prediction_time`, `label_start_time`, and `label_end_time` columns.
3. Implement event-time purge rather than relying only on a fixed row count.
4. Add an explicit embargo parameter and test it.
5. Produce immutable OOS prediction artifacts with code/data/config hashes.
6. Split OOS history into development and untouched final holdout.
7. Freeze model, feature set, threshold, execution rule, fees, slippage and sizing before final evaluation.
8. Run CPCV/CSCV or an equivalent search-adjusted analysis across the full trial registry.

## Current verdict

Validation quality improved because the direct fixed-horizon overlap is now removed from the authoritative production path. But the project is still not ready to claim a robust trading edge: the validation helper itself has defects, explicit event-time embargo is not yet enforced, and the generated OOS artifacts are not yet an immutable, independently reproducible evidence set.
