# H45 — Complete Trial Registry and Selection Freeze

**Status:** Proposed
**Date:** 2026-09-11

## Hypothesis

A trading result is not promotable unless every materially tested candidate is recorded before the final holdout is opened, and the selected policy is frozen before final evaluation.

## Motivation

The production research engine currently evaluates multiple feature-source configurations and an ensemble of three model families. The research history also contains repeated changes to labels, execution rules, costs, and validation procedures. Treating only the final candidate as the effective trial count would understate selection pressure.

Bailey & López de Prado (2014) show that the Deflated Sharpe Ratio must account for selection bias from multiple trials and non-normal returns. Recent 2026 work combining DSR, PBO, SPA and minimum-track-record diagnostics likewise treats the validation layer as a post-selection robustness audit rather than evidence of future profitability.

## Required registry fields

Each materially tested candidate must record:

- immutable trial ID
- code/data version or commit SHA
- dataset snapshot/hash
- feature set and feature availability rule
- target/event definition and horizon
- model family and hyperparameters
- random seed(s)
- training/validation/test split and embargo/purge rule
- execution model
- fee, spread, slippage and impact assumptions
- position/risk controls
- threshold/filter parameters
- whether the candidate was selected, rejected, or superseded
- reason for selection/rejection

## Selection protocol

1. Development data may be used for hypothesis generation and model selection.
2. All materially tested candidates are entered into the registry.
3. A single policy is frozen using development evidence.
4. The untouched final holdout is opened exactly once for the frozen policy.
5. No threshold, feature, model, cost assumption, execution rule, or risk control may be changed after viewing final-holdout results without restarting the final evaluation.
6. DSR/PBO/SPA use the documented trial history rather than only the winning candidate.

## Falsification / promotion rule

If the final holdout requires any post-hoc change, the holdout is considered contaminated and the result is not a final confirmation.

If the complete registry cannot be reconstructed, the result is downgraded to exploratory regardless of its raw Sharpe, return, or predictive metric.

## Current implication

No new profitability claim should be promoted until the registry exists and the frozen OOS artifacts can be reproduced from the recorded data/code versions.
