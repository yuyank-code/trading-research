# Research 45 — Predictive Content vs Economic Baseline

## Date
2026-09-20

## Question
Does a sophisticated ML predictor add economically meaningful value beyond a transparent baseline once both are subjected to identical portfolio construction and realistic execution costs?

## Literature synthesis

### 1. Bysik & Ślepaczuk (2026)
The hourly BTC-USDT walk-forward study evaluates XGBoost, LSTM and iTransformer under 10 bps transaction costs. Naive sign-based strategies lose money after costs; cost-aware filtering can restore profitability in selected configurations, but bootstrap evidence does not establish formal dominance of XGBoost over alternatives.

Implication: prediction quality is not sufficient; the conversion from forecast to trade and the execution layer must be evaluated jointly.

### 2. Lalwani et al. (2026)
The empirical asset-pricing study evaluates 5,376 ML portfolios and finds large return variation from research-design choices, with nonstandard errors up to five times standard errors. This makes the common practice of treating one portfolio construction and one training-window choice as fixed evidence especially fragile.

Implication: baseline and design choices must be frozen and treated as part of the experiment, not optimized after observing results.

### 3. Saly-Kaufmann et al. (2026)
The large-scale financial time-series benchmark evaluates OOS risk-adjusted performance across multiple asset classes and includes transaction-cost break-even analysis, tail risk, random-seed robustness and computational efficiency.

Implication: a useful benchmark must evaluate economic robustness, not only predictive accuracy or raw return.

### 4. Arian, Norouzi Mobarekeh & Seco (2024)
Controlled synthetic experiments report CPCV as superior to conventional OOS methods for mitigating backtest-overfitting risk.

Implication: incremental-value testing must sit on top of leakage-safe OOS validation, not replace it.

### 5. Santoni, Jouanne & Scullin (2026)
The MinervaScore combines DSR, PBO, SPA and minimum-track-record gates. Importantly, its own pre-registered real-market test did not show a significant forward relationship, so it should be interpreted as an audit/reporting layer rather than evidence of predictive power.

Implication: robustness scores must not be confused with alpha.

## Testable hypothesis
H95 asks whether the candidate's incremental net value versus a transparent baseline survives identical execution, subperiod, cost and multiplicity controls.

## Required experiment
- Freeze baseline and candidate specifications before scoring.
- Use point-in-time data.
- Correct forward-label overlap at walk-forward boundaries.
- Purge and embargo all overlapping information.
- Generate an immutable candidate-level OOS prediction/return matrix.
- Apply identical portfolio construction and execution to candidate and baseline.
- Include commission, spread, slippage, market impact and capacity assumptions.
- Report gross/net return, Sharpe, Sortino, drawdown, turnover, break-even cost and benchmark-relative net value.
- Run adverse cost stress and pre-specified regime/subperiod analysis.
- Account for all candidate/seed/design trials through the committed trial ledger.
- Compare the selected candidate with matched null-search winners.

## Current conclusion
The literature strengthens the case for testing **incremental economic content**, rather than rewarding models for absolute performance that may originate from the common portfolio/execution layer. No new alpha claim is made because the repository still lacks the required immutable candidate-level OOS matrix and corrected forward-label-overlap validation.

## Sources
- Bysik, A. & Ślepaczuk, R. (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*, arXiv:2606.00060.
- Lalwani et al. (2026), *Empirical Asset Pricing via Machine Learning: The Role of Research Design Choices*, European Financial Management, DOI:10.1111/eufm.70033.
- Saly-Kaufmann et al. (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*, arXiv:2603.01820.
- Arian, H., Norouzi Mobarekeh, D. & Seco, L. (2024), *Backtest overfitting in the machine learning era: A comparison of out-of-sample testing methods in a synthetic controlled environment*, Knowledge-Based Systems 305, 112477. DOI:10.1016/j.knosys.2024.112477.
- Santoni, M. L., Jouanne, V. & Scullin, M. L. (2026), *Equity Strategy Backtesting: Luck or Edge? The MinervaScore as a Statistical Robustness Grade*, arXiv:2608.23808.
