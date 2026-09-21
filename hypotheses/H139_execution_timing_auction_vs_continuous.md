# H139 — Execution Timing vs Continuous-Market Execution

Status: proposed, untested
Date: 2026-09-21

## Claim

For frozen predictions and identical portfolio targets, a pre-specified auction/timing-aware execution rule can improve net OOS utility relative to a default continuous-market execution model without changing the underlying alpha signal.

## Null hypothesis

Execution timing provides no incremental economic value after realistic costs, liquidity constraints, participation limits, and execution uncertainty.

## Experiment arms

- A: frozen signal + default continuous execution
- B: frozen signal + pre-specified auction/timing execution
- C: frozen signal + matched-turnover randomized timing placebo
- D: frozen signal + liquidity-constrained continuous baseline

## Primary metric

Incremental net OOS utility of B relative to A, evaluated on the untouched outer OOS period.

## Secondary metrics

- annualized net Sharpe
- annualized turnover
- implementation shortfall
- realized spread/slippage
- estimated market impact
- breakeven transaction cost
- maximum drawdown
- regime/tail stability
- capacity by participation bucket

## Falsification

Reject H139 if the execution-aware improvement disappears under realistic impact costs, 1.5x/2x cost stress, execution-lag perturbations, liquidity restrictions, or matched-turnover placebo controls.

## Anti-overfitting rule

Timing windows, auction eligibility, participation limits, and all execution parameters must be registered before outer OOS evaluation. Any parameter search counts toward the project's research/search budget.

## Data requirements

Exact information timestamps, order timestamps, venue/session state, point-in-time liquidity measures, fills or defensible fill simulation, and realized execution costs are required. Date-keyed proxies are insufficient where the decision depends on intraday availability.

## Dependency

This hypothesis cannot promote an alpha model until the repository's forward-label-overlap issue is corrected and the immutable prediction -> position -> execution -> net-P&L ledger is available.
