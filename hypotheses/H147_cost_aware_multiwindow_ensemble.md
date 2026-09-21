# H147 — Cost-Aware Multiwindow Ensemble vs Single-Horizon Baseline

Date: 2026-09-22

## Hypothesis

A fixed, low-dimensional ensemble of causal models using distinct pre-specified lookback horizons can improve **net** out-of-sample utility versus the strongest single-horizon baseline, after realistic execution costs, without relying on horizon/weight/threshold selection that is itself overfit.

## Primary comparison

1. Single-horizon strong baseline.
2. Equal-weight multiwindow ensemble with horizons fixed ex ante.
3. Cost-aware adaptive weighting using only the training/meta window.
4. Matched-complexity placebo: random horizon assignment or random weights subject to the same turnover/exposure constraints.

## Required controls

- Point-in-time features and exact information timestamps.
- Purged/embargoed walk-forward validation for overlapping labels.
- Untouched final OOS period.
- Same model family and feature budget across arms where possible.
- All independent stochastic seeds retained.
- Commission, spread, slippage, market impact, borrow/capacity where relevant.
- 1x, 1.5x and 2x cost stress.
- Execution-lag stress.
- Regime and tail-period breakdowns.
- Research-trial ledger including failed configurations.

## Primary metrics

Net Sharpe/utility, turnover, maximum drawdown, tail loss, breakeven transaction cost, fraction of OOS windows with positive net utility, and stability across seeds and market regimes.

## Promotion rule

Do not promote unless the ensemble beats the single-horizon baseline on locked OOS after costs and remains superior to the matched-complexity placebo. A gain attributable only to lower turnover or lower exposure must be reported as a risk/execution effect rather than predictive alpha.

## Falsification

Reject H147 if the ensemble advantage disappears under realistic cost stress, is concentrated in one OOS window, fails the placebo comparison, or requires meta-layer choices that were selected using the final OOS period.

## Current blocker

The repository's forward-label-overlap validation issue remains unresolved; no historical numerical result should be promoted until corrected purged/embargoed validation is operational.
