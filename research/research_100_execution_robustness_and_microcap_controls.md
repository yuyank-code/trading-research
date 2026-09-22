# Research 100 — Execution Robustness and Economic Universe Controls

Date: 2026-09-22

## Core finding

Recent 2026 evidence strengthens two pipeline requirements: economic evaluation must dominate in-sample feature importance, and the tradable universe itself is a model assumption. Jo & Kim (Financial Analysts Journal, 2026) report that in-sample variable importance overfits, while microcaps can inflate ML portfolio returns and concentrate gains in costly-to-trade names. Their conclusion is that liquidity and risk signals deserve explicit economic treatment and that microcap exclusions materially affect inference.

A 2026 large-scale futures benchmark likewise evaluates models using out-of-sample risk-adjusted performance, downside/tail risk, breakeven transaction costs, seed robustness, and computational efficiency. Separately, 2026 BTC walk-forward work finds that naive sign trading fails under 10 bps costs while cost-aware execution filtering can materially change the result; model ranking was not statistically decisive.

## Implication for this project

A strategy cannot be promoted on a single universe and a single cost assumption. Universe construction and execution assumptions must be treated as first-class experimental factors and recorded before model selection.

## Required controls

1. Freeze the tradable universe using only information available at each decision date.
2. Report results for the baseline universe and a liquidity-filtered universe.
3. Report gross, net, turnover, average holding period, and breakeven cost.
4. Stress spread/slippage/impact at 1x, 1.5x, and 2x the base assumption.
5. Report results by liquidity bucket and by regime.
6. Keep model ranking fixed from the validation layer; do not re-select a model separately for each cost scenario.
7. Treat microcap/execution-sensitive outperformance as suspect until it survives liquidity and cost controls.

## Literature

- Jo, Y. & Kim, Y.H. (2026), “Rethinking Variable Importance in Machine Learning: An Economic Perspective on Empirical Asset Pricing,” Financial Analysts Journal 82(2).
- Saly-Kaufmann et al. (2026), “Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance,” arXiv:2603.01820.
- Bysik & Ślepaczuk (2026), “Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting,” arXiv:2606.00060.
- Koijen & Levy (2026), NBER Working Paper 35431, real-time out-of-sample asset-pricing benchmark.

## Status

This is a protocol update, not evidence of alpha. Existing repository documentation still flags forward-label overlap as a blocker for trusting older model results.
