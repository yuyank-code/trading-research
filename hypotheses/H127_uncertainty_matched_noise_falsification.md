# H127 — Uncertainty Signal vs Matched-Noise Falsification

## Status

Proposed. This hypothesis is a direct falsification test of H126 rather than an assumption that predictive uncertainty is economically useful.

## Motivation

Recent evidence is mixed. Liu, Luo, Wang, and Zhang (2026) report gains from uncertainty-adjusted sorting, mainly through lower volatility. In contrast, Cho (2026), *When uncertainty doesn't help: Operator learning ignores belief uncertainty in portfolio optimization*, reports that calibrated uncertainty channels did not reliably improve out-of-sample certainty-equivalent performance across multiple architectures and held-out crash/OOD tests; matched-variance random-noise controls were often indistinguishable.

The disagreement makes a controlled placebo test more valuable than adding another uncertainty model.

## Test

For every frozen candidate and identical OOS timestamps, compare:

1. Point-prediction portfolio.
2. Uncertainty-adjusted portfolio using forecast uncertainty calibrated only inside the training/validation fold.
3. Matched-variance noise control replacing the uncertainty channel while preserving its marginal distribution.

Keep universe, signal timestamp, portfolio construction, execution, turnover limits, and cost model identical.

## Required stresses

- realistic spread, slippage, impact and other applicable costs;
- 1.5x and 2x cost stress;
- execution-lag perturbation;
- purged/embargoed validation for overlapping labels;
- selection-aware inference over every uncertainty threshold/model choice;
- held-out regime/crash/OOD slices;
- seed stability where stochastic models are used.

## Primary decision rule

Uncertainty adjustment is supported only if it beats point prediction on incremental **net** OOS utility and also beats the matched-noise placebo with a pre-specified effect-size margin across the majority of pre-declared folds/regimes.

If uncertainty adjustment is statistically/economically indistinguishable from matched noise, H126 is rejected as evidence that uncertainty itself is useful.

If it beats point prediction before costs but not after costs, reject as economically non-tradable.

If the result requires final-OOS threshold tuning, reject as selection/leakage.

## Required artifact

Immutable row-level OOS record:

`information_cutoff, prediction, uncertainty, placebo_uncertainty, position, execution_price, turnover, gross_return, commission, spread, slippage, impact, borrow_or_funding, net_return, fold_id, model_version, seed`
