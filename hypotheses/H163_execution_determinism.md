# H163 — Execution-Determinism / Implementation-Risk Test

**Status:** Registered — not yet run
**Registered:** 2026-09-22

## Hypothesis

If a trading strategy is economically robust, two independent implementations of the same frozen signal, portfolio construction, and execution specification should produce materially consistent net OOS conclusions.

## Null

Implementation details can materially change reported net performance or candidate-vs-baseline ranking.

## Experimental controls

- identical frozen PIT-safe input artifact
- identical decision timestamps
- identical universe snapshot
- identical portfolio weights
- identical execution delay
- identical cost schedule
- no post-OOS parameter changes

## Required tests

1. Zero-cost numerical equivalence.
2. Base-cost equivalence.
3. 1.5x and 2x cost stress.
4. Spread/slippage stress.
5. Candidate-minus-baseline paired difference.
6. Turnover-matched placebo.

## Promotion gate

Implementation differences must remain inside the pre-registered uncertainty interval and cannot change the sign of the incremental net OOS result. Otherwise the candidate remains BLOCKED until the discrepancy is explained.

## Motivation

Recent research on implementation risk in portfolio backtesting finds that transaction-cost implementation can create structured divergence between otherwise equivalent backtest engines. This makes execution semantics a first-class research variable.
