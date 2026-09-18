# H65 — Selective deployment / abstention gate

## Status
Proposed, not yet empirically validated.

## Motivation
Recent 2026 research argues that an ML trading system should be allowed to **not trade** when its forecast does not clear a pre-specified economic hurdle. A separate 2026 walk-forward study finds that the choice of walk-forward window can materially affect reported performance and recommends a final single-time out-of-sample evaluation.

## Hypothesis
A frozen predictive model combined with a leakage-safe abstention rule can improve **net** risk-adjusted performance versus always trading, primarily by removing low-edge trades that do not cover realistic execution costs.

## Pre-registered test
For each decision date, estimate expected edge only from information available by that date. Trade only when:

`expected_edge > estimated_round_trip_cost + safety_margin`

Evaluate safety margins of 0, 0.25x, 0.50x, 1.0x and 1.5x of estimated round-trip cost. Threshold selection occurs only inside the development/validation layer; the final OOS period is untouched.

Compare against:
1. always-trade baseline;
2. fixed signal threshold;
3. cost-aware abstention;
4. placebo/randomized abstention with matched trade counts.

## Required evaluation
- point-in-time feature and execution timestamps;
- purged/embargoed walk-forward validation;
- explicit spread, commission, slippage and latency assumptions;
- +25%, +50%, +100% adverse cost stress;
- turnover, trade count and capacity proxies;
- OOS Sharpe/Sortino, max drawdown and break-even cost;
- family-level Reality Check/SPA where multiple thresholds/models are searched;
- DSR/PBO and search-budget accounting;
- report every tested threshold, including failures.

## Falsification
Reject H65 if abstention does not improve net OOS performance after costs, or if the apparent gain disappears under modest adverse cost/slippage stress, placebo controls, or untouched confirmation.

## Promotion rule
No deployment recommendation from this hypothesis alone. Promotion requires passing all upstream causal/leakage gates and the project's multiplicity-aware statistical gates.
