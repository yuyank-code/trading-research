# H99 — Pre-registered Hypotheses vs Adaptive Search

## Claim

A small set of pre-registered, economically motivated hypotheses should produce more reliable out-of-sample evidence than an adaptively searched candidate set when both are evaluated under identical execution costs and selection-aware inference.

## Motivation

Recent controlled research on LLM-driven strategy discovery reports that leakage-safe, search-aware evaluation can reject large candidate searches even when raw backtests look attractive. The result reinforces a distinction between hypothesis testing and unconstrained strategy mining: the evidential burden should rise with the amount of adaptive search.

## Test

Create two locked arms before touching the confirmation period:

1. **Pre-registered arm:** a small fixed set of hypotheses, model classes, features and execution rules specified before confirmation evaluation.
2. **Adaptive-search arm:** the same data, model families and execution simulator, but with a larger explicitly logged search budget.

Both arms must use the same:
- point-in-time data;
- label definitions and corrected overlap checks;
- purging/embargo rules;
- transaction costs, spread, slippage, impact and borrow assumptions;
- seed/trial ledger;
- confirmation period;
- DSR/PBO/SPA/Reality-Check/MCS controls.

## Primary outcome

Compare the two arms on **selection-adjusted incremental net OOS performance versus the same transparent baseline**.

Secondary outcomes: cost break-even, turnover, drawdown/tail risk, regime stability, and rank degradation from development to confirmation.

## Falsification

H99 fails if the pre-registered arm does not show better selection-adjusted confirmation behavior than the adaptive-search arm, or if any apparent advantage disappears after equal-cost execution and multiplicity correction.

## Promotion rule

No arm is promoted because of raw Sharpe, validation score, or a composite robustness grade alone. Structural information-set and label-overlap gates remain mandatory.
