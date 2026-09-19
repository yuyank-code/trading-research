# Research 34 — Time-Scale Ensembles, Nonstationarity, and Robust FX Deployment

## Date
2026-09-19

## Research question
Can time-scale diversification make an FX ML trading signal less dependent on a single estimation window, while preserving net economic value after realistic execution costs?

## High-quality evidence

### Grigoriev, Musaev & Grigorieva (2026), *Cost-Aware Multiwindow Ensemble Decision Support for Nonstationary Foreign Exchange Markets*
The paper proposes transparent multiwindow FX experts using rolling-statistic features at different windows, with cost-aware supervisory aggregation. It evaluates non-overlapping OOS blocks across 16 FX pairs and includes Bayesian/dynamic aggregation baselines, lagged ML and sequence baselines, and ablations. The relevant methodological contribution is the explicit separation of time-scale diversity from the supervisory decision layer. This supports testing multiwindow stability as a pre-registered robustness mechanism, not treating the paper's reported results as evidence for our own FX universe.

### Saly-Kaufmann et al. (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*
A large benchmark across futures including FX evaluates OOS Sharpe together with statistical significance, downside/tail risk, break-even transaction costs, random-seed robustness, and computational efficiency. The study reinforces that architecture ranking should be judged on economic and stability criteria rather than generic predictive metrics alone.

### Zhang, Zhu & Linnainmaa (2025), *Man versus Machine Learning Revisited*, Review of Financial Studies
The paper demonstrates that correcting look-ahead bias can erase an apparently strong ML trading result. This is directly relevant: any ensemble weighting or lookback selection must be strictly nested inside the information set available at the decision time.

### Lopez de Prado & Fabozzi (2026), *The False Discovery Rate in Finance: Identification Failure and Search-Adjusted Estimation*
The paper highlights identification problems in estimating false discovery rates from reported financial research. For our project, this reinforces explicit search-budget accounting and the requirement that the ensemble not be granted free degrees of freedom through repeated window/weight selection.

## Testable implication
If time-scale diversity is economically useful, an ensemble fixed before confirmation should show either:
- higher benchmark-relative net utility; or
- similar utility with materially better fold/regime stability and lower sensitivity to the estimation window.

If the benefit is only visible after selecting the best lookback or weights on confirmation data, it is invalid evidence.

## Experimental design
1. Freeze candidate model architecture and causal feature set.
2. Generate forecasts for three fixed lookbacks: 8, 16, 32 observations.
3. Compare each single-window model with an equal-weight ensemble.
4. Optionally test one validation-only cost-aware supervisory weighting rule.
5. Keep confirmation untouched.
6. Apply the project's purge/embargo rule using the maximum label horizon.
7. Apply identical spread, slippage, market-impact, borrow, turnover, and capacity assumptions.
8. Evaluate benchmark-relative net utility, Sharpe/Sortino, drawdown, expected shortfall, turnover, implementation shortfall, and break-even costs.
9. Run matched-count random-window and synthetic-zero-alpha controls.
10. Apply DSR/PBO, SPA/Reality Check, and Model Confidence Set where the candidate count permits.

## Important limitation
The cited FX paper uses its own data, universe, frequency, and protocol. Its conclusions cannot be transferred directly to this project. The experiment is valuable only if the result survives our locked causal/OOS protocol.

## Status
Pre-registered as H83. No empirical result or promotion yet.
