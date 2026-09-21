# H141 — Real-Time Selection Falsification

Date: 2026-09-21

## Hypothesis

A candidate trading workflow that appears profitable under retrospective/date-keyed data will retain incremental net out-of-sample utility when evaluated with exact point-in-time information, an untouched final OOS period, identical research/search budgets, and realistic execution costs.

## Null / failure criteria

Reject the workflow if any of the following occurs:

- performance disappears when publication/revision timestamps replace calendar-date joins;
- performance disappears under label-shuffled or zero-predictability placebo data;
- the apparent winner is driven by a single seed, regime, asset, or execution assumption;
- the candidate loses its advantage under 1.5x or 2x transaction-cost stress;
- corrected purged/embargoed validation materially reduces the effect;
- the final OOS result cannot beat the strong non-ML baseline after accounting for selection multiplicity.

## Experimental arms

A. Candidate model with date-keyed data.
B. Same candidate with exact point-in-time timestamps.
C. Strong non-ML baseline.
D. Label-shuffled placebo with matched search budget.
E. Zero-predictability synthetic benchmark through the same pipeline.

## Required controls

- Purged/embargoed validation for overlapping labels.
- Final OOS locked before model selection.
- Complete trial ledger across architecture, feature, window, threshold, execution, and seed choices.
- Commission, spread, slippage, impact, borrow/capacity where relevant.
- Base, 1.5x and 2x cost stress.
- Execution-lag perturbation.
- Seed distribution and not only best seed.
- Regime and tail slices.
- DSR/PBO/CPCV or equivalent selection-aware diagnostics where sample structure permits.

## Primary metric

Incremental net OOS utility versus the strong baseline, with secondary reporting of Sharpe, maximum drawdown, turnover, breakeven transaction cost, tail loss, and seed dispersion.

## Promotion rule

Do not promote on statistical significance alone. Promotion requires economic improvement that survives the timestamp audit, placebo tests, cost stress, selection adjustment, and untouched final OOS.
