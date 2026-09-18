# Research 21 — Volatility normalization and regime robustness

## Literature synthesis

A March 2026 large-scale benchmark of financial time-series models evaluates daily futures across commodities, equity indices, bonds, and FX from 2010–2025 using out-of-sample risk-adjusted performance, downside/tail-risk measures, break-even transaction costs, random-seed robustness, and computational efficiency. The methodological implication for this project is that a model should not be judged by directional accuracy or gross return alone.

A January 2026 macro portfolio study proposes robust objectives that explicitly penalize poor historical windows and reports that regime robustness can be materially different from average historical performance. This is useful motivation, but its reported results are not evidence for our FX strategy because the datasets and strategy are different.

A 2026 BTC walk-forward study provides a complementary execution lesson: positive gross ML forecasts did not automatically survive transaction costs, while cost-aware trade selection improved selected configurations. Therefore risk normalization must be evaluated jointly with realistic costs rather than in a frictionless backtest.

## New research question

Can a simple causal volatility-normalization layer improve the *distribution* of net OOS outcomes for a frozen signal, rather than merely improving the average backtest?

## Proposed experiment

Keep the predictive model, features, signal threshold, execution timing and universe fixed. Change only the position-sizing layer:

- unscaled/unit sizing;
- causal rolling-volatility targeting;
- the same targeting rule with a conservative exposure floor/cap.

The volatility estimator must use only observations available before the decision. Its parameters are frozen before the outer test.

## Primary evidence

The preferred outcome is not maximum Sharpe. The strongest evidence would be a consistent reduction in downside/tail risk and drawdown across independent OOS folds/regimes while preserving acceptable net Sharpe and break-even costs.

## Anti-overfitting controls

- one untouched confirmation period;
- purging and embargoing for overlapping labels;
- no test-set parameter tuning;
- report every tested sizing specification;
- DSR/PBO for selected candidate families;
- SPA/Reality Check when comparing a family of related strategies;
- synthetic null workflow to ensure the sizing layer cannot manufacture alpha.

## Execution controls

Use the same cost engine as H68, including liquidity/size-conditioned impact and adverse cost stress of 25%, 50%, and 100%. Report turnover, participation, implementation shortfall and break-even costs alongside returns.

## Current conclusion

This is a testable robustness hypothesis, not an observed trading edge. The repository currently does not contain a frozen OOS signal/return matrix sufficient to produce honest numerical results. The correct next step is to run H69 only after that artifact is frozen.

## Sources

- Saly-Kaufmann, Wood, Peter-Calliess, Zohren (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*, arXiv:2603.01820.
- *DeePM: Regime-Robust Deep Learning for Systematic Macro Portfolio Management* (2026), arXiv:2601.05975.
- Bysik & Ślepaczuk (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*, arXiv:2606.00060.
