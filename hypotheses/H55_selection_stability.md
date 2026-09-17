# H55 — Selection stability under correlated search

## Status
Proposed research gate; no empirical result claimed.

## Hypothesis
If an apparent trading edge is genuine rather than a product of correlated specification search, the selected candidate should remain competitive across disjoint OOS paths and under modest perturbations of the candidate family, cost assumptions, and random seeds.

## Motivation
Recent quantitative research emphasizes that adaptive specification search can manufacture significant walk-forward results even under zero-predictability nulls. Separately, large ML-trading benchmarks emphasize OOS risk-adjusted returns, tail risk, break-even transaction costs, and seed robustness rather than prediction metrics alone.

## Test design
1. Freeze the complete candidate family before scoring.
2. Generate purged/embargoed OOS paths with label-horizon-aware exclusion.
3. Preserve every candidate/configuration in the trial registry.
4. Rank candidates on development OOS data only; never use the final confirmation window for selection.
5. Re-run selection over disjoint path subsets and report rank stability, not only the winning Sharpe.
6. Repeat with cost stress at baseline, +25%, +50%, and +100% and with adverse slippage assumptions.
7. Repeat model training under multiple fixed random seeds where applicable.
8. Calculate DSR and PBO/CSCV using the full effective trial count.
9. Compare the real-data selection stability distribution with the same workflow applied to zero-predictability null data.

## Primary metrics
- Net OOS Sharpe and geometric return
- Maximum drawdown and tail loss
- Turnover and trades per unit time
- Break-even transaction cost
- Candidate rank correlation across OOS paths
- Selection frequency of the eventual winner
- DSR and PBO
- Null-workflow false-selection rate

## Falsification
Reject H55 if the apparent winner is unstable across disjoint OOS paths, loses its advantage under modest cost/slippage stress, or is not distinguishable from the null-workflow selection distribution after multiplicity adjustment.

## Promotion rule
No candidate is promoted from H55 alone. A candidate must also pass leakage audits, executable-horizon alignment, realistic execution costs, workflow-level null falsification, and an untouched confirmation period.
