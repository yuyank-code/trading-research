# Research Pass 17 — Event Alignment, Embargo, and CPCV

Date: 2026-09-02

## Evidence audited

The authoritative `bitcoin-ml-trading/production_research.py` now purges six bars before each walk-forward test fold. This removes the direct forward-label overlap that existed in the earlier implementation.

However, the current target is still defined as `Close[t+6] / Close[t] - 1`, while the execution simulator enters at `Open[t+1]` and exits at the later row. The research event and monetized event are therefore not identical. This is a validation-design issue, not proof of look-ahead, but it makes economic interpretation of prior model results ambiguous.

## New literature

A 2024 Knowledge-Based Systems study comparing financial OOS methods in controlled experiments reports that Combinatorial Purged Cross-Validation (CPCV) reduced backtest-overfitting risk relative to conventional walk-forward evaluation, with stronger DSR/PBO diagnostics.

Current 2026 implementations of purged-CV tooling also emphasize that purging and embargo solve different problems: purging removes training observations whose label intervals overlap test intervals; embargo adds a post-test buffer for serial dependence/information persistence.

Recent BTC/USDT ML research continues to show that apparently profitable high-turnover forecasts can collapse once proportional transaction costs are applied, while confidence/forecast-magnitude filters can reduce turnover. This is supporting evidence for a cost-aware abstention hypothesis, not proof of an edge in this project.

## Testable hypotheses

H17.1 — Event-aligned labels improve economic validity: labels generated from the exact executable entry/exit event produce different and more interpretable OOS rankings than the current close-to-close proxy.

H17.2 — Explicit embargo reduces optimistic validation: adding an embargo after each test interval does not materially change a genuinely robust strategy, but should reduce performance for strategies relying on serially persistent information.

H17.3 — Cost-aware abstention survives costs: restricting trades to signals whose expected gross payoff exceeds a predeclared conservative execution-cost hurdle improves net expectancy and reduces turnover without requiring a threshold selected on the final holdout.

H17.4 — CPCV path dispersion is informative: a robust candidate should remain acceptable across a distribution of purged/embargoed paths rather than depending on one chronological walk-forward path.

## Required experiment order

1. Define signal, executable entry, and executable exit timestamps explicitly.
2. Generate labels from the same executable event used by the simulator.
3. Purge using event end-times rather than only a fixed row count.
4. Add configurable post-test embargo and regression tests for fold boundaries.
5. Generate immutable OOS predictions before changing execution policy.
6. Apply a predeclared fee/spread/slippage/impact grid.
7. Use CPCV/CSCV or an equivalent multiple-path procedure for development-stage selection.
8. Freeze the complete policy and evaluate once on an untouched final holdout.
9. Record the full trial history for DSR/PBO adjustment.

## Current conclusion

No new profitability claim is justified in this pass. The strongest progress is narrowing the research question from model discovery to event-correct, cost-aware, selection-resistant validation. The absence of checked-in generated OOS artifacts remains a reproducibility blocker for numerical claims.
