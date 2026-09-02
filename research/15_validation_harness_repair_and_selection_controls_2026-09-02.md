# Run 15 — Validation harness repair and selection controls

Date: 2026-09-02

## Meaningful progress

A direct code audit of `bitcoin-ml-trading` found that the validation harness had two concrete defects: duplicate timestamps were counted only after deduplication, and `stress_costs()` passed a config object to an execution function whose API accepts scalar fee/slippage arguments.

A fix was prepared on `fix/validation-harness` and opened as PR #4. The patch:

- counts duplicate timestamps before deduplication and surfaces a validation error;
- calls the authoritative backtest with explicit `fee_bps=` and `slip_bps=` values;
- keeps the deterministic 0.5x, 1x, 1.5x, 2x, 3x cost grid.

No performance result is promoted from this repair.

## Literature update

Bailey & López de Prado (2014), *The Deflated Sharpe Ratio*, remains the primary selection-control reference: the observed Sharpe must be discounted for multiple testing and non-normality.

Bailey et al. (2017), *The Probability of Backtest Overfitting*, motivates combinatorial validation because selecting the best among many configurations can contaminate an otherwise chronological OOS stream.

A recent 2026 BTC-USDT study (Bysik & Ślepaczuk, arXiv:2606.00060) reports that naive hourly ML strategies can lose their apparent edge at 10 bps while forecast-magnitude cost filters can reduce turnover and recover profitability in selected configurations. Their model-family differences were not statistically established, so the execution-policy finding is treated as a hypothesis rather than proof.

## New hypotheses

- H35: the repaired validator detects duplicate timestamps rather than silently normalizing them away.
- H36: the cost-stress grid produces monotonic degradation as execution costs increase, absent pathological trade-selection effects.
- H37: the selected execution policy survives an untouched final holdout after all model/threshold trials are accounted for.
- H38: cost-aware abstention remains useful with predictions frozen.
- H39: any apparent edge survives DSR/PBO-style selection controls.

## Blocking status

The repository still lacks checked-in immutable OOS prediction/trade/equity artifacts and a complete trial registry. Therefore no new Sharpe, CAGR, or profitability claim is promoted in this run.

Next gate: merge the validator repair only after review/CI, then generate frozen OOS artifacts and run the predeclared cost grid without changing the model search space.
