# H103 — Selective Deployment Gate Adds Net Value Beyond Always-Trade

## Status
Proposed — preregistered for testing; not a result.

## Motivation
Recent 2026 work on leakage-aware selective deployment reports that a model can improve net risk-adjusted performance by abstaining when its validation improvement over a transparent fallback is insufficient. Separate 2026 evidence shows that transaction costs can destroy naive high-frequency ML strategies, making the decision to trade—not only the forecast—economically important.

## Hypothesis
For a frozen candidate signal, a causal validation gate that either deploys the signal or falls back to a transparent benchmark will improve selection-adjusted net OOS utility versus the same signal traded continuously, without increasing false promotion on placebo data.

## Test
Compare: (1) always-trade candidate; (2) candidate with selective deployment gate calibrated only on rolling training/validation history; (3) transparent fallback benchmark.

Use identical point-in-time data, purging/embargo, execution model, commissions, spread, slippage, impact, borrow, capacity, seed budget and trial ledger.

## Primary endpoint
Incremental net OOS utility of (2) versus (1), with confidence intervals and multiplicity adjustment. Secondary endpoints: turnover, drawdown, cost break-even, trade frequency and regime stability.

## Falsification
Reject H103 if the gate does not improve net OOS utility, only improves gross performance, requires materially more search than preregistered, or shows comparable improvement on timestamp-preserving placebo signals.

## Promotion rule
No promotion from this hypothesis alone. The result must also pass the repository-wide leakage, label-overlap, OOS, cost, placebo, search-budget and power gates.
