# Research 58 — Uncertainty-Aware Forecasts as a Trading Gate

## Research question

Does estimating forecast uncertainty add economically useful information beyond the point forecast itself, once the strategy is evaluated with causal timing, realistic execution costs, and a frozen confirmation sample?

## Literature

Rohit Allena (2026), *Confident Risk Premiums and Investments Using Machine Learning Uncertainties*, Review of Financial Studies 39(5), 1463–1505. The paper derives ex-ante confidence intervals for stock risk-premium forecasts and reports that confidence-filtered high-minus-low strategies improve out-of-sample returns and Sharpe ratios across the studied models. The reported effect increases with model complexity and decreases with model bias.

This is a useful hypothesis source, not a promotion criterion. The project will test whether the mechanism survives its own stronger controls, especially search accounting, costs, leakage audits, seed stability, and placebo workflows.

A complementary 2026 Journal of Financial Econometrics paper, *Neural-Network Volatility Forecasting*, reports that for the specifications studied, increasing sample size contributes more to volatility-forecasting performance than increasing model size or changing architecture. This motivates keeping uncertainty estimation simple enough that it does not become another high-dimensional source of overfitting.

The 2025 Review of Financial Studies paper *Man versus Machine Learning Revisited* remains a central warning: a previously reported ML trading alpha disappeared after a look-ahead-bias correction, with simpler linear models performing competitively. The journal also published an Expression of Concern concerning the original 2023 paper, reinforcing the need for strict provenance and reproducibility around published ML findings.

## Design implication

The project should treat uncertainty estimation as a separate model component with its own search budget. Any confidence threshold, calibration window, model class, or interval construction chosen after viewing confirmation performance counts as additional research trials.

The clean experiment is therefore:

forecast -> uncertainty estimate -> frozen gate -> execution simulator -> net OOS outcome

versus

forecast -> execution simulator -> net OOS outcome.

The same OOS timestamps, positions, turnover, costs, capacity assumptions, seeds, and benchmarks must be shared.

## Required diagnostics

1. Calibration of uncertainty against realized forecast error.
2. Net performance by uncertainty quantile.
3. Turnover and cost decomposition by gate intensity.
4. Break-even transaction-cost frontier.
5. Seed and regime stability.
6. Placebo workflow promotion rate.
7. Incremental performance relative to transparent baselines.
8. Multiple-testing correction over all gate specifications actually tried.

## Current conclusion

No robust alpha has been established. The literature supports a falsifiable mechanism: forecast precision may be useful for deciding when *not* to trade. The repository will only accept a positive result if it survives the project's causal timing, OOS, cost, placebo, power, and selection controls.
