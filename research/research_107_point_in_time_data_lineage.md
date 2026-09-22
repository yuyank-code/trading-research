# Research 107 — Point-in-Time Data Lineage as a First-Class Backtest Input

Date: 2026-09-22

## Core finding

Recent 2026 research strengthens the case that temporal validity must be enforced at the data-generation layer, not merely by chronological train/test splits. Koijen & Levy (NBER 35431, July 2026) construct a real-time benchmark using only information available at the announcement timestamp and argue that historical AI backtests otherwise inherit look-ahead bias. Kelly, Malamud, Schwab & Xu (NBER 35247, May 2026) construct point-in-time language-model checkpoints and report positive out-of-sample economic performance under chronological information constraints.

A separate 2026 validation study (Kim, *Beyond Accuracy*, revised August 2026) reports that prediction-oriented validation can produce false positives and that transaction costs materially reduce net Sharpe. These results reinforce the need to audit the entire information path from raw source publication to feature availability to execution.

## Implication for this project

The existing repository correctly identifies forward-label overlap as a blocker for trusting older walk-forward results. The next step is to make point-in-time lineage machine-auditable for every feature family and every decision timestamp.

Required lineage fields:

- source identifier
- source publication/availability timestamp
- feature observation timestamp
- transformation timestamp
- decision timestamp
- maximum permissible lookback
- label start/end interval
- purge interval
- embargo interval
- execution timestamp

A feature is invalid if any dependency has an availability timestamp after the decision timestamp, even if its observation date appears historical.

## Testable consequence

Run the same candidate strategy through two pipelines: (A) ordinary historical data and (B) strict point-in-time reconstructed data. Any material degradation in B is evidence that the original workflow contained information-timing contamination or publication-revision effects.

## Promotion rule

No model may enter final OOS comparison unless all feature dependencies pass the point-in-time lineage audit and the forward-label purge/embargo test.

## Sources

- Koijen, R. S. J. & Levy, B., *Assessing the Benefits of Optimized Agentic AI Systems for Asset Pricing*, NBER Working Paper 35431, July 2026.
- Kelly, B. T., Malamud, S., Schwab, J. & Xu, T. A., *Scaling Point-in-Time Language Models*, NBER Working Paper 35247, May 2026.
- Kim, J., *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, SSRN 6508779, revised August 2026.
