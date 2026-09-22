# Research 116 — Null Falsification Before Alpha Certification

**Date:** 2026-09-23
**Status:** Committed research synthesis

## Executive finding

The next high-value test is not another model architecture. It is a falsification audit of the **entire predictive-to-trading workflow** on data where no exploitable signal is present.

Recent 2026 research strengthens this priority. *Spurious Predictability in Financial Machine Learning* proposes testing complete workflows against synthetic zero-predictability environments and microstructure placebos, because adaptive specification search can generate significant walk-forward evidence even under martingale-difference nulls. The paper describes winner inflation growing with effective search size and recommends measuring the gap between optimized in-sample evidence and disjoint walk-forward realizations.

A separate 2026 leakage-safe strategy-discovery study reports that structural leakage can survive Deflated Sharpe Ratio and Probability of Backtest Overfitting corrections; therefore statistical correction cannot substitute for information-flow controls. It also finds that explicit trial counting materially raises the evidential bar as search expands.

For hourly BTC specifically, 2026 walk-forward evidence reports that naive sign-based ML strategies can fail at 10 bps transaction costs, while a cost-aware forecast-magnitude filter can improve selected configurations. This supports testing the economic decision layer directly rather than optimizing prediction metrics in isolation.

## Implication for this project

Before any candidate can be promoted, the same feature engineering, scaling, model fitting, signal conversion, execution, cost model and statistical-selection machinery should be run through controlled nulls.

The audit should contain at least:

1. **Martingale null:** returns generated with no conditional predictive structure.
2. **Block-shuffled null:** preserve local dependence while destroying temporal predictability.
3. **Microstructure placebo:** preserve realistic volatility/spread-like behavior but remove the proposed alpha mechanism.
4. **Injected-signal control:** add a known signal with a predefined effect size to verify that the pipeline retains power rather than simply rejecting everything.

The complete search budget must be identical across null and signal controls. Every trial must be recorded before selecting a winner.

## Promotion consequence

A workflow that produces economically significant OOS results on the nulls is **falsified**, regardless of its DSR/PBO/SPA statistics. A workflow that fails to recover the injected signal is **underpowered or incorrectly implemented** and should not be trusted on historical data.

This creates a stronger hierarchy:

**information-flow validity → null falsification → injected-signal power → historical OOS evidence → cost/impact stress → selection-adjusted inference → final holdout.**

## Sources

- Gençay, E. (2026), *What survives honest evaluation? Leakage-safe, search-aware assessment of LLM-driven trading strategy discovery*, arXiv:2608.27734.
- Nikolopoulos, S. D. (2026), *Spurious Predictability in Financial Machine Learning*, arXiv:2604.15531.
- Bysik, A. & Ślepaczuk, R. (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*, arXiv:2606.00060.
- Saly-Kaufmann, A. et al. (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*, arXiv:2603.01820.
