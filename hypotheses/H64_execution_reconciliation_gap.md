# H64 — Backtest-to-Execution Reconciliation Gap

## Status
Proposed hard gate — no empirical promotion yet.

## Motivation
Recent FX research documents material divergence between backtests and simulated live execution when the execution assumptions are not reconciled against the actual feed, timestamps, fills, spread, and order semantics. This is consistent with the project's existing requirement that execution be causal and cost-aware.

## Hypothesis
For any candidate FX strategy, the difference between backtest-simulated execution and a timestamp-aligned paper/live execution replay can be bounded by a pre-registered tolerance. If the reconciliation gap is persistently larger than the tolerance, the backtest is not considered deployment-valid regardless of its OOS Sharpe.

## Pre-registered protocol

1. Freeze the strategy, parameters, feature code, signal timestamps, and execution policy before reconciliation.
2. Record, for every order:
   - signal/decision timestamp;
   - order submission timestamp;
   - market-data timestamp used for execution;
   - intended price;
   - simulated fill price;
   - observed paper/live fill price;
   - spread estimate;
   - slippage;
   - quantity and position state.
3. Reconstruct the backtest using only information available at each decision timestamp.
4. Replay the identical signals against the execution record without changing strategy parameters.
5. Compute the reconciliation gap for:
   - fill price in basis points;
   - round-trip trading cost;
   - turnover;
   - trade count;
   - net PnL;
   - maximum drawdown.
6. Report median, 90th/95th percentile and worst-case execution deviation.
7. Repeat under adverse execution stress of +25%, +50%, and +100% versus the baseline cost model.
8. Do not tune the strategy to the reconciliation sample. Any execution-model adjustment must be frozen before the final untouched confirmation period.

## Promotion criteria
A strategy fails this gate if:

- execution inputs violate `available_time <= decision_time`;
- observed execution systematically differs from the simulator beyond the pre-registered tolerance;
- the reconciliation gap changes the sign of net profitability under realistic costs;
- the strategy requires post-hoc execution assumptions to remain profitable; or
- the reconciliation period is too short to establish a meaningful execution sample.

A pass does **not** establish profitability. It establishes only that the backtest execution model is sufficiently consistent with observed execution to justify further statistical evaluation.

## Required outputs

- `results/h64_execution_reconciliation.csv`
- `results/h64_execution_reconciliation_summary.json`
- immutable signal/order ledger;
- cost-model version identifier;
- data-feed/version identifier;
- exact strategy commit SHA;
- reconciliation period and exclusion rules.

## Why this matters
Statistical controls such as DSR, PBO, Reality Check and SPA cannot repair a causal execution error. Execution reconciliation therefore sits upstream of statistical strategy promotion.

## Evidence

- Rounce (2026), *What Survived Live Reconciliation: Auditing a Systematic FX Strategy* — documents material divergence between an earlier backtest and three months of simulated live paper trading and describes the resulting methodological rebuild.
- Chaboud et al., *Rise of the Machines: Algorithmic Trading in the Foreign Exchange Market* — provides evidence that FX market efficiency and high-frequency trading conditions matter for execution-aware research.
- Gencay et al., *Real-Time Trading Models and the Statistical Properties of Foreign Exchange Rates* — evaluates real-time FX trading models out of sample with transaction costs explicitly incorporated.

## Decision
Do not promote any candidate solely from historical backtest results. Require H64 reconciliation before deployment-oriented claims.
