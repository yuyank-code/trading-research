# H85 — Metric-Invariance and Decision-Utility Robustness

## Status
Pre-registered hypothesis; not yet empirically tested because the immutable candidate-level OOS prediction/return matrix is still unavailable.

## Motivation
A model can appear strong because the researcher implicitly selects the performance metric after seeing results. Sharpe, Sortino, drawdown, turnover, break-even cost, tail loss, and benchmark-relative value can rank the same candidate family differently. Recent large-scale financial-ML benchmarking therefore evaluates several risk-adjusted and economic dimensions rather than relying on a single score.

## Hypothesis
A genuinely useful trading candidate should retain its deployment ranking, or remain inside the same small Model Confidence Set, across a pre-registered family of economically meaningful objectives. If the preferred model changes materially depending on the chosen metric, the result is research-design sensitive and should not be promoted without an explicit utility rationale fixed before confirmation.

## Test
Using the frozen candidate-level OOS return matrix, compute for every candidate:

- net Sharpe and annualized return;
- Sortino ratio;
- maximum drawdown and expected shortfall/tail loss;
- turnover and implementation-cost burden;
- break-even transaction cost;
- benchmark-relative net return;
- capacity/impact stress performance.

Rank candidates using each metric separately and measure rank correlations, top-k overlap, and Model Confidence Set membership. No metric may be chosen after observing confirmation results.

## Statistical controls
- Purged/embargoed chronological OOS evaluation.
- Locked confirmation set.
- DSR/PBO for selection effects.
- SPA / White Reality Check for benchmark-relative superiority.
- Model Confidence Set for statistically indistinguishable candidates.
- Matched-count placebo candidates and synthetic zero-alpha controls.
- Cost-model and holding-period stress from H78/H84.

## Falsification
The hypothesis is weakened if the apparent winner changes sharply across reasonable metrics, if no candidate remains in the MCS across objectives, or if the same metric-sensitive ranking occurs for zero-alpha controls.

## Promotion rule
No candidate is promoted solely because it maximizes one metric. Promotion requires a pre-specified economic utility function or demonstrated metric-invariance plus survival of all existing leakage, cost, capacity, and multiple-testing gates.
