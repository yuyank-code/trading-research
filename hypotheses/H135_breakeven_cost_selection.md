# H135 — Breakeven-Cost Selection vs Sharpe Selection

## Hypothesis
Selecting a candidate using its estimated breakeven transaction-cost buffer will produce more robust net out-of-sample performance than selecting candidates by gross Sharpe alone.

## Test
Construct a fixed-budget candidate set using identical data, timestamps, features, and training procedure. Inside each research/training layer, select candidates using one of the pre-declared rules:

A. highest gross Sharpe;
B. highest base-cost net Sharpe;
C. highest breakeven transaction-cost buffer;
D. pre-specified robustness composite.

The final OOS set is frozen before any final-period inspection.

## Primary endpoint
Incremental net OOS utility over the strongest non-ML baseline, measured after the full execution-cost model.

## Secondary endpoints
- breakeven cost;
- OOS Sharpe and Sortino;
- fold-to-fold dispersion;
- maximum drawdown and tail loss;
- turnover and capacity proxy;
- stability under 1x/1.5x/2x costs;
- execution-lag sensitivity.

## Falsification
Reject H135 if breakeven-cost selection fails to outperform gross-Sharpe selection on the primary OOS endpoint, or if its apparent advantage disappears under pre-specified cost/lags/regime stresses.

## Leakage/overfitting controls
All preprocessing, feature selection, hyperparameters, thresholds and candidate selection must occur inside the appropriate training/validation layer. Forward-label overlap must be purged and embargoed. The final OOS period is immutable. The full search/trial ledger must be retained so selection effects can be audited.

## Status
Not yet numerically tested because the repository still requires the corrected immutable prediction-to-execution OOS artifact before historical performance claims can be trusted.
