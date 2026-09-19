# H87 — Seed and Training-Path Stability

Date: 2026-09-19

## Hypothesis

If a trading candidate represents a genuine, learnable relationship rather than optimizer noise, its economic conclusion should be reasonably stable across pre-registered random seeds and training-order perturbations that do not change the information set.

## Why this is testable

For stochastic ML models, initialization, minibatch order, augmentation/random sampling, and optimizer nondeterminism can create materially different fitted functions. A candidate that survives only one seed is exposed to an additional hidden research degree of freedom: the seed itself.

Recent large-scale financial time-series benchmarking explicitly reports robustness to random-seed selection as part of model evaluation. This project therefore treats seed robustness as a validation dimension rather than an implementation detail.

## Pre-registration

For each frozen candidate specification:

- use 10 fixed seeds: 7, 19, 31, 43, 59, 71, 83, 97, 109, 127;
- do not select the best seed using validation or confirmation performance;
- fit each seed independently within the same causal training folds;
- keep architecture, feature set, label, horizon, cost model, execution rule and hyperparameter budget identical;
- record every seed's OOS predictions and net returns;
- evaluate the median, interquartile range, worst seed, and fraction of seeds with positive net performance;
- compare seed dispersion with matched-count null/placebo models.

## Promotion rule

A candidate is not promoted on the basis of the best seed. The primary result is the pre-registered seed-aggregate, with the worst-seed result reported separately. Large seed dispersion is a robustness warning even if the aggregate is positive.

## Leakage controls

Seed runs must share no fitted state across folds. Feature normalization, imputation, calibration, thresholding, and hyperparameter selection remain fold-local. Confirmation is scored after the seed protocol is frozen.

## Economic controls

Evaluate after realistic commissions/spread/slippage/impact assumptions. Report turnover, break-even cost, drawdown and tail risk alongside Sharpe/Sortino.

## Statistical controls

Seed robustness does not replace multiple-testing correction. The candidate must still pass the project's DSR/PBO, SPA/Reality Check, MCS, benchmark-relative, placebo/null, capacity and cost-model gates.

## Falsification

Reject H87 if the candidate's apparent edge is concentrated in one or a small minority of seeds, if seed dispersion is materially larger than matched nulls without an economic reason, or if the aggregate conclusion disappears under adverse but pre-registered cost assumptions.
