# Run 17 — Validation harness merged and selection controls

Date: 2026-09-02

## Meaningful progress

The validation-harness repair in `bitcoin-ml-trading` PR #4 was merged after its head commit passed GitHub Actions (`tests`, run 40, conclusion: success). The repair:

- counts duplicate timestamps before deduplication and raises a validation error;
- wires cost stress directly to the authoritative `signal_backtest` scalar `fee_bps` / `slip_bps` interface;
- preserves the deterministic 0.5x, 1x, 1.5x, 2x, 3x cost grid.

Merged commit: `0c8e79c549def7937d9b367793d41238083527c3`.

This is an infrastructure repair only; it does not establish trading performance.

## Code audit result

The current production research engine uses `HORIZON_BARS=6` and trains each walk-forward fold through `start - horizon_bars`, so the six-bar forward label cannot directly cross the first OOS test boundary. Future return is retained for target construction/evaluation and is not used as an entry feature in the reference signal backtest.

## Statistical/research controls

The next evidence gate remains strict because selecting among many candidate configurations on the same OOS stream creates selection bias. Bailey et al.'s Probability of Backtest Overfitting recommends CSCV/PBO for this problem, while the Deflated Sharpe Ratio explicitly adjusts for multiple testing and non-normality.

The project should therefore maintain a complete trial registry and distinguish:

1. development OOS used for model/policy selection;
2. frozen predictions and frozen execution assumptions;
3. untouched final holdout used once for final evaluation.

## New hypotheses

- H35: the repaired validator rejects duplicated timestamps instead of silently normalizing them.
- H36: the deterministic cost grid produces monotonic/inspectable degradation where economically expected, without changing predictions.
- H37: a policy selected on development OOS retains positive risk-adjusted performance on the untouched holdout after costs.
- H38: cost-aware abstention improves net performance primarily by reducing turnover, not by exploiting future information.
- H39: the selected result remains credible after accounting for the full number of trials.

## Current conclusion

Validation infrastructure has materially improved and the repair is now on the default branch. No numerical trading edge is promoted until immutable OOS prediction/trade/equity artifacts exist and the final holdout is evaluated under the predeclared cost model and trial-accounting procedure.
