# Research 53 — Selective Deployment and Cost-Aware Abstention

## Core evidence
A 2026 SSRN paper proposes leakage-aware selective ML deployment: deploy a model only when its validation improvement over a transparent fallback exceeds a calibrated threshold, otherwise abstain and fall back. Its reported sector-rotation experiment is promising but remains hypothesis-generating for this project.

A 2026 BTC walk-forward study provides complementary evidence: naive sign-based ML strategies fail under 10 bps transaction costs, while a forecast-magnitude execution threshold reduces turnover and restores profitability in selected configurations; formal model dominance was not established.

A 2026 large-scale futures benchmark further supports evaluating statistical significance, downside/tail risk, breakeven transaction costs and random-seed robustness together rather than optimizing average Sharpe alone.

## Project implication
The economically relevant object is not merely the forecast. It is the complete predictable policy: forecast -> deploy/abstain decision -> portfolio -> execution.

## New testable direction
H103 tests whether selective deployment adds incremental net OOS value beyond always trading the same frozen signal. The test must use the same baseline, execution simulator, costs, purging/embargo, trial ledger and placebo workflow.

## Guardrails
The literature does not justify adopting a selective gate automatically. A gate can itself become a new overfitting layer if its threshold, validation window, fallback and trading rules are tuned repeatedly. Therefore gate parameters must be frozen before confirmation, included in the search budget, and tested on placebos.

## Current conclusion
The evidence supports testing selective deployment as an execution/risk-control hypothesis, not as established alpha. No model promotion follows from this research alone.
