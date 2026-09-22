# Run 12 — Decision-Time Audit and Current Execution Blocker

Date: 2026-09-23

## Meaningful progress

A fresh literature and repository audit produced one concrete methodological upgrade: decision-time leakage is now treated as a **one-switch experimental variable**, rather than only as a static checklist item.

The connected `bitcoin-ml-trading/production_research.py` engine currently has a six-bar forward label, six-bar fold purge, next-bar execution, deterministic cost stress, and intrabar ambiguity logging. However, its trading simulator still monetizes a next-bar path while the supervised target is a six-bar forward-close event. The repository's own Run 11 finding already identifies this horizon/target mismatch as unresolved.

## New literature evidence

Zhang et al. (2026), *When Alpha Disappears: A One-Switch Benchmark for Decision-Time Leakage in Financial Backtests*, introduces a paired protocol that changes exactly one evaluation convention while freezing the data, model, folds, horizon, portfolio rule, and cost convention. Across daily equity panels and six model families, centered temporal features and same-day-open execution with post-open information produced large, stable metric inflation, while several other convention changes had much weaker effects. The paper is diagnostic rather than evidence of tradable alpha.

Koijen & Levy (NBER 2026) likewise argue that historical AI backtests suffer look-ahead when models use information that was unavailable at the historical decision time, and propose real-time benchmarks using only contemporaneously available information.

Bysik & Ślepaczuk (2026) provide complementary execution evidence in hourly BTC: naive sign strategies fail under tested 10-bps costs, while cost-aware forecast filtering can rescue selected configurations; however, their bootstrap tests do not establish formal dominance of XGBoost over neural alternatives.

The combined implication is that **decision-time validity and economic conversion must be tested before architecture ranking**.

## H135

Register a one-switch audit that freezes the candidate model and changes only the decision-time/execution convention. Measure the change in both prediction metrics and paired net OOS utility. A material unexplained drop is evidence that the original convention was contaminating the result.

## Current verdict

No profitability claim is promoted. The connected repository still lacks `outputs/final_model_report.json` in the expected path, so the complete immutable candidate-level OOS artifact cannot yet be recomputed from the repository alone. The correct state remains **BLOCKED**, not NEGATIVE and not PROMOTED.

Next decisive execution: generate the immutable prediction-to-execution artifact, then run H135 alongside the existing horizon-invariance, cost-stress, intrabar-bound, seed, and search-aware tests.
