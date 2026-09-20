# Research 70 — Design-Perturbation Stability and Selection Risk

**Date:** 2026-09-21  
**Hypothesis:** H121

## Literature synthesis

### Lalwani et al. (2025/2026), European Financial Management

The study evaluates 5,376 ML portfolios across multiple research-design choices and seven ML models. It reports substantial return variation attributable to choices such as training-window length, data filters and portfolio construction. The reported nonstandard errors can be several times conventional standard errors, and roughly one-third of portfolios remain significant after transaction costs. The direct implication is that a single favorable design should not be treated as evidence of model robustness.

### Kim (2026), VALID

Across 340 cryptocurrency strategy variants, the paper reports that statistical validation can disagree with economic usefulness. A strategy may pass a permutation test yet fail combinatorial purged cross-validation or economic gates, while higher trading frequency worsens net Sharpe. This supports fixing economic and validation gates before model selection.

### Saly-Kaufmann et al. (2026), large-scale deep-learning benchmark

The benchmark evaluates daily futures models from 2010–2025 using OOS risk-adjusted performance, significance, downside/tail risk, break-even transaction costs, random-seed robustness and computational efficiency. This provides a useful template for separating architecture quality from deployment robustness.

### Bysik & Ślepaczuk (2026), BTC walk-forward study

The study reports that naive sign-based ML strategies lose economics under a 10-bps transaction-cost assumption, while a cost-aware forecast threshold can reduce turnover and recover profitability in selected configurations. Its XGBoost-versus-neural ranking is descriptive rather than formally dominant. This reinforces the need to stress execution assumptions rather than optimize only forecast quality.

## New implication

The project should measure **research-design elasticity** explicitly. If a candidate's advantage exists only under one training window, rebalance interval, liquidity filter, or execution lag, the evidence is fragile even when the baseline backtest looks strong.

## Protocol added as H121

Use a frozen candidate and evaluate a pre-specified perturbation grid without reselecting on final OOS:

- training history: shorter / baseline / longer;
- rebalance: baseline / slower;
- portfolio construction: baseline / risk-scaled or capped;
- liquidity floor: baseline / stricter;
- execution lag: baseline / +1 bar;
- cost: flat / liquidity-conditioned / 1.5x variable cost.

The final OOS period is never used to choose the perturbation that looks best.

## Decision statistics

Primary: fraction of perturbations with positive incremental net OOS utility versus the frozen baseline.

Secondary: median and worst-case incremental utility, candidate-rank correlation, turnover, gross-to-net decay, drawdown, tail loss, break-even cost, and seed dispersion.

A candidate that wins only the baseline specification is classified as fragile rather than promoted.

## Current limitation

The repository does not yet contain the immutable candidate-level OOS prediction/position/realized-return/cost matrix required to execute H121 numerically. Forward-label-overlap correction also remains a prerequisite for trusting earlier walk-forward results.

## Sources

- Lalwani, V. et al. (2026), *Empirical Asset Pricing via Machine Learning: The Role of Research Design Choices*, European Financial Management, DOI: 10.1111/eufm.70033.
- Kim, J. (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, SSRN 6508779.
- Saly-Kaufmann, A., Wood, K., Calliess, J.P. & Zohren, S. (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*, arXiv:2603.01820.
- Bysik, A. & Ślepaczuk, R. (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*, arXiv:2606.00060.
