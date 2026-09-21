# Research 90 — Real-Time Benchmarking and Selection-Aware Validation

Date: 2026-09-21

## Question
Can the project distinguish genuine economic predictability from gains created by adaptive research choices and retrospective information?

## Literature

- Koijen & Levy (NBER Working Paper 35431, July 2026), *Assessing the Benefits of Optimized Agentic AI Systems for Asset Pricing*: constructs a real-time OOS benchmark using only information available at announcement time and explicitly highlights look-ahead bias and market reflexivity.
- Lalwani, Meshram & Jindal (European Financial Management, 2026), *Empirical Asset Pricing via Machine Learning: The Role of Research Design Choices*: evaluates 5,376 ML portfolios and finds research-design choices can create substantial dispersion in performance; transaction costs do not eliminate the importance of design choices.
- Arian, Norouzi Mobarekeh & Seco (Knowledge-Based Systems, 2024), *Backtest overfitting in the machine learning era*: controlled synthetic experiments find combinatorial purged cross-validation reduces overfitting risk relative to conventional validation, using PBO and DSR diagnostics.
- Bysik & Ślepaczuk (2026 preprint), *Machine Learning-Based Bitcoin Trading Under Transaction Costs*: 27-fold walk-forward tests show naive sign trading can fail at 10 bps while cost-aware forecast thresholds reduce turnover; formal dominance of XGBoost over neural alternatives is not established.
- Mroziewicz & Ślepaczuk (2026 preprint), *A novel approach to trading strategy parameter optimization using double out-of-sample data and walk-forward techniques*: emphasizes a final unseen period and cost sensitivity rather than relying on a single optimized backtest.
- Nikolopoulos (2026 preprint), *Spurious Predictability in Financial Machine Learning*: proposes falsification against zero-predictability and microstructure placebo environments to detect selection-induced significance.

## Synthesis

The strongest common point is not that one model family wins. It is that the research process itself is a source of statistical risk. The project therefore needs an explicit separation between (1) model estimation, (2) research selection, and (3) final deployment evidence.

## Pipeline change

For every promoted candidate, retain a trial ledger containing model family, feature set, training window, fold design, cost model, execution rule, seed, and selection metric. The final OOS set must be inaccessible to selection decisions. Timestamp provenance must be retained as observation_ts, publication_ts/revision, decision_ts and earliest_trade_ts where applicable.

## Falsification requirements

1. Run a zero-predictability synthetic benchmark through the complete research harness.
2. Run a label-shuffled placebo with identical search budget.
3. Compare date-keyed and exact timestamp-keyed information sets.
4. Apply purging/embargo and, where appropriate, CPCV/DSR/PBO diagnostics.
5. Report net OOS performance under base, 1.5x and 2x cost assumptions.
6. Report the distribution across stochastic seeds instead of best-seed performance.

## Interpretation

A positive result that disappears in either placebo, exact-timestamp, or cost-stress testing is not promoted. A candidate must demonstrate incremental net OOS utility against the strong baseline while surviving the selection audit.

## Status

This research pass identifies a concrete validation architecture; it does not establish alpha. Historical results remain provisional until the repository's previously identified forward-label-overlap issue is corrected and the immutable prediction-to-execution ledger exists.
