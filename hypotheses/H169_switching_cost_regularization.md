# H169 — Switching-Cost Regularization Improves Net Utility Without Predictive Leakage

## Hypothesis

For a frozen predictive model, a predeclared switching-cost/hysteresis execution rule can improve net out-of-sample economic utility by reducing low-value position changes, without requiring additional predictive information.

## Null

Switching-cost regularization does not improve paired outer-OOS net utility after accounting for reduced turnover and the extra policy-selection dimension.

## Protocol

- freeze the predictive model and its predictions before policy evaluation;
- preserve the full label-horizon purge/embargo;
- compare raw signal, fixed cost threshold, fixed hysteresis, nested threshold, and nested hysteresis;
- select any adaptive policy only on a calibration block inside each outer fold;
- freeze the selected policy before the outer test;
- keep the final holdout untouched until all choices are frozen;
- use identical execution timing and cost assumptions for every comparator.

## Cost model

Evaluate baseline costs plus 1.5x and 2x stress, with explicit spread/slippage assumptions and an additional execution-delay stress. Report gross return, commissions/fees, spread/slippage, turnover and net return separately.

## Primary metric

Paired outer-OOS incremental net utility versus the fixed baseline.

## Secondary metrics

Sharpe, maximum drawdown, turnover, trade count, average holding time, fold-level win rate, threshold/hysteresis stability and cost-break-even level.

## Anti-overfitting gates

- no outer-OOS policy selection;
- complete accounting of thresholds/hysteresis values tried;
- search-aware inference;
- seed aggregation for stochastic models;
- null falsification tests from H167;
- final untouched holdout;
- no promotion from gross performance alone.

## Falsification

H169 is rejected if the execution regularizer fails to improve paired net utility versus the fixed baseline, if gains disappear under 1.5x/2x cost stress, or if the apparent advantage is confined to a small number of folds or to the calibration/selection sample.

## Expected interpretation

A successful result would support the execution-layer hypothesis, not prove a new predictive signal. It would justify treating cost-aware execution as a separate, reusable module while keeping predictive model claims unchanged.
