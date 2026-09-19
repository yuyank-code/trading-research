# H94 — Committed Trial Ledger and Effective Search Budget

## Status
Proposed — pipeline gate, not yet an empirical alpha result.

## Hypothesis
If candidate evaluation is corrected for the full research search budget — including model families, hyperparameters, feature variants, execution rules, thresholds, seeds, and researcher-visible branch decisions — then apparent OOS winners should lose statistical support relative to an evaluation that counts only the final reported configuration.

## Motivation
The practical weakness of Deflated Sharpe Ratio (DSR) is that the trial count can itself be researcher-supplied. Recent 2026 work argues for a committed trial ledger so the multiplicity correction cannot be reduced after observing results. Recent DRL evidence likewise shows that selecting the best random seed creates a multiplicity problem analogous to hyperparameter search.

## Pre-registration rule
Before confirmation data are evaluated, record one immutable ledger entry for every candidate-producing decision:

- feature/label specification
- model family
- hyperparameter configuration
- training-window choice
- portfolio construction
- threshold/execution rule
- cost/slippage model
- random seed
- data/universe version
- benchmark choice
- failed or abandoned candidates that produced an observed performance result

No trial may be removed because it was unsuccessful, redundant, or later considered exploratory.

## Primary test
Compare:

1. naive DSR using only the final candidate count;
2. committed-ledger DSR using the full candidate-generation history;
3. selection-aware null distribution generated with the same search budget.

The candidate is only considered statistically credible if it survives (2) and separates from (3).

## Falsification
H94 fails if the committed ledger does not materially change the selection-adjusted conclusion in controlled null searches, or if ledger counting can be changed without changing the reported inference.

## Guardrails
This is an inference-control hypothesis. It does not replace purged/embargoed OOS testing, leakage fixtures, realistic execution costs, SPA/Reality Check, PBO, MCS, or untouched confirmation.
