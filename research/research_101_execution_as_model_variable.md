# Research 101 — Execution as a Model Variable

Date: 2026-09-22

## Question

Can an execution-aware decision layer improve net trading utility more robustly than improving the return forecaster itself?

## Literature

- McAuliffe et al. (2026), *Model Predictive Control For Trade Execution*, arXiv:2603.28898. The paper frames execution as a constrained control problem balancing completion, market impact and opportunity cost. Using NASDAQ level-3 data and simulated orders, it reports roughly 40–50% lower schedule shortfall than spread-crossing benchmarks. This is promising but remains simulation-based evidence and should not be treated as portable alpha.
- Kim (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, SSRN 6508779. Across 340 variants, the paper emphasizes the statistical/economic disconnect and shows that transaction costs can eliminate apparently strong gross performance. This supports making execution a first-class research object.
- Bysik & Ślepaczuk (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs*, arXiv:2606.00060. Their walk-forward study finds naive sign trading fails under 10-bps costs in selected settings, while a cost-aware execution threshold can reduce turnover and recover performance in selected configurations. Bootstrap tests did not establish formal dominance of XGBoost over neural alternatives.
- Lalwani et al. (2026), *Empirical Asset Pricing via Machine Learning: The Role of Research Design Choices*, European Financial Management. Across 5,376 portfolios, research-design choices produce large dispersion in reported performance. This motivates freezing the execution rule before final OOS.

## Research interpretation

The useful hypothesis is not that MPC itself creates alpha. The testable claim is narrower: when the same forecast is converted to positions, an execution-aware controller may preserve more of the forecast's economic value than a static execution rule, after realistic costs and under adverse liquidity conditions.

## Falsification requirements

A controller is not promoted if its benefit disappears under modest cost stress, if it only works in one liquidity regime, if it requires post-decision information, or if adaptive execution is re-optimized separately on each stress scenario.

## Status

Literature-backed hypothesis/protocol. No numerical OOS result is claimed from this research pass because the project's corrected walk-forward/forward-label-overlap validation gate remains a prerequisite for historical model promotion.
