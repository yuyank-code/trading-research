# H154 — Incremental ML Alpha vs Strong Baselines

Date: 2026-09-22

## Hypothesis

After controlling for universe, covariance/risk model, portfolio construction, turnover, leverage, and execution costs, a nonlinear ML forecast produces statistically and economically meaningful incremental OOS utility over a strong no-ML/shrinkage baseline.

## Null hypothesis

Any apparent ML improvement is explained by portfolio construction, risk regularization, turnover differences, or selection noise rather than incremental predictive information.

## Test

Use a frozen research budget and compare equal-weight, shrinkage/risk-only, linear, and nonlinear ML forecasts under identical portfolio and execution rules. Add a turnover-matched placebo so that lower trading activity cannot masquerade as predictive alpha.

## Required checks

- point-in-time data and feature timestamps;
- purging and embargo for overlapping forward labels;
- untouched final OOS;
- realistic commission, spread, slippage, impact, borrow and capacity assumptions;
- 1x/1.5x/2x cost stress and execution-lag stress;
- random-seed stability;
- PBO/DSR or comparable multiple-testing control;
- null/synthetic workflow;
- performance attribution to forecast versus portfolio/risk layer.

## Promotion rule

Promote only if incremental net OOS utility remains positive and practically material versus the strongest baseline after all controls, and the effect is absent or materially weaker in null/placebo workflows.

## Current status

Untested. Historical model results remain blocked by the repository's previously identified forward-label-overlap validation issue.
