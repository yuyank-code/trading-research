# Research 76 — Uncertainty Selection Requires a Matched-Noise Control

## New evidence

A June 2026 Finance Research Open article by WonChan Cho, *When uncertainty doesn't help: Operator learning ignores belief uncertainty in portfolio optimization*, reports a controlled test of predictive uncertainty. Across multiple portfolio-policy architectures, time-split validation and held-out crash/OOD tests, calibrated uncertainty features did not reliably improve out-of-sample certainty-equivalent performance over mean-only inputs. Replacing uncertainty with variance-matched random noise was often indistinguishable.

This is important because H126 currently treats uncertainty as a potentially useful trade-selection variable. The new evidence supplies a credible null: an uncertainty channel can look useful without the policy actually using information contained in that channel.

The evidence is not universal: Liu et al. (2026) report positive results from uncertainty-adjusted sorting in U.S. equities. Therefore the correct conclusion is not that uncertainty is useless, but that any claimed benefit must beat a matched-noise placebo under the same economic evaluation.

A 2026 BTC walk-forward study provides a separate execution lesson: complex models can produce positive frictionless results while naive trading fails under 10-bps costs; cost-aware filtering can reduce turnover and recover economics in selected configurations, but model dominance remains statistically fragile.

## Research implication

H126 should not be evaluated as a simple point-forecast versus uncertainty-adjusted comparison. It needs a third arm:

**point prediction -> uncertainty-adjusted -> matched-variance-noise placebo**.

The placebo is essential because an uncertainty channel can act as a generic regularizer or selection variable without carrying economically useful information about forecast error.

## Experimental controls

- calibrate uncertainty only inside each training/validation fold;
- preserve identical OOS timestamps and universe;
- use purging/embargo for overlapping labels;
- freeze all thresholds before final OOS;
- evaluate realistic costs plus 1.5x and 2x stress;
- include execution-lag stress;
- report fold/regime distributions rather than only pooled Sharpe;
- apply selection-aware inference to all searched thresholds;
- retain immutable row-level prediction-to-net-return accounting.

## Decision standard

Support uncertainty only if it produces a pre-specified, economically meaningful incremental net-OOS improvement over both point prediction and matched noise. Otherwise classify the result as null, placebo-equivalent, cost-fragile, or selection-dependent rather than as evidence of alpha.

## Sources

- Cho (2026), *When uncertainty doesn't help: Operator learning ignores belief uncertainty in portfolio optimization*, Finance Research Open, DOI 10.1016/j.finr.2026.100107.
- Liu, Luo, Wang, Zhang (2026), *Uncertainty-Adjusted Sorting for Asset Pricing with Machine Learning*, arXiv:2601.00593.
- Bysik & Ślepaczuk (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*, arXiv:2606.00060.
