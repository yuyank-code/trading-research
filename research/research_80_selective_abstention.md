# Research 80 — Selective Deployment, Abstention, and the Prediction-to-Trading Gap

## Evidence reviewed

A January 2026 preprint, *When Not to Trade: Leakage-Aware Selective Machine Learning for Factor Rotation*, proposes a rolling-origin deployment gate that compares an ML signal with a transparent fallback and abstains when validation evidence is insufficient. Its reported baseline experiment is promising, but it remains preprint evidence and therefore should be treated as hypothesis-generating rather than established alpha.

A May 2026 walk-forward BTC study evaluates roughly 70,000 hourly observations over 27 folds. It reports that naive sign trading fails after 10 bps transaction costs while a cost-aware forecast-magnitude filter reduces turnover and restores profitability in selected configurations; its bootstrap analysis does not establish formal dominance of XGBoost over neural alternatives.

A July 2026 NBER benchmark emphasizes real-time out-of-sample evaluation using only information available at the announcement timestamp, directly reinforcing the need for deployment-time information controls.

## Research implication

The economically relevant decision is not simply whether a forecast is accurate. It is whether the forecast is sufficiently valuable, relative to a fallback and after trading frictions, to justify changing the portfolio.

## New testable hypothesis

H131 tests whether selective abstention provides incremental net OOS utility versus always-trade, while controlling for selection through a matched-noise placebo and nested calibration.

## Failure conditions

The mechanism is not considered robust if its benefit disappears under corrected purge/embargo validation, realistic cost stress, execution-lag stress, or the matched-noise placebo; if thresholds are tuned on final OOS; or if gains are isolated to a single cost model or regime.

## Current conclusion

Literature supports testing selective deployment, but does not establish that it is robust alpha. The repository still lacks a validated immutable candidate-level OOS prediction-to-net-return artifact, so no new Sharpe, return, or promotion claim is made in this research pass.
