# Research 82 — Volatility Forecastability as a Separate Economic Channel

## Date
2026-09-21

## Research question
Is the project's effort better spent on forecasting conditional volatility/risk state and using that information for position sizing or exposure control, rather than forcing a weak next-period signed-return forecast to carry the entire trading signal?

## Literature signal
A June 2026 leakage-controlled benchmark on US mega-cap equities compared naive baselines, regularized linear models, tree ensembles, LSTM, Transformer and graph-attention models using 41 expanding-window causal folds with fold-isolated preprocessing. Its central result was an asymmetry: next-day signed-return prediction remained close to strong simple baselines, while next-day volatility-proxy prediction was more separable and forecastable. The result is useful as a research direction, not proof that volatility timing is profitable.

A July 2026 transaction-cost study of hourly BTC trading likewise reports a large prediction-to-trading gap: complex-model improvements in forecast metrics did not compensate for trading frictions, while simple cost-aware filters materially reduced turnover. This reinforces testing whether a forecast is economically useful only after it is translated into a low-turnover decision.

A March 2026 market-impact study further shows that the execution-cost model can change both absolute performance and relative model ranking. Therefore any volatility-based sizing rule must be evaluated through the same execution engine as the return-signal arms.

## Proposed mechanism
Use a strictly point-in-time volatility estimate/forecast to scale an independently specified directional signal or baseline exposure. The volatility model is not allowed to select the return-model architecture, feature set, or final OOS period.

## Experimental comparison
A. Unscaled directional baseline
B. Volatility-scaled baseline using realized-volatility information available at decision time
C. Volatility-forecast-scaled baseline
D. Forecast-only placebo with matched conditional variance information but no genuine predictive content
E. Strong non-ML risk-control baseline

The primary question is not whether volatility forecasting improves raw return. It is whether it improves net OOS risk-adjusted utility, drawdown control, turnover-adjusted utility, or tail loss without creating selection leakage.

## Required controls
- fold-isolated feature preprocessing;
- point-in-time timestamps and reporting lags;
- purging/embargo matched to every forward horizon;
- volatility-target parameters frozen before final OOS;
- identical universe, signal, execution and cost engine across arms;
- commission, spread, slippage, market impact and borrow/funding where applicable;
- 1x / 1.5x / 2x cost stress;
- execution-lag perturbation;
- crash/regime slices;
- placebo volatility signal;
- complete search/trial ledger;
- immutable row-level prediction -> position -> execution -> turnover -> gross P&L -> cost -> net P&L artifact.

## Interpretation
A volatility model is not promoted merely because it lowers volatility or raises Sharpe. It must create incremental net OOS utility relative to an equally risk-controlled baseline. If the benefit disappears against a simple realized-volatility scaler, the ML volatility forecast has not demonstrated incremental value.

## Status
OPEN. No numerical result claimed in this research pass.
