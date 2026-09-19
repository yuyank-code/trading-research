# Research 38 — Seed Stability and Training-Path Dependence

Date: 2026-09-19

## Executive summary

A new robustness layer is added: stochastic training choices must not become an unrecorded route to selecting a trading model. Recent 2026 financial time-series benchmarking explicitly includes robustness to random seed selection alongside OOS risk-adjusted performance, downside/tail risk, break-even transaction costs and computational efficiency. The benchmark also reports that model families can rank differently depending on the economic evaluation rather than ordinary forecasting metrics.

The project's implication is narrower and testable: once a candidate specification is frozen, random initialization and training-order variation should be treated as controlled nuisance variation. The best seed must never be selected after seeing confirmation results.

## Evidence reviewed

1. **Saly-Kaufmann, Wood, Calliess & Zohren (2026), Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance.** Evaluates linear, recurrent, transformer, state-space and sequence-representation models on daily futures from 2010–2025, reporting statistical significance, downside/tail risk, break-even transaction costs, random-seed robustness and computational efficiency. The paper is directly relevant to the project's evaluation stack.
2. **Kim (2026), Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading.** Reports that conventional predictive validation can generate high false-positive rates and argues for fixed-order statistical/economic validation with CPCV, PBO and DSR. This supports keeping seed analysis subordinate to the broader leakage and multiple-testing framework.
3. **Arian, Norouzi Mobarekeh & Seco (2024), Backtest overfitting in the machine learning era.** Controlled synthetic experiments report CPCV as superior to conventional OOS procedures for reducing overfitting risk, reinforcing the need to combine seed analysis with purging/embargo and post-selection controls rather than treating seed averaging as evidence by itself.
4. **Bysik & Ślepaczuk (2026), Machine Learning-Based Bitcoin Trading Under Transaction Costs.** Walk-forward experiments show that gross profitability can disappear at realistic costs and that cost-aware execution filters can alter results substantially without establishing formal model dominance. This motivates running every seed through the same execution model.

## New pipeline change: H87

For each frozen candidate, the project will run ten pre-registered seeds: 7, 19, 31, 43, 59, 71, 83, 97, 109 and 127.

For each seed, preserve:

- fold-local training state;
- OOS predictions;
- gross and net returns;
- turnover;
- drawdown/tail metrics;
- break-even transaction cost;
- model artifact hash;
- software/data manifest.

Primary reporting is the pre-registered seed aggregate plus worst-seed result. Best-seed selection is prohibited.

## Required controls

Seed robustness is evaluated only after the candidate's causal data construction and corrected forward-label-overlap handling are in place. It does not replace:

- purged/embargoed OOS validation;
- point-in-time data checks;
- realistic costs, slippage and impact;
- benchmark-relative value;
- DSR/PBO;
- SPA/Reality Check;
- MCS;
- matched-count placebo/null controls;
- capacity stress;
- metric-invariance analysis;
- research-degrees-of-freedom accounting.

## Important limitation

This pass does not claim that any candidate has passed H87. The repository still does not contain the immutable candidate-level OOS prediction/return matrix required for trustworthy model promotion, and the known forward-label-overlap validation defect remains a prerequisite to numerical conclusions.

## Sources

- https://arxiv.org/abs/2603.01820
- https://doi.org/10.1016/j.knosys.2024.112477
- https://doi.org/10.2139/ssrn.6508779
- https://arxiv.org/abs/2606.00060
