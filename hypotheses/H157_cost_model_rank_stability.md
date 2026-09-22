# H157 — Cost-model rank stability

**Status:** registered, untested

## Hypothesis

If a candidate strategy contains economically meaningful signal rather than cost-model overfitting, its net out-of-sample ranking versus strong baselines should remain reasonably stable across a pre-specified plausible transaction-cost/slippage matrix.

## Required comparison

- candidate signal
- equal-weight / risk-only baseline
- strongest current simple predictive baseline
- turnover-matched placebo

## Required stresses

1x, 1.5x, and 2x aggregate costs; spread/slippage perturbations; execution delay; conservative liquidity/capacity assumptions; and alternative market-impact functional forms where supported by data.

## No re-optimization rule

No model, threshold, feature, horizon, or portfolio parameter may be changed after seeing a stress result. The stress matrix is an evaluation layer, not a tuning layer.

## Promotion gate

The candidate must retain positive net OOS utility and competitive rank across the pre-registered matrix, survive leakage audits and purged/embargoed validation, and pass multiplicity-aware significance checks. A single favorable cost specification is insufficient.

## Caveat

This hypothesis is motivated by 2026 literature showing that transaction-cost assumptions can materially alter both strategy profitability and the relative ranking of ML trading algorithms. Those published results do not establish that the same effect or any alpha transfers to this project.
