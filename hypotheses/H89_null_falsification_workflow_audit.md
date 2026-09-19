# H89 — Null-Environment Falsification Workflow Audit

## Status
Pre-registered hypothesis; numerical test pending availability of the frozen candidate-level OOS prediction/return matrix.

## Motivation
A trading research pipeline can pass conventional OOS and multiple-testing checks while still producing false discoveries if its entire workflow has hidden structural leakage, adaptive search effects, or a backtest engine that behaves differently on null data than on real data. Recent 2026 work argues for falsification audits using zero-predictability environments and microstructure placebos, rather than relying only on performance corrections.

## Hypothesis
**H89:** A correctly implemented research workflow should not systematically produce economically meaningful, statistically significant trading performance when its predictive structure is destroyed while preserving the relevant time-series and execution characteristics.

## Primary falsification environments
1. **IID null:** returns independently resampled within the permitted causal data structure.
2. **Block null:** stationary/block bootstrap preserving short-range dependence and volatility clustering without predictive signal.
3. **Feature-permutation null:** features permuted within causal/time-safe blocks so marginal distributions remain plausible but feature/return alignment is destroyed.
4. **Microstructure placebo:** signal timestamps are shifted or matched to non-predictive execution timestamps while preserving turnover and holding-period mechanics.

## Required controls
- Same feature-generation code path as the real experiment.
- Same candidate search budget and model families.
- Same purging and embargo rules.
- Same transaction-cost and slippage assumptions.
- Same benchmark-relative metrics.
- Same DSR/PBO, SPA/Reality Check and MCS machinery.
- No threshold or model selection after observing null results.

## Pass criterion
The complete workflow must show no systematic excess performance in the null environments. In particular, the distribution of selected-best performance across null trials must be consistent with the multiplicity-adjusted null and must not repeatedly exceed the locked promotion thresholds.

## Failure interpretation
A null failure is a **pipeline failure**, not evidence of a profitable strategy. Any such failure blocks promotion of real-data candidates until the source is isolated and fixed.

## Confirmation discipline
The real confirmation set remains untouched. Null calibration and diagnostic decisions must be completed before confirmation is scored.
