# Research 114 — Information Value Before Model Complexity

## Date
2026-09-23

## Objective
Reassess whether the next unit of research effort should go into model architecture or into proving that the available information actually contains economically useful signal after costs.

## New literature evidence

1. Bysik & Ślepaczuk (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs*: across roughly 70,000 hourly BTC-USDT observations and 27 walk-forward folds, naive sign trading failed under a 10 bp cost assumption; a cost-aware forecast-magnitude filter reduced turnover and restored profitability in selected configurations. XGBoost was descriptively strongest, but bootstrap evidence did not establish formal dominance.

2. Kim (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*: the study reports that transaction costs consumed 55–91% of gross alpha across its strategy variants and that AUC-only validation produced false positives in Monte Carlo tests. This supports treating economic utility and falsification as primary gates rather than predictive accuracy.

3. Gençay (2026), *What survives honest evaluation?*: structural leakage controls and search-trial accounting were necessary even when Deflated Sharpe and PBO-style corrections were applied. A deliberately leaky oracle could survive statistical correction, showing that multiplicity adjustment cannot repair invalid information sets.

4. Lalwani, Meshram & Jindal (2025/2026), *Empirical Asset Pricing via Machine Learning: The Role of Research Design Choices*: across 5,376 portfolios, research-design choices generated large dispersion in reported strategy returns. This makes pipeline design itself an experimental factor.

5. Pardo (2026), *On the Limits of Low-Frequency OHLCV Signals...*: a leak-free, cost-aware benchmark found that an ML optimizer only marginally improved a no-ML baseline while incurring materially higher cumulative transaction costs; an equal-weight baseline was nearly as strong. This is a strong warning against assuming predictive complexity creates economic value.

## Synthesis

The evidence now supports a stronger ordering principle:

> First establish incremental information value under a frozen economic pipeline; only then spend search budget on additional model complexity.

This is not an anti-ML conclusion. The large-scale futures benchmark and VAE-ER work provide evidence that structured temporal representations and economically motivated restrictions can improve OOS results. But those gains are useful only if they survive the same PIT, search, cost, seed, and baseline controls.

## Pipeline implication

The project should separate two questions:

A. **Information test:** does the feature set add stable, cost-adjusted incremental utility over a frozen baseline?

B. **Architecture test:** conditional on A passing, does a more complex model extract more of that information than a regularized/simple model under the same search budget?

This prevents architecture selection from being used to compensate for weak information content.

## Status
No new alpha claim is made. Historical candidate results remain untrusted until the repository's PIT and label-overlap requirements are satisfied.
