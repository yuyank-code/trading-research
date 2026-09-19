# H86 — Research-Degrees-of-Freedom Audit

## Question
Can an explicit, immutable accounting of researcher degrees of freedom materially reduce false promotion of trading candidates compared with ordinary OOS reporting?

## Motivation
Recent financial-ML validation work shows that AUC/accuracy-based evaluation can have high false-positive rates, while CPCV/PBO/DSR can reject apparently successful variants. Recent AlphaAudit work also frames strategy evaluation as an audit problem: leakage and multiple testing can make large strategy corpora look convincing unless the verifier is frozen before the candidates are scored.

## Hypothesis
H86 passes only if candidate promotion remains stable after explicitly accounting for all material search dimensions: model family, features, labels/horizons, universe, hyperparameters, holding period, threshold, cost model, execution rule, and benchmark.

## Pre-registered protocol
1. Create a candidate ledger before confirmation containing a unique candidate ID and every degree of freedom explored.
2. Freeze the confirmation dataset and evaluator before candidate confirmation begins.
3. Count the effective search family and preserve failed candidates.
4. Run purged/embargoed OOS evaluation with point-in-time features and corrected forward-label boundaries.
5. Apply realistic spread, slippage, impact, borrow and capacity assumptions where applicable.
6. Compare net performance with frozen simple benchmarks.
7. Apply DSR/PBO and SPA/Reality Check; report MCS membership where feasible.
8. Run matched-count placebo/null candidates through the identical evaluator.
9. Do not allow confirmation results to modify any specification.

## Promotion gate
A candidate cannot be promoted merely because it has positive net return or a high Sharpe. It must remain economically superior to the benchmark under the frozen evaluator, survive the multiple-testing controls, and avoid material degradation across confirmation subperiods and adverse cost scenarios.

## Failure conditions
- Missing search-history entries.
- Any confirmation-driven tuning.
- Feature availability ambiguity.
- Label overlap across train/validation/confirmation.
- Survivorship or universe hindsight.
- Candidate wins only before costs.
- Candidate loses to placebo-adjusted null controls.
- Candidate conclusion changes materially under the pre-registered cost family.

## Status
Design only. No empirical pass until the immutable candidate-level OOS prediction/return matrix and corrected forward-label validation are available.
