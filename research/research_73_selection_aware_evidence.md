# Research 73 — Selection-Aware Evidence and Immutable OOS Accounting

## Question

What minimum evidence is required to distinguish a genuinely incremental trading signal from a selected backtest winner?

## Literature

- Bailey & López de Prado (2014), *The Deflated Sharpe Ratio*: repeated strategy search inflates the apparent Sharpe of the selected winner; inference must account for selection bias and non-normal returns. DOI: 10.3905/jpm.2014.40.5.094.
- Kim (2026), *Beyond Accuracy*: reports that conventional predictive validation can produce false positives and that transaction costs can consume a large fraction of gross trading alpha across cryptocurrency strategy variants. This is a preprint/posted-content result and is treated as hypothesis-generating, not established universal evidence.
- Jo & Kim (2026), *Rethinking Variable Importance in Machine Learning*: in-sample variable importance is unreliable; microcap exposure can inflate apparent ML returns; economic restrictions and OOS evaluation materially change inference.
- Bengoechea Pardo (2026), SSRN 6952859: a leak-free, cost-aware large-cap equity benchmark reports that a promoted ML model only marginally beat a no-ML baseline while incurring materially higher transaction costs. This is a useful negative benchmark for incremental-value testing.

## New hypothesis H124

A candidate that appears superior before selection adjustment will frequently lose its apparent advantage when the complete trial history, paired OOS comparison, realistic cost stress and frozen-baseline attribution are all included.

## Test

For each candidate and strongest frozen baseline:

1. freeze the candidate before final-holdout access;
2. emit one immutable row per OOS decision using the project OOS Evaluation Contract;
3. compute paired net-return differences on identical timestamps;
4. repeat under baseline, 1.5x and 2x costs;
5. run liquidity-conditioned costs where supported;
6. preserve all candidate trials, including failures;
7. apply selection-aware inference using the complete trial registry;
8. report predefined regime/subperiod stability and seed dispersion.

## Promotion criterion

Promotion requires positive incremental net OOS utility versus the strongest frozen baseline, survival under cost stress, no leakage/label-overlap violations, and selection-adjusted evidence. A candidate that only beats a weak baseline or only works at one cost assumption is not promoted.

## Important distinction

Missing OOS artifacts produce `BLOCKED`, not `NEGATIVE`. A negative result requires an executable, leakage-clean comparison with complete cost accounting. This prevents both false positives and false negatives caused by incomplete evaluation.

## Status

The repository currently lacks the candidate-level immutable OOS return matrix required for execution of H124. The new contract is therefore the next implementation gate rather than evidence of model performance.
