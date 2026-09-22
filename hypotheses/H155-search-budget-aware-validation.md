# H155 — Search-Budget-Aware Validation

Date: 2026-09-22

## Claim to test

Explicitly accounting for the research/search budget, preserving an untouched final holdout, and applying multiplicity-aware validation should reduce false strategy discoveries without eliminating genuinely strong signals.

## Controls

A. Existing validation workflow.
B. Same workflow + effective trial count.
C. Same workflow + purged/embargoed CPCV + PBO/DSR.
D. Same as C + minimum-track-record gate.
E. Null/placebo versions of A-D.
F. Injected-signal versions of A-D with controlled signal-to-noise ratios.

## Primary metrics

- false-positive rate under null data;
- recovery rate of injected signals;
- final OOS net Sharpe and utility;
- PBO and DSR;
- minimum track record required by the selected significance threshold;
- sensitivity to 1x/1.5x/2x transaction-cost assumptions.

## Leakage requirements

All transformations, feature selection, scaling, hyperparameter tuning and model fitting must be performed using information available inside the corresponding training window. Overlapping forward labels must be purged; embargo length must cover the maximum label horizon plus any required execution/feature lookback buffer.

## Multiple-testing accounting

The ledger must record every candidate inspected before selection, including discarded feature sets, horizons, seeds, cost assumptions used during research, model architectures and execution rules. Correlated candidates should additionally be summarized with an effective-trial estimate rather than relying only on nominal trial count.

## Decision rule

Do not promote a candidate merely because the stricter workflow produces a lower p-value or higher OOS Sharpe. The gate is successful only if it materially suppresses null discoveries while preserving pre-specified injected signals and remains economically viable after realistic costs.

## Current status

Hypothesis registered; implementation and null/injected-signal experiments pending. No alpha claim.
