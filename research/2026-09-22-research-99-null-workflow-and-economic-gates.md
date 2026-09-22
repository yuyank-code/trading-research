# Research 99 — Null-workflow falsification and economic promotion gates

Date: 2026-09-22

## Evidence

Recent 2026 literature reinforces that prediction metrics are insufficient for trading promotion. Kim (2026) reports that permutation/AUC-style validation can produce false positives while CPCV/PBO and transaction-cost gates reject many apparently strong crypto strategies. A large 2026 ML asset-pricing study shows research-design choices materially change reported returns. Koijen & Levy (2026) emphasize real-time, point-in-time evaluation to avoid look-ahead bias. A 2026 large-scale futures benchmark evaluates risk-adjusted OOS performance together with downside/tail risk, breakeven costs, seed robustness and compute efficiency.

## Research implication

The project should promote a candidate only after it passes both statistical and economic gates, and the complete selection workflow should be run on null/reference data to estimate the false-discovery rate induced by adaptive research.

## Promotion gates

1. Point-in-time feature availability and timestamp audit.
2. Purged/embargoed validation appropriate to label horizon.
3. Untouched final OOS period.
4. Immutable prediction -> position -> execution -> cost -> net P&L ledger.
5. Explicit commissions, spread, slippage, market impact, borrow/capacity where relevant.
6. Cost stress at 1x, 1.5x and 2x and execution-lag stress.
7. Research-budget accounting across model, feature, horizon, threshold and execution searches.
8. PBO/DSR or equivalent multiplicity-aware inference.
9. Full-workflow null tests using shuffled labels and synthetic zero-predictability reference data.
10. Seed and regime robustness.

## Current status

No model is promoted. The repository's known forward-label-overlap issue remains a hard blocker for trusting older numerical results; corrected validation must precede any claim of robust alpha.
