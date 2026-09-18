# Research 22 — Complexity vs. Robustness in Trading ML

## Date
2026-09-18

## Literature synthesis

A 2025 *Review of Financial Studies* paper, "Man versus Machine Learning Revisited," revisits an influential machine-learning predictability result and finds that the reported trading alpha disappears after correcting a look-ahead bias. The authors report that linear models remain competitive and that alternative ML models do not restore the removed predictability. The practical lesson is not that ML is useless; it is that a more flexible model cannot be credited with economic value until the information set and evaluation protocol are demonstrably causal.

A 2026 *Review of Financial Studies* paper, "Confident Risk Premiums and Investments Using Machine Learning Uncertainties," provides complementary evidence that forecast uncertainty can matter for portfolio construction: strategies restricted to observations with more precise forecasts can improve out-of-sample performance in its stock-risk-premium setting. This supports treating model uncertainty as an explicit variable, while not assuming the result transfers to FX.

A 2025 *Review of Finance* study on tradable risk factors finds a 2–4 percentage-point annual implementation shortfall between paper factors and implementable versions after accounting for trading frictions, reinforcing that model comparisons must be made after execution costs rather than on statistical forecasts alone.

## Implication for this project

The next model comparison should not ask "which ML model has the highest backtest Sharpe?" It should ask whether complexity creates a reproducible incremental economic contribution after controlling for the same information set, search budget, OOS protocol and execution assumptions.

This motivates H70: Complexity Premium Audit.

## Testable prediction

If nonlinear models capture genuine structure unavailable to a regularized linear baseline, their incremental net OOS performance should persist across independent walk-forward folds and remain positive under cost stress. If the apparent advantage is primarily model-selection noise or leakage sensitivity, the advantage should shrink toward zero or reverse on untouched data.

## Evidence classification

- Theory/literature: complexity can increase fit while increasing selection risk.
- Empirical literature: recent work shows at least one prominent ML trading result was not robust to look-ahead correction.
- Project hypothesis: FX-specific complexity premium remains unestablished.

## Status

Literature synthesis complete; no project performance claim. Numerical evaluation awaits the frozen OOS signal/return dataset.
