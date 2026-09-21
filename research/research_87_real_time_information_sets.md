# Research 87 — Real-Time Information Sets and Timestamp Fidelity

## Date
2026-09-21

## Research question
Can a strategy that appears out-of-sample under ordinary date-based splits lose its edge when every feature is restricted to the exact timestamp at which the information became available to a trader?

## Literature
- Koijen & Levy, **Assessing the Benefits of Optimized Agentic AI Systems for Asset Pricing**, NBER Working Paper 35431 (July 2026). They emphasize real-time, announcement-time information sets to avoid look-ahead bias.
- Bhand & Joshi, **The Illusion of Alpha: Quantifying Hidden Data Leakage in Financial Machine Learning** (March 2026 preprint). Controlled experiments report large Sharpe inflation from temporal, cross-sectional and validation leakage; this is treated as preprint evidence.
- Jo & Kim, **Rethinking Variable Importance in Machine Learning: An Economic Perspective on Empirical Asset Pricing**, Financial Analysts Journal 82(2), 2026. They emphasize out-of-sample economic evaluation rather than in-sample importance.

## Key methodological inference
A calendar date is not necessarily an information timestamp. Fundamentals, macro releases, earnings announcements, corporate actions and revised datasets can have publication, effective, revision and market-availability times that differ. A date-keyed join can therefore look leakage-safe while still using information unavailable at the decision timestamp.

## H138 — Timestamp fidelity test
If a candidate signal is genuine, enforcing exact point-in-time information availability should preserve most of its incremental net OOS utility. A material collapse after timestamp correction indicates that the apparent edge was at least partly an information-set artifact.

## Experimental protocol
1. Freeze candidate features and model/search budget before the audit.
2. Build two views: `date_only` and `point_in_time`.
3. For every feature record observation timestamp, publication/availability timestamp, effective period, revision/version ID, decision timestamp and earliest permissible trade timestamp.
4. Add explicit latency buffers when exact availability is uncertain.
5. Run identical purged/embargoed walk-forward folds on both views.
6. Emit an immutable ledger: `decision_ts -> feature_version -> prediction -> position -> execution_ts -> turnover -> gross_pnl -> commission -> spread -> slippage -> impact -> net_pnl`.
7. Apply 1x/1.5x/2x cost stress and execution-lag stress.
8. Compare against a strong baseline and timestamp-shuffled placebo.

## Promotion criterion
The point-in-time version must retain a pre-declared fraction of the date-only incremental net OOS utility and remain economically positive under base and stressed execution assumptions. The retention threshold must be fixed before results are observed.

## Failure criterion
A large performance collapse after timestamp correction is recorded as a leakage finding, not repaired by changing features, horizons or thresholds inside the same evaluation.

## Current project relevance
The README still identifies forward-label overlap at walk-forward boundaries as unresolved. Timestamp fidelity is a separate leakage channel and must be audited before older results are trusted.

## Status
Hypothesis proposed; no numerical result claimed.
