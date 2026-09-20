# Research 59 — Cost Stress, Break-Even Alpha, and Economic Fragility

## Date
2026-09-20

## New evidence

Recent work reinforces that financial ML should be judged on economic output rather than forecast accuracy alone. Bysik & Ślepaczuk (2026) evaluate hourly BTC strategies with walk-forward forecasting and explicit transaction costs; their main result is that naive sign-based strategies fail at 10 bps while a cost-aware forecast-magnitude filter can materially reduce turnover. Importantly, the reported model ranking is descriptive rather than formal statistical dominance.

Huang, Wang & Jiang (2026) similarly report a disconnect between predictive improvements and net high-frequency trading performance once fees, spreads and slippage are modeled.

Kim (2026) provides a broader validation warning: AUC-only evaluation can have high false-positive rates, while combinatorial purged CV, PBO and multiple-testing controls can eliminate apparently impressive candidates.

## New research contribution

The project will add a **cost-stress surface** rather than reporting one assumed transaction-cost scenario. Every candidate is evaluated on the same immutable OOS return stream under a frozen cost grid. This produces a break-even-cost statistic and shows whether an apparent alpha is robust or depends on optimistic execution assumptions.

## Required artifact

`candidate_oos_predictions_returns.parquet` (or equivalent immutable candidate-level OOS matrix) is still required before numerical claims can be made. The matrix must contain timestamp, candidate_id, prediction, position/weight, realized return, turnover and all execution-cost components.

## Interpretation

A robust candidate should show a smooth and economically plausible degradation as costs increase. A sharp collapse at or below the reference cost is evidence of economic fragility. A placebo that survives the same stress curve is evidence of a pipeline failure rather than alpha.

## Decision

No candidate is promoted from this research pass. This is a pipeline and hypothesis improvement until the immutable OOS matrix exists.

## Sources

- Bysik, A. & Ślepaczuk, R. (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*, arXiv:2606.00060.
- Huang, W., Wang, Z. & Jiang, W. (2026), *Research on Machine Learning High-Frequency Trading Strategies Under Transaction Cost*, Journal of the European Academy Open University, 2(4).
- Kim, J. (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, SSRN 6508779.
- Li, S., Mulvey, J.M. & Fabozzi, F.J. (2026), *Smart Trading Rule: A Modular Machine Learning Framework for Portfolio Optimization with Transaction Costs*, Journal of Financial Data Science, 8(2), 145–175.
