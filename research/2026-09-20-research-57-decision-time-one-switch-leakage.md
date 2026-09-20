# Research 57 — Decision-Time One-Switch Leakage Audit

## Literature update

A 2026 benchmark, *When Alpha Disappears: A One-Switch Benchmark for Decision-Time Leakage in Financial Backtests*, studies leakage by changing one evaluation convention at a time around a clean t+1-open reference while holding the panel, walk-forward split, model family, portfolio rule and cost convention fixed. It reports that centered temporal features and same-day-open execution using post-open daily-bar information can create large and stable inflation, while several other suspected conventions have much weaker effects.

A separate 2026 study, *Spurious Predictability in Financial Machine Learning*, argues that adaptive specification search can create significant walk-forward evidence under martingale-difference nulls and proposes falsification of complete workflows against zero-predictability and microstructure-placebo environments.

## Research implication

The project should not treat leakage as a binary property. We need a quantitative **decision-time sensitivity surface** showing how much performance changes when exactly one timing convention is violated. This is complementary to purging, embargoing and label-overlap controls: those controls protect fold construction, while this audit tests the information/execution contract inside each fold.

## Testable design

Clean reference:
- feature timestamp <= information cutoff;
- model fit only on observations whose information cutoff precedes the fold boundary;
- order generated after the final admissible observation;
- execution starts at the next admissible event;
- costs applied to actual position changes.

One-switch violations:
- post-open information used for same-open execution;
- centered rolling features;
- global normalization;
- future-informed joins;
- same-bar close/execution mismatch.

For every switch preserve the exact OOS path and calculate deltas in forecast quality, turnover, gross return, net return, Sharpe and maximum drawdown. The switch suite is diagnostic and must not increase the trial count used to select a production model.

## Current finding

No new alpha is claimed. The repository contains research protocols and hypotheses but does not yet contain the immutable candidate-level OOS prediction/return matrix required to execute this comparison credibly. The existing README continues to identify forward-label overlap as a blocker for trusting older model results.

## Verdict

**Pipeline improvement: YES. Robust trading alpha: NOT ESTABLISHED.**
