# Research 65 — Null-Environment Falsification and Search Calibration

Date: 2026-09-20

## Key literature signal

Recent 2026 work on *Spurious Predictability in Financial Machine Learning* argues that adaptive specification search can generate statistically significant backtests even under martingale-difference nulls. The proposed remedy is a workflow-level falsification audit using synthetic zero-predictability reference classes and microstructure placebos, followed by quantification of selection-induced performance inflation on disjoint walk-forward realizations.

This is materially different from a feature-level leakage test. A pipeline can obey chronological information constraints and still manufacture a winner by searching enough correlated specifications, thresholds, model families, and research-design choices.

A separate 2026 empirical study of ML trading under transaction costs reports a disconnect between predictive metrics and net trading performance, with transaction-cost-aware filtering outperforming repeated architecture optimization in its Bitcoin experiments. This supports testing the entire decision workflow rather than optimizing prediction accuracy in isolation.

## New research direction

The project now adds a pre-promotion null-environment audit. The same search process used on real data should be run against deliberately non-predictive synthetic/reference data. Every trial remains in the immutable search ledger.

The central comparison is:

**real-data maximum/promoted performance** versus **null maximum/promoted performance**

using the same candidate universe, validation geometry, costs, execution rules, and multiplicity controls.

## Why this matters

Existing controls in the repository target look-ahead, label overlap, decision-time leakage, transaction costs, research-design sensitivity, seed instability, CPCV versus walk-forward geometry, and trial accounting. H115 adds a different layer: whether the *whole research workflow* is capable of manufacturing a false positive even when no predictive structure exists.

## Test protocol

- preserve realistic autocorrelation/volatility features in synthetic nulls where possible;
- include multiple independent seeds;
- run the complete search rather than a hand-picked subset;
- include placebo/microstructure decoupling tests;
- apply the production promotion gate unchanged;
- measure false-promotion rate and maximum-null performance;
- estimate selection inflation as optimized evidence minus independent OOS evidence.

## Current result

No numerical result is claimed yet. The repository still requires immutable candidate-level OOS prediction/return artifacts and corrected forward-label-overlap validation before historical model-performance numbers can be considered trustworthy.

## Sources

- Nikolopoulos, S. D. (2026), *Spurious Predictability in Financial Machine Learning*, alphaXiv/arXiv record, submitted 16 Apr 2026.
- Bysik, A. & Ślepaczuk, R. (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*, arXiv:2606.00060, submitted 19 May 2026.
- Lalwani, V., Meshram, V. & Jindal, V. (2025/2026), *Empirical Asset Pricing via Machine Learning: The Role of Research Design Choices*, European Financial Management.
