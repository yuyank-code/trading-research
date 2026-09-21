# H128 — Nested Walk-Forward Window Selection

## Hypothesis

Selecting training/testing window lengths from historical performance can itself overfit. A model whose walk-forward window is chosen inside the same outer evaluation period should not be credited with the benefit of that selection unless the window choice is made strictly inside an inner training/validation layer.

## Motivation

Recent 2026 evidence shows that reported trading performance can be highly sensitive to walk-forward window length. Optimizing that choice across many windows therefore creates another research degree of freedom. The correct test is nested walk-forward selection: inner windows may be searched using only information available before the outer test block; the outer test block remains untouched until evaluation.

## Controlled comparison

A. Fixed pre-declared walk-forward window.

B. Single-layer adaptive window selection using prior OOS results.

C. Nested walk-forward window selection: inner training/validation chooses the window, outer test measures performance.

D. Matched-noise/placebo selection using the same search budget.

## Required controls

- Point-in-time features and labels.
- Purging and embargo whenever label horizons overlap.
- No use of outer-test returns for window selection.
- Immutable outer-test predictions before execution-cost accounting.
- Identical universe, features, model class, portfolio construction and execution across A-D.
- Realistic commission, spread, slippage and market-impact assumptions.
- 1.0x, 1.5x and 2.0x cost stress.
- Execution-lag perturbation.
- Multiple-testing accounting for the number of windows searched.
- Null/placebo search with the same number of candidate windows.

## Primary metric

Incremental net OOS utility of adaptive selection versus the fixed-window baseline, measured only on the outer test periods.

## Secondary diagnostics

- Outer-fold Sharpe and return distribution.
- Worst-fold and median-fold utility.
- Turnover and cost share.
- Break-even transaction cost.
- Window-selection stability.
- Rank stability across outer folds.
- Difference between single-layer and nested estimates.
- Selection inflation: inner-selected score minus outer realized score.

## Falsification

Reject the hypothesis that adaptive window selection adds value if its outer-test improvement disappears under nested evaluation, matched-noise selection, cost stress, or multiple-testing correction.

## Promotion rule

No candidate can be promoted because an adaptive walk-forward window produced a favorable backtest. The adaptive procedure must demonstrate incremental net OOS value in the untouched outer test and survive the same leakage, cost and selection controls as every other candidate.
