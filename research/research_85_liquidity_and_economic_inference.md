# Research 85 — Liquidity Constraints and Economic Inference

## Motivation

Recent evidence shows that ML portfolio results can be distorted by economically hard-to-trade observations. Jo & Kim (Financial Analysts Journal, 2026) find that in-sample variable importance is unreliable, microcaps can dominate reported returns while concentrating gains in costly-to-trade stocks, and economic restrictions materially improve inference.

A separate 2026 validation framework for crypto trading reports a statistical/economic disconnect: strategies can pass statistical tests while failing combinatorial purged validation or becoming uneconomic after transaction costs. A 2026 deep-learning benchmark likewise reports breakeven transaction costs and downside risk alongside Sharpe, rather than treating predictive or gross-return metrics as sufficient.

## Research implication

Liquidity should be treated as an explicit part of the data-generating and execution problem, not merely as a post-hoc cost adjustment. A model that only works in the least liquid tail is not equivalent to one that works in a tradable universe.

## Proposed pipeline change

Every candidate OOS row should carry a point-in-time liquidity state, including where available:

- dollar volume / ADV;
- price;
- spread proxy or observed spread;
- turnover;
- estimated participation rate;
- capacity bucket.

Universe eligibility and cost parameters must be determined using information available before execution. No full-sample liquidity percentile may be used.

## Evaluation

For every candidate, report:

1. full universe;
2. liquidity-constrained universe;
3. matched liquidity-weighted benchmark;
4. lowest-liquidity decile separately;
5. incremental net performance after liquidity-conditioned costs;
6. breakeven cost and turnover by liquidity bucket.

A result that disappears after the pre-specified tradability filter is applied is classified as a liquidity artifact, not robust alpha.

## Sources

- Jo, Y. & Kim, Y. H. (2026), *Rethinking Variable Importance in Machine Learning: An Economic Perspective on Empirical Asset Pricing*, Financial Analysts Journal 82(2), 92–135. DOI: 10.1080/0015198X.2026.2621646.
- Kim, J. (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, SSRN 6508779, revised Aug. 3, 2026.
- Saly-Kaufmann, A. et al. (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*, arXiv:2603.01820.
