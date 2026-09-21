# H126 — Uncertainty-Adjusted Signal Selection

## Hypothesis

For flexible return-prediction models, ranking trades by a conservative uncertainty-adjusted signal (rather than point forecast alone) can improve net out-of-sample utility by suppressing low-confidence positions, without creating a hidden tuning advantage.

## Motivation

Liu, Luo, Wang, and Zhang (2026), *Uncertainty-Adjusted Sorting for Asset Pricing with Machine Learning*, report that uncertainty-adjusted prediction bounds can improve portfolio performance relative to point-prediction sorting, with gains arising mainly from reduced volatility. The result is a preprint and therefore hypothesis-generating for this project.

## Falsification design

Compare, on identical timestamps and candidate universe:

1. point-forecast ranking;
2. lower-confidence-bound ranking;
3. upper-confidence-bound ranking where directionally appropriate;
4. uncertainty-neutralized random/placebo ranking using the same portfolio construction.

Uncertainty estimates must be produced using only information available at the prediction timestamp. Calibration is restricted to the training/validation portion of each walk-forward fold. No final OOS observation may influence calibration or threshold selection.

## Primary metric

Incremental net OOS utility versus point-forecast ranking after all execution costs.

## Required robustness checks

- purging and embargo for overlapping labels;
- point-in-time feature availability;
- commissions, spread, slippage and market impact;
- 1.5x and 2x cost stress;
- one-bar execution-lag stress;
- turnover and capacity diagnostics;
- subperiod/regime stability;
- random-seed stability for stochastic models;
- multiple-testing/search accounting;
- placebo uncertainty scores generated independently of future returns.

## Promotion rule

No promotion unless the uncertainty-adjusted method beats the frozen point-forecast baseline on net OOS utility, survives cost stress and execution lag, and retains the advantage after selection-aware inference. A positive result in only one favorable subperiod is insufficient.

## Current status

**UNTESTED.** The repository currently does not contain the immutable candidate-level OOS prediction -> position -> turnover -> realized-return -> cost artifact required to evaluate this hypothesis.

## Source

Yan Liu, Ye Luo, Zigan Wang, Xiaowei Zhang (2026), *Uncertainty-Adjusted Sorting for Asset Pricing with Machine Learning*, working paper/preprint, January 2026.
