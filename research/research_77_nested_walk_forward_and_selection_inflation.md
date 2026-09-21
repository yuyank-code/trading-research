# Research 77 — Nested Walk-Forward Selection and Selection Inflation

Date: 2026-09-21

## Executive finding

Walk-forward window length is itself a hyperparameter. If many window lengths are compared and the best one is selected using the same data later used to report performance, the evaluation acquires another hidden multiple-testing channel. The appropriate response is nested walk-forward evaluation, with window selection confined to an inner layer and a completely untouched outer test.

## New literature

Mroziewicz and Ślepaczuk (2026), *A Novel Approach to Trading Strategy Parameter Optimization, using Double Out-of-Sample Data and Walk-Forward Techniques*, evaluates 81 combinations of walk-forward window lengths on intraday crypto data and explicitly emphasizes single-time unseen testing. The key methodological implication for this project is not that any one window is universally best; it is that the choice of window can materially affect reported results and therefore must be treated as a research choice rather than a harmless implementation detail.

Lalwani et al. (European Financial Management, 2026) study 5,376 ML portfolios and show that research-design choices such as training-window length, filtering and portfolio construction create large return dispersion. This supports treating window selection as part of the model-selection/search process.

Kim (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, reports substantial false-positive rates for prediction-only validation and shows that CPCV/PBO and economic gates eliminate apparently successful variants. This supports applying selection-aware inference to window searches as well as model searches.

Nikolopoulos (2026), *Spurious Predictability in Financial Machine Learning*, argues that complete adaptive research workflows can generate significant results under zero-predictability nulls and proposes falsification audits using synthetic nulls and microstructure placebos. This motivates a matched-budget null search for window selection.

## Test design

The project should compare fixed, adaptive single-layer, nested adaptive, and matched-noise window selection under the same outer test blocks. All costs and execution assumptions remain identical. The outer test is never used to choose a window, threshold, model or cost parameter.

## Expected interpretation

If single-layer adaptive selection outperforms the fixed baseline but nested selection does not, the apparent gain should be classified as selection inflation. If nested selection retains positive incremental net utility after realistic costs and multiple-testing correction, window adaptation becomes a credible candidate mechanism for further research.

## Status

Hypothesis H128 added. Numerical validation remains pending until the repository contains the executable immutable OOS prediction-to-cost artifact and corrected label-overlap handling.

## Sources

- Mroziewicz & Ślepaczuk (2026), SSRN/arXiv 2602.10785.
- Lalwani et al. (2026), European Financial Management, DOI 10.1111/eufm.70033.
- Kim (2026), SSRN 6508779.
- Nikolopoulos (2026), arXiv/alphaXiv 2604.15531.
