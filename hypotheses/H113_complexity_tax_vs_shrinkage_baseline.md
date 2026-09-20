# H113 — Complexity Tax vs Shrinkage Baseline

## Status
Proposed; not yet numerically evaluated.

## Motivation
Recent 2026 evidence shows that apparently strong ML portfolio results can be driven primarily by covariance regularization, Bayesian shrinkage, and portfolio construction rather than incremental predictive content. A January 2026 leak-free, cost-aware US-equity benchmark reported that its promoted MLP only marginally exceeded a no-ML Black-Litterman prior while generating more than three times the cumulative transaction cost. This motivates testing whether model complexity adds economically useful information after the same portfolio/risk machinery is applied.

## Hypothesis
After identical point-in-time preprocessing, portfolio construction, risk controls, and realistic execution costs, a complex predictive model must deliver statistically and economically significant incremental net OOS utility over a transparent shrinkage/prior-only baseline. If it does not, the model is not promoted regardless of raw predictive metrics.

## Primary comparison
1. Prior-only / shrinkage baseline using only information available at decision time.
2. Regularized linear predictive model.
3. Candidate nonlinear model(s).

All share the same universe, covariance estimator, optimizer, constraints, rebalance schedule, execution lag, cost model, and capacity assumptions.

## Primary endpoints
- Incremental net OOS return versus prior-only baseline.
- Difference in risk-adjusted utility.
- Turnover and cumulative execution cost.
- Break-even cost.
- Benchmark-relative alpha with multiplicity adjustment.

## Leakage controls
- Point-in-time data only.
- Training-only fitting for scalers, covariance, feature transforms, and hyperparameters.
- Purge/embargo for overlapping labels.
- Immutable candidate-level OOS prediction/position/return records.
- Complete trial ledger, including discarded configurations.

## Robustness
Run the frozen candidate set across predefined cost stress levels, walk-forward/CPCV validation geometries, and seed repetitions where stochastic training is used. No post-hoc baseline substitution is permitted.

## Promotion rule
No promotion unless the candidate beats the prior-only baseline on the preregistered primary utility measure, survives realistic base costs and at least the predefined stress grid, and remains significant after accounting for the complete search budget.

## Failure criteria
- No incremental alpha.
- Incremental alpha disappears after costs.
- Higher return is explained by higher turnover/risk.
- Ranking reverses materially under reasonable validation or cost perturbations.
- Candidate fails placebo or leakage-control tests.
