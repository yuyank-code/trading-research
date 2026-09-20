# H111 — Research-Design Robustness

## Hypothesis

A candidate trading model that contains genuine, economically useful signal should retain its net OOS advantage across a preregistered set of reasonable research-design perturbations. If performance depends strongly on one arbitrary training window, rebalance convention, normalization rule, portfolio construction choice, or execution convention, the apparent edge is more likely to be selection-sensitive than robust.

## Null hypothesis

After realistic costs and multiple-testing adjustment, the candidate's economic advantage is not materially different across the preregistered perturbation battery; observed variation is consistent with sampling noise and research selection.

## Test

Use identical frozen candidate predictions wherever possible. Recompute only the specified research-design component using information available at each decision time. Preserve chronological OOS splits and all leakage controls.

Compare:

- baseline specification;
- alternative training windows;
- alternative holding/rebalance frequencies;
- training-only normalization variants;
- alternative portfolio/risk-scaling rules;
- execution-lag conventions;
- cost/slippage stress levels;
- fixed regime/subperiod partitions.

All attempted configurations count as trials, including failed and discarded configurations.

## Primary endpoint

Distribution of benchmark-relative net OOS return and risk-adjusted performance across the complete preregistered perturbation set.

## Secondary endpoints

- turnover;
- maximum drawdown;
- downside risk;
- break-even transaction cost;
- consistency across subperiods/regimes;
- fraction of perturbations retaining the sign of incremental net alpha;
- multiplicity-adjusted significance.

## Failure criteria

Fail H111 if the apparent advantage disappears under small reasonable specification changes, exists only in one favorable convention, or becomes statistically/economically weak after accounting for all perturbation trials.

## Promotion rule

H111 is not a license to optimize across perturbations. The battery is frozen before OOS inspection. Robustness is assessed from the full distribution, not the best configuration.

## Current status

Protocol committed. Numerical evaluation remains blocked until immutable candidate-level OOS prediction/return records and corrected forward-label-overlap validation are available.
