# Research 41 — Selection-Aware Null Calibration

Date: 2026-09-19
Status: protocol / pipeline hardening; no alpha claim

## Question

Can the trading research workflow distinguish genuine predictive structure from a strategy selected from a large adaptive search when the null environment has the same dependence structure, cost model, and research budget?

## Literature basis

Bailey & López de Prado (2014) formalize the Deflated Sharpe Ratio as a correction for multiple testing and non-normal returns. A 2024 controlled study found Combinatorial Purged Cross-Validation superior to conventional OOS procedures for reducing backtest-overfitting risk. A 2026 multi-market validation harness reports that even the best of tens of thousands of fully-costed strategies can fail DSR after accounting for selection. These results imply that a null must reproduce the *selection process*, not merely test one arbitrary strategy.

## Hypothesis H90

After controlling for the effective number of trials, a genuine signal should produce a stronger confirmation statistic than the best candidate produced by an equally sized search over a matched zero-alpha null. If the real-search winner is not separated from the null-search distribution, the result is not promoted.

## Protocol

1. Freeze the candidate-generation/search budget before confirmation.
2. Construct nulls that preserve chronology, volatility clustering and cross-sectional dependence where applicable, while destroying the hypothesized predictive relation.
3. Run the same candidate-generation procedure, model classes, hyperparameter budget, seed budget, purging/embargo, execution model and cost assumptions on the null.
4. Record the maximum and full distribution of net OOS performance from each null search.
5. Compute effective trial count from the correlation structure of candidate return series; do not equate nominal candidates with independent trials.
6. Apply DSR/PSR, PBO and SPA/Reality Check to the real search and null search.
7. Keep confirmation data untouched. No threshold, candidate, cost model or metric may be selected after confirmation results are observed.
8. Require robustness across realistic cost stress and major subperiods before promotion.

## Failure conditions

- Real-search winner falls inside the null winner distribution.
- Statistical significance disappears after trial-count correction.
- Performance depends on one seed, one metric, one cost assumption or one regime.
- Null search itself frequently generates apparently deployable Sharpe ratios.
- Any future-information fixture is not detected before performance evaluation.

## Expected value

This test combines the project's existing leakage, cost, seed, metric and research-DoF controls into one workflow-level falsification experiment. It is designed to answer whether the *research process* can manufacture alpha, rather than whether a single selected backtest looks good.

## Current conclusion

No empirical result is claimed in this document. The project remains blocked from model promotion until corrected forward-label-overlap validation and an immutable candidate-level OOS prediction/return matrix are available.

## Sources

- Bailey, D. H., & López de Prado, M. (2014), *The Deflated Sharpe Ratio*, Journal of Portfolio Management, 40(5), 94–107. DOI: 10.3905/jpm.2014.40.5.094.
- Arian, H., Norouzi Mobarekeh, D., & Seco, L. (2024), *Backtest overfitting in the machine learning era: A comparison of out-of-sample testing methods in a synthetic controlled environment*, Knowledge-Based Systems 305, 112477. DOI: 10.1016/j.knosys.2024.112477.
- Gatto, D. V. (2026), *Backtest Overfitting and the Deflated Sharpe Ratio: A Multi-Market Validation Harness*, working paper.
