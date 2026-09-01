# Validation & Overfitting Update — 2026-09-01

## Meaningful literature update

The strongest new result from this research pass is methodological rather than a new trading edge: **the project should treat the entire research search history as part of the statistical evidence.**

Bailey & López de Prado's Deflated Sharpe Ratio explicitly corrects performance inflation from multiple testing and non-normal returns. Their central warning is directly applicable to a model-selection pipeline that evaluates many features, models, thresholds and trading rules. [Bailey & López de Prado, 2014 — Journal of Portfolio Management](https://doi.org/10.3905/jpm.2014.40.5.094).

Recent work reinforces this. A 2026 study of LLM-driven strategy discovery makes the search process itself auditable and reports that leakage-safe constraints and trial-count-aware evaluation are both necessary; in its experiments, discovered strategies failed honest OOS certification while passive benchmarks survived. This is especially relevant to our project because our research process is also capable of generating many candidate specifications.

## New project rule: trial registry

Every candidate experiment must be logged, including failures. The registry should contain at minimum:

- experiment ID
- timestamp
- dataset/version
- information set
- feature family
- model family
- hyperparameters
- label horizon
- training/validation/OOS periods
- cost assumptions
- selection criterion
- result metrics
- whether the candidate was selected for further testing
- reason for rejection

The number of tested candidates must be available when calculating post-selection statistics.

## New hypothesis H9 — search-aware validation

> A candidate strategy that appears strong before accounting for the number of specifications searched will lose a material portion of its evidential strength after DSR/PBO-style correction.

### Test

1. Register every model/feature/threshold/cost configuration.
2. Select candidates only from a designated development period.
3. Freeze the final specification.
4. Run exactly once on a locked OOS period.
5. Calculate raw Sharpe and other economic metrics.
6. Calculate Deflated Sharpe Ratio using the documented trial count and return distribution.
7. Estimate Probability of Backtest Overfitting using an appropriate combinatorial/partition procedure where sample size permits.
8. Report both raw and corrected results.

## Purging and embargo

The project already recognizes that forward-return labels can overlap the test boundary. Purging must therefore operate on **label/event intervals**, not simply on row counts. An embargo should be considered where nearby observations may remain correlated after direct label-overlap removal.

A current open-source implementation of purged/embargoed and combinatorial purged CV provides a useful engineering reference, but we should implement and test our own validation layer rather than blindly depend on an external package.

## Complexity finding

The literature does not support a blanket rule that simpler models are always better. NBER research on factor pricing finds settings where very high-dimensional models outperform simpler alternatives out of sample. Therefore the project's complexity policy remains:

> Complexity is permitted, but only incremental OOS evidence earns it a place in the final model.

This means Ridge, tree ensembles, boosting and neural/sequence models should all be compared against strong simple baselines under identical information and cost assumptions.

## Pipeline changes required

### P0 — mandatory

- Add a persistent experiment/trial registry.
- Record failed candidates, not only winners.
- Freeze a final OOS period before model selection.
- Add DSR calculation to the final research report.
- Add a PBO/CPCV research module where computationally feasible.

### P1 — high value

- Make purge duration derive from the actual label horizon.
- Add explicit embargo configuration.
- Record the maximum feature lookback and execution delay in each experiment.
- Add stress tests across multiple transaction-cost assumptions.

### P2 — later

- Regime-conditional robustness reports.
- Cross-asset replication.
- Capacity/market-impact modeling.

## Current status

**No new trading edge is claimed in this update.** The meaningful finding is that the research pipeline itself needs search-aware statistical accounting before any model winner can be promoted. This is now a formal validation requirement for the project.

## Sources

- Bailey, D. H. & López de Prado, M. (2014). *The Deflated Sharpe Ratio: Correcting for Selection Bias, Backtest Overfitting, and Non-Normality*. Journal of Portfolio Management 40(5), 94–107. https://doi.org/10.3905/jpm.2014.40.5.094
- Gençay, E. (2026). *What survives honest evaluation? Leakage-safe, search-aware assessment of LLM-driven trading strategy discovery*. arXiv:2608.27734.
- Didisheim, A., Ke, S., Kelly, B. T. & Malamud, S. (2023). *Complexity in Factor Pricing Models*. NBER Working Paper 31689. https://www.nber.org/papers/w31689
