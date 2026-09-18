# H76 — Data-Snooping and Survivorship-Bias Stress Test

## Motivation

Recent financial-ML validation work reinforces that a large search over specifications can manufacture apparently significant results even under zero-predictability nulls, while replication quality deteriorates when the effective search space becomes large. This motivates a dedicated stress test for the *data universe itself*, not only model hyperparameters.

Sources reviewed this pass:

- Nikolopoulos (2026), *Spurious Predictability in Financial Machine Learning*: adaptive specification search can create significant walk-forward evidence under martingale-difference nulls; recommends synthetic zero-alpha and microstructure placebo audits.
- Kim (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*: reports that AUC/permutation evidence can remain economically irrelevant and argues for CPCV/PBO plus economic gates.
- Saly-Kaufmann et al. (2026), *Deep Learning for Financial Time Series*: benchmark spans futures and FX and evaluates OOS risk, break-even costs and seed robustness rather than accuracy alone.

## Hypothesis

**H76:** A candidate that survives model-level leakage and multiple-testing controls should remain viable when the historical asset/data universe is reconstructed using only securities that were actually available at each date. If performance depends materially on a hindsight-defined universe, the apparent edge is contaminated by survivorship/data-selection bias.

## Test design

Compare, without changing signal code or model search budget:

1. a hindsight/static universe;
2. a point-in-time eligible universe;
3. a deliberately perturbed eligibility universe using only information available by each decision date.

All variants use the same chronological OOS protocol, embargo rules, frozen confirmation block, execution model, and cost assumptions.

Report:

- net OOS Sharpe and Sortino;
- maximum drawdown and tail loss;
- turnover and capacity;
- break-even transaction cost;
- candidate rank stability;
- performance delta between static and point-in-time universes;
- whether the economic conclusion changes.

## Falsification / promotion rule

A material performance advantage that disappears under point-in-time eligibility is **not evidence of alpha**. No re-tuning is permitted after seeing the point-in-time result. Any universe definition that is selected after inspecting OOS results counts toward the research-search budget.

## Status

**Pre-registered. Not empirically passed.** The frozen candidate-level OOS return/prediction matrix and point-in-time eligibility data are still required for numerical evaluation.
