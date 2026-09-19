# H83 — Time-Scale Ensemble Stability

## Question
Does combining forecasts built on pre-specified, causally available lookback windows improve net out-of-sample trading performance and reduce sensitivity to regime/estimation-window choice relative to the best single window selected ex post?

## Motivation
Recent 2026 FX research evaluates transparent multiwindow ensembles with non-overlapping OOS blocks and cost-aware supervisory weighting. The relevant lesson for this project is not that a multiwindow ensemble is profitable, but that time-scale diversity can be tested as a robustness mechanism rather than selecting one lookback after inspecting OOS outcomes.

## Falsifiable hypothesis
For a frozen candidate model family, a pre-registered equal-weight or validation-only cost-aware ensemble across a small fixed set of causal lookbacks will have higher or more stable net OOS utility than the median single-lookback model, without materially increasing turnover or search exposure.

## Pre-registration
- Lookbacks are fixed before confirmation: 8, 16, and 32 observations.
- No confirmation-period information may determine weights, lookbacks, thresholds, or model family.
- Any supervisory weighting is fitted only within each training/validation fold.
- The maximum label horizon determines purge/embargo requirements.
- All variants are evaluated under identical execution, spread, slippage, impact, and capacity assumptions.

## Primary metrics
- Net Sharpe and Sortino.
- Benchmark-relative net utility.
- Maximum drawdown and expected shortfall.
- Turnover and implementation shortfall.
- Break-even transaction cost.
- Fold/regime stability.

## Robustness gates
- Purged/embargoed walk-forward OOS.
- Locked confirmation set.
- DSR/PBO and search-count accounting.
- SPA/Reality Check and Model Confidence Set where applicable.
- Matched-count random-window placebo.
- Synthetic zero-alpha null.
- Adverse-cost and impact stress.
- Seed stability if stochastic models are used.

## Failure conditions
Reject H83 if the ensemble advantage:
1. appears only after inspecting confirmation results;
2. disappears under modest cost/impact stress;
3. is concentrated in one regime/fold;
4. is matched by placebo windows;
5. requires materially more tuning/search than the comparator;
6. depends on a single arbitrarily selected lookback or weighting rule.

## Current status
Pre-registered. No empirical pass. The project still requires corrected forward-label-overlap validation and an immutable candidate-level OOS prediction/return matrix before numerical claims are permitted.
