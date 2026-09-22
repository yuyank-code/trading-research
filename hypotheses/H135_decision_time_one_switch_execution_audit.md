# H135 — One-Switch Decision-Time Execution Audit

## Claim to test

A candidate's apparent predictive and trading performance is invariant to replacing any signal/execution convention with a strictly decision-time-valid convention, except for the mechanical effect of execution delay and costs.

## Null

Changing only the information/execution convention at the decision boundary does not materially change candidate-minus-baseline net OOS utility.

## Alternative

A decision-time correction materially reduces predictive or trading performance, indicating that the original protocol contained decision-time leakage or an execution mismatch.

## Required design

- Freeze the same data panel, folds, model family, feature set, and search budget.
- Change exactly one convention at a time.
- Use an explicit information cutoff for every feature.
- Execute at the first price that is actually observable after the cutoff.
- Preserve purge/embargo and all fold-local transformations.
- Compare gross prediction metrics and net trading utility separately.
- Repeat under baseline, 1.5x, and 2x costs plus execution-lag stress.
- Preserve row-level artifacts identifying information cutoff, execution timestamp, and label end.

## Falsification

The hypothesis is rejected if a one-switch correction causes a material deterioration that cannot be explained by the mechanical execution delay/cost change, or if the sign of candidate-minus-baseline incremental utility reverses.

## Promotion rule

Any candidate whose evidence depends on a convention that is not valid at decision time is BLOCKED, regardless of Sharpe, AUC, or statistical significance.

## Motivation

Zhang et al. (2026), *When Alpha Disappears*, show that some apparently small backtest convention changes—especially centered temporal features and same-day-open execution using post-open daily-bar information—can create large, stable inflation in both predictive and trading metrics. Their paired one-switch design is directly applicable to this project.

## Current status

REGISTERED. Numerical execution is blocked until the immutable prediction-to-execution artifact is available.
