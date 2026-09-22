# Research 118 — Switching-Cost Regularization as a Separate Execution Layer

## Date
2026-09-23

## Literature synthesis

Recent work published 22 September 2026 in *Computational Economics* argues that supervised trading models can implicitly regularize turnover by conditioning predictions on the previous model output, effectively introducing a switching-cost penalty without changing the predictive loss. The practical implication is that the signal-generation layer and the execution layer should not be assumed to have the same objective.

A March 2026 *Journal of Financial Data Science* paper similarly proposes a modular "smart trading rule": first generate a frictionless allocation, then execute only when expected benefit exceeds transaction cost. The reported evidence emphasizes lower turnover and better risk-adjusted results, but the result must be treated as literature evidence rather than as proof for this project.

A 2026 BTC walk-forward study provides a complementary empirical warning: naive sign-based ML strategies can become unprofitable at 10 bps per trade, while a predeclared forecast-magnitude/cost filter can materially reduce turnover. XGBoost was descriptively strongest in that study, but bootstrap evidence did not establish formal dominance over neural alternatives.

## Research implication

The project should not let a threshold sweep, hysteresis parameter, or execution rule become an uncounted model-selection dimension. Execution regularization can improve economics, but it can also become another source of backtest overfitting if tuned on the final OOS sample.

## Proposed controlled comparison

For a frozen predictive model and frozen PIT dataset compare:

1. frictionless/raw signal;
2. fixed cost-aware threshold;
3. nested-selected threshold;
4. fixed hysteresis/switching-cost rule;
5. nested-selected hysteresis rule.

All policies must use identical predictions, splits, execution timestamps, costs, and untouched final holdout.

## Required reporting

Report paired net utility versus the frozen baseline, turnover, trade count, maximum drawdown, cost decomposition, performance at 1x/1.5x/2x costs, execution-delay stress, fold-level win rate, and selection-adjusted inference.

## Interpretation rule

A lower-turnover policy is not automatically better. It earns promotion only if the reduction in trading friction produces a positive incremental outer-OOS economic result that survives cost stress and remains stable across folds.

## References

- Witkowski, T. (2026), *Implicit Switching-Cost Regularization in Supervised Trading Signal Classification*, Computational Economics, published 2026-09-22.
- Li, S., Mulvey, J. M., & Fabozzi, F. J. (2026), *Smart Trading Rule: A Modular Machine Learning Framework for Portfolio Optimization with Transaction Costs*, Journal of Financial Data Science 8(2), 145–175, DOI 10.3905/jfds.2026.1.217.
- Bysik, A. & Ślepaczuk, R. (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*, arXiv:2606.00060.
