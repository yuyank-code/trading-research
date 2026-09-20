# H107 — Decision-Time One-Switch Leakage Sensitivity

## Motivation

Recent 2026 evidence shows that backtest inflation can be highly selective: changing only a decision-time convention (for example, using information from the daily bar before the simulated execution point) can materially inflate predictive and trading metrics, while other commonly suspected transformations may have much smaller effects. This motivates an explicit one-switch audit rather than a binary claim that a pipeline is simply “leakage free.”

## Hypothesis

If the research pipeline is decision-time correct, toggling one execution/information convention at a time around a clean causal reference should produce only small, explainable changes. Large and repeatable jumps identify a protocol-sensitive leakage surface.

## Protocol

1. Freeze the data panel, feature definitions, model family, walk-forward folds, portfolio rule, and cost model.
2. Define the clean reference as information available at decision time t and execution beginning at the next admissible market event.
3. Create one-switch variants only: same-day execution, centered temporal transforms, global-vs-training-only normalization, future-informed joins, and alternative close/open conventions.
4. Re-run identical OOS folds and preserve every path.
5. Report metric inflation relative to the clean reference: forecast score, turnover, gross return, net return, Sharpe, drawdown and hit rate.
6. Treat each switch as a diagnostic, not as a candidate optimization.
7. Promotion requires the clean reference to remain economically viable; no leaky variant may be used to justify a candidate.

## Pass criteria

A workflow passes only if the clean reference is used for all production claims and all intentional leakage switches are detected by automated assertions or materially flagged by the audit report. Any unexplained large performance increase under a one-switch violation is a pipeline failure.

## Status

Pre-registered. Numerical execution awaits immutable candidate-level OOS prediction/return artifacts.
