# Research 68 — Volatility-Gated Execution and Cost-Aware Deployment

## Date
2026-09-21

## Research question
Can a trading model's economic value improve by selectively refusing to execute predictions when market volatility or expected friction makes the forecast too expensive to monetize?

## Literature
A September 3, 2026 SSRN preprint by Mukitu Islam Nishat studies volatility-gated inference on EUR/USD daily data from 2019 through August 2026. Its reported experiment compares an always-on directional model with a post-hoc volatility gate and finds fewer trade switches and better reported OOS economics for the gated strategy. Because this is a single preprint experiment, it is evidence for a testable mechanism rather than proof of generalizable alpha.

A May 19, 2026 arXiv study of hourly BTC-USDT walk-forward forecasting similarly reports that naive sign trading can lose money after 10-bps transaction costs, while a forecast-magnitude execution threshold can reduce turnover and recover profitability in selected configurations. The paper also reports that bootstrap evidence does not establish formal statistical dominance for XGBoost.

A July 2026 SSRN paper on leakage-aware selective ML proposes deployment only when a candidate improves a transparent fallback by a calibrated validation threshold, otherwise abstaining. Its reported results are promising but remain preprint evidence.

A March 2026 large-scale futures benchmark evaluates financial deep-learning systems with OOS performance, statistical significance, tail risk, break-even transaction costs and seed robustness, reinforcing that economic evaluation must go beyond predictive loss.

## Synthesis
The literature points to a common mechanism: prediction quality and tradability are separate objects. A forecast can be statistically useful while being economically unprofitable when expected edge is smaller than all-in execution friction. A selective execution layer is therefore worth testing, but the gate itself becomes another model-selection opportunity and must be subjected to the same leakage, multiple-testing and null controls as the underlying predictor.

## Project implication
H119 is added as the next falsifiable experiment. The gate will be tested against always-trade, a frozen fallback, a cost-threshold gate and placebo predictions. Gate calibration remains inside training/validation only; the final OOS period is locked.

## Evidence status
- Mechanism supported by converging recent literature: YES.
- Project-specific numerical evidence: NOT YET.
- Robust alpha established: NO.
- Promotion: NO.

## Sources
- Nishat (2026), "Mitigating Transaction-cost Degradation in Financial Forecasting via Volatility-gated Inference," SSRN 7405518.
- Bysik & Ślepaczuk (2026), "Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting," arXiv:2606.00060.
- Guo (2026), "When Not to Trade: Leakage-Aware Selective Machine Learning for Factor Rotation," SSRN 7021298.
- Saly-Kaufmann et al. (2026), "Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance," arXiv:2603.01820.
