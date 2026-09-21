# H138 — Timestamp Fidelity vs Date-Keyed Information

**Status:** Proposed, not tested

## Claim
A candidate trading signal should retain its incremental net out-of-sample utility when every feature is constrained to the information actually available at the decision timestamp. If performance collapses, part of the apparent edge was caused by timestamp leakage.

## Null
Point-in-time timestamp correction does not materially reduce incremental net OOS utility relative to the date-keyed implementation.

## Alternative
Point-in-time correction materially reduces incremental net OOS utility.

## Required controls
- same model and hyperparameter budget;
- same purged/embargoed folds;
- no tuning on the final OOS period;
- exact publication/availability timestamps where possible;
- explicit latency buffers for uncertain feeds;
- commission, spread, slippage, market impact and borrow where applicable;
- 1x, 1.5x and 2x cost stress;
- execution-lag stress;
- strong baseline;
- timestamp-shuffled placebo;
- immutable row-level prediction-to-net-P&L ledger.

## Decision rule
Pre-register the retention threshold before observing results. Promote only if the point-in-time implementation passes the threshold and remains economically positive under stressed costs. Otherwise record the degradation as a failure/leakage finding.

## No-result rule
Until the corrected forward-label-overlap validation is implemented, neither the date-keyed nor point-in-time backtest is considered sufficient evidence for strategy promotion.
