# H152 — Execution-aware controller vs static execution

Date: 2026-09-22

## Hypothesis

For a fixed, point-in-time forecast and identical portfolio target, an execution-aware controller that trades off expected alpha decay, spread, impact, completion risk and opportunity cost will produce higher **net-of-cost OOS utility** than a static execution rule.

## Primary comparison

1. Static baseline: fixed participation / immediate execution rule.
2. Cost-threshold baseline: trade only when forecast edge exceeds estimated round-trip cost.
3. Execution-aware controller: dynamically adjust urgency using only information observable before each execution decision.
4. Matched-control: a controller with randomized urgency shocks calibrated to the same turnover distribution.

## Data and timing controls

- All features must have explicit availability timestamps.
- Execution observations after the decision timestamp cannot influence the decision.
- Forecast model and execution controller are trained/calibrated only inside the training/validation window.
- Final OOS remains untouched until the complete specification is frozen.
- Forward labels with overlapping horizons require purging and an embargo at least as long as the maximum label horizon.

## Economic tests

Report net return, Sharpe, Sortino, max drawdown, turnover, implementation shortfall, average spread paid, estimated impact, capacity and breakeven cost.

Stress without re-optimization:

- 1.0x baseline costs
- 1.5x costs
- 2.0x costs
- execution latency stress
- adverse-liquidity regime
- reduced ADV / capacity stress

## Overfitting controls

- Pre-register controller parameter ranges.
- Count all controller/model configurations tested.
- Use purged/embargoed walk-forward evaluation.
- Apply multiplicity-aware inference/PBO/DSR where applicable.
- Run the complete selection workflow on null and placebo data.
- Require improvement over both the static baseline and the matched-turnover randomized controller.

## Promotion criterion

Promote only if the execution-aware controller improves net OOS utility across multiple disjoint periods, survives cost/latency stress, does not depend on one liquidity regime, and passes the project's leakage and multiple-testing gates.

## Current status

Testable protocol only. No OOS performance claim is made until the forward-label-overlap validation correction is completed and the final OOS period is untouched.
