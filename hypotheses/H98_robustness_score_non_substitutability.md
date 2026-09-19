# H98 — Composite Robustness Scores Must Not Substitute for Primary Gates

## Claim

A composite robustness score may improve research reporting, but it should not be allowed to replace the underlying information-availability, leakage, out-of-sample, execution-cost, and multiplicity gates.

## Motivation

Recent 2026 work proposes composite backtest-robustness scores combining Deflated Sharpe Ratio, Probability of Backtest Overfitting, Superior Predictive Ability, minimum track record, and regime stability. A large synthetic calibration can separate known signal from luck, but a pre-registered test on unseen real-market data reported no significant forward relationship between the score and subsequent outcomes. This is evidence that a score can be useful as an audit/reporting layer without being evidence of predictive power itself.

## Testable prediction

1. Composite scores should correlate with robustness on synthetic data with known ground truth.
2. On untouched real-market data, score rank should not be assumed to predict future net returns unless this relationship is demonstrated prospectively.
3. Any candidate passing a composite score but failing a primary structural gate must be rejected.

## Experimental protocol

- Freeze score definition and weights before confirmation data are inspected.
- Run on synthetic nulls, synthetic planted-signal environments, and untouched real-market confirmation data.
- Preserve the full trial ledger.
- Apply identical purging/embargo and realistic execution costs to all candidates.
- Report score calibration separately from trading performance.
- Require primary gates independently: causal information availability, corrected label-overlap validation, immutable OOS predictions/returns, cost frontier, and selection-aware inference.

## Falsification

Reject H98 if a pre-registered composite score repeatedly provides statistically significant incremental prediction of future net OOS performance beyond the individual primary gates across independent markets and confirmation periods.

## Status

Proposed. No alpha claim and no model promotion.
