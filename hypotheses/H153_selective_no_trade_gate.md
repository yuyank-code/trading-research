# H153 — Selective No-Trade Gate vs Always-Trade Baseline

## Hypothesis

A pre-specified, point-in-time selective deployment rule that abstains when predicted edge does not exceed a validated cost/risk hurdle will improve net out-of-sample utility relative to always trading the same underlying signal, while beating a turnover/coverage-matched placebo gate.

## Null hypothesis

Any observed improvement is attributable to reduced trading frequency, exposure smoothing, or selection noise rather than economically informative abstention.

## Controls

- Same underlying forecast model.
- Same universe and position limits.
- Same training and feature information.
- Always-trade baseline.
- Fixed cost hurdle.
- Validation-calibrated gate.
- Turnover/coverage-matched placebo gate.

## Hard requirements

1. Point-in-time data only.
2. Purged/embargoed validation using the maximum label horizon.
3. Gate calibration occurs only on data preceding the evaluation window.
4. Final OOS is untouched during model/gate selection.
5. Full execution ledger includes spread, commission, slippage, impact, borrow and turnover as applicable.
6. Stress costs at 1x/1.5x/2x and execution delay without retuning.
7. Record all threshold and gate trials for multiple-testing correction.
8. Run the same search workflow on null data.
9. Require improvement over a matched placebo, not merely lower turnover.

## Success criterion

The selective rule is promoted only if it delivers a statistically and economically meaningful improvement in net OOS utility, survives 1.5x cost stress, and does not show a comparable gain on the null workflow. If it only lowers volatility/turnover without improving cost-adjusted edge, classify the result as risk control rather than predictive alpha.
