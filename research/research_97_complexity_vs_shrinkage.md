# Research 97 — Complexity vs Shrinkage: Does ML Add Predictive Value?

Date: 2026-09-22

## Question

When a disciplined portfolio already uses shrinkage/covariance regularization, does additional nonlinear ML predictive complexity improve *net* out-of-sample utility, or does the apparent gain come from better risk control?

## Literature signal

A January 2026 preprint on large-cap U.S. equities reports a deliberately leak-free, cost-aware benchmark in which an MLP only marginally exceeded a no-ML Black-Litterman prior out of sample, while incurring more than three times the cumulative transaction cost. A naive equal-weight portfolio was also close to the optimized ML results. This is a negative result against assuming that more predictive complexity automatically creates economically useful alpha.

A March 2026 large-scale futures benchmark finds some temporal-representation models can outperform linear baselines, but evaluates breakeven transaction costs, downside/tail risk, seed robustness, and computational efficiency rather than predictive accuracy alone. This creates a useful positive counterpoint: complexity may earn its place, but only when the economic improvement survives the full evaluation stack.

## Interpretation

The relevant comparison is not ML model A vs ML model B. It is:

1. strong shrinkage/risk baseline;
2. same portfolio construction plus nonlinear forecast;
3. same portfolio construction plus nonlinear forecast and cost-aware execution.

If ML improves Sharpe but not net utility, turnover-adjusted return, or breakeven costs, it has not demonstrated incremental economic value.

## Required controls

- exact point-in-time feature timestamps;
- purging/embargo for overlapping labels;
- untouched final OOS;
- fixed portfolio construction across model arms;
- commissions, spread, slippage, nonlinear impact, borrow and capacity;
- 1x/1.5x/2x cost stress;
- multiple random seeds for stochastic models;
- label-shuffled and synthetic-null workflow checks;
- complete trial ledger and selection budget.

## Promotion rule

Do not promote complexity unless the incremental net OOS utility is positive versus the shrinkage baseline and survives cost stress, seed dispersion, placebo tests, and multiple-testing adjustment. A lower drawdown alone is not sufficient if the same improvement is delivered by the baseline's risk controls.
