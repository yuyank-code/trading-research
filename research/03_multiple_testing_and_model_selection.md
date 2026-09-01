# Multiple Testing, Model Selection, and the Next Validation Gate

Date: 2026-09-01

## New literature reviewed

### Bailey & López de Prado (2014) — Deflated Sharpe Ratio

The Deflated Sharpe Ratio (DSR) was developed to correct observed Sharpe ratios for selection bias from multiple trials and for non-normal return distributions. The central implication for this project is that the best result in a large model/feature/threshold search cannot be interpreted using its raw Sharpe alone. The number and dependence structure of trials must be part of the evidence.

Source: https://doi.org/10.3905/jpm.2014.40.5.094

### Bailey, Borwein, López de Prado & Zhu (2017) — Probability of Backtest Overfitting

The authors propose combinatorially symmetric cross-validation (CSCV) to estimate the probability that an investment backtest is overfit. They emphasize that ordinary holdout logic can be inadequate for strategy selection because repeated model/search decisions create a selection problem.

Source: https://doi.org/10.21314/JCF.2016.322

### Bailey, Borwein, López de Prado & Zhu (2014) — Pseudo-Mathematics and Financial Charlatanism

This work demonstrates how high simulated performance can arise after testing relatively small numbers of alternative configurations. The practical lesson is to record the complete research/search history, including unsuccessful alternatives, instead of reporting only the final winner.

Source: https://doi.org/10.1090/noti1105

### Hansen (2005) — Superior Predictive Ability

Hansen's Superior Predictive Ability framework provides another way to evaluate whether a candidate model is genuinely better than a benchmark after accounting for data snooping. It is useful as a complementary statistical gate rather than relying on a single Sharpe-based metric.

Reference: Hansen, P. R. (2005), *A Test for Superior Predictive Ability*, Journal of Business & Economic Statistics, 23, 365–380.

### Hsu, Hsu & Kuan (2010) — Stepwise SPA

The stepwise SPA procedure extends the SPA framework to identify useful models under large-scale testing while controlling data-snooping concerns. Their empirical application also illustrates that apparent technical predictability can weaken when the market environment changes.

Source: https://ideas.repec.org/a/eee/empfin/v17y2010i3p471-484.html

## Implications for our trading project

The current project has already tested or planned many dimensions: model family, feature group, probability threshold, signal rules, costs, and trading-frequency limits. Treating each choice independently would understate the effective research count.

Therefore:

1. Every experiment must receive a unique trial ID.
2. The registry must record the hypothesis, data period, feature set, model, hyperparameters, threshold, cost assumptions, and OOS windows.
3. Failed experiments remain in the registry.
4. The final candidate cannot be selected from the untouched final test set.
5. The final test must be evaluated only after the selection process is frozen.
6. DSR/PBO/SPA-style diagnostics must be reported alongside raw performance.
7. Correlated trials should not automatically be counted as independent trials; effective trial count should be estimated where practical.

## New testable hypotheses

### H9 — Incremental nonlinear value

After controlling for a strong linear baseline, do tree/boosting models improve truly OOS predictive loss and net trading performance enough to justify their additional search degrees of freedom?

**Test:** frozen linear baseline vs pre-registered nonlinear candidates, using the same purged walk-forward windows and costs.

### H10 — Economic superiority rather than Sharpe superiority

Does the model selected on predictive loss remain superior after converting predictions into a cost-aware trading policy?

**Test:** compare log loss/Brier/AUC selection against net PnL/utility selection, while keeping the final OOS set untouched.

### H11 — Search-adjusted superiority

Does the best candidate remain statistically credible after accounting for the full trial registry?

**Test:** DSR plus PBO/CSCV and, where feasible, SPA against the strongest baseline.

### H12 — Threshold robustness

Does performance remain economically useful across a neighborhood of probability thresholds rather than at one isolated optimum?

**Test:** freeze threshold on training/validation windows, then examine adjacent thresholds only on the final untouched OOS report.

## Pipeline changes required

### Event-aware purging

For a label based on a forward horizon H, training observations whose label interval overlaps the test interval must be excluded. A simple fixed-row purge is acceptable only when the event duration is fixed and the data are regular. The implementation should move toward explicit event start/end timestamps.

### Embargo

After the purge, an embargo should be applied when nearby observations can still transmit dependence through overlapping information, execution windows, or serial correlation. The embargo duration must be pre-specified rather than optimized on OOS performance.

### Search ledger

Every candidate run should produce a machine-readable record. Suggested fields:

- trial_id
- parent_hypothesis
- data_version
- feature_version
- model_family
- hyperparameters
- threshold
- training_window
- validation_window
- test_window
- purge_horizon
- embargo
- fee_bps
- slippage_bps
- turnover
- trades
- net_return
- Sharpe
- drawdown
- predictive metrics
- rejection/selection reason

## Robust finding from this research pass

The most important result is methodological rather than a new alpha signal: **the project's model-selection evidence is only as credible as its accounting for the search process.** A high raw OOS Sharpe is not enough if the OOS period influenced threshold/model selection or if dozens of alternatives were searched before selecting the reported model.

This means expanding the candidate-model search should temporarily be deprioritized. The next highest-value engineering task is to make the trial registry, event-aware purge/embargo, and search-adjusted evaluation executable and reproducible.

## Current conclusion

No new model is promoted by this literature review. The project remains in research/validation mode. The next model results should be reported only after passing the stricter search-aware validation protocol.
