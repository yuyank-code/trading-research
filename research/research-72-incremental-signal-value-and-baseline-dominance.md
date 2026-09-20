# Research 72 — Incremental Signal Value and Baseline Dominance

Date: 2026-09-21

## Executive finding

The strongest new evidence this pass argues for a stricter question than “which ML model wins?”: **does the predictive model add value beyond a disciplined baseline once the entire downstream portfolio and execution stack is held constant?**

## Evidence reviewed

### Bengoechea Pardo (2026)

*On the Limits of Low-Frequency OHLCV Signals in Machine Learning-Driven Portfolio Optimization* (SSRN 6952859) reports a leak-free, cost-aware benchmark on 30 large-cap US equities from 2010–2025. Eleven models were evaluated with anchored walk-forward retraining and a pre-specified promotion gate. The reported negative result is especially relevant: the best promoted MLP had only a marginal Sharpe advantage over a no-ML Black-Litterman prior-only baseline while incurring substantially higher cumulative transaction costs; an equal-weight portfolio was also close. The author's attribution is that much of the risk-adjusted performance came from covariance regularization and Bayesian shrinkage rather than predictive content.

Source: https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6952859

### Saly-Kaufmann, Wood, Calliess & Zohren (2026)

The large-scale futures benchmark evaluates linear, recurrent, transformer, state-space and hybrid sequence models on daily futures data from 2010–2025. It goes beyond average return to include statistical significance, downside/tail risk, break-even transaction costs, random-seed robustness and computational efficiency. It reports that some richer temporal models outperform linear baselines, demonstrating that baseline dominance is not assumed; it must be measured under a comparable economic protocol.

Source: https://arxiv.org/abs/2603.01820

### Bysik & Ślepaczuk (2026)

The hourly BTC walk-forward study finds that sign-based ML strategies can lose their economics at 10 bps, while cost-aware filtering improves selected configurations. XGBoost is descriptively stronger in their tested set, but bootstrap evidence does not establish formal statistical dominance. This reinforces the need to compare complete trading systems rather than predictive metrics alone.

Source: https://arxiv.org/abs/2606.00060

### Belyakov (2026)

AlphaZeroBeta uses a transaction-cost-aware reward and rolling walk-forward evaluation for market-neutral portfolio construction. The paper is useful as evidence that portfolio objectives can incorporate costs directly, but its reported outperformance is treated as external evidence rather than as proof of a transferable edge.

Source: https://arxiv.org/abs/2607.18001

## Project implication

H123 introduces **baseline dominance / incremental signal value** as a promotion gate. Candidate ML models must beat strong frozen baselines using identical information, universe, risk normalization, portfolio construction, execution timing and cost assumptions.

This avoids a common attribution error: crediting the model for performance actually produced by a portfolio optimizer, covariance estimator, risk target, or generic market exposure.

## Required result artifact

For every candidate and baseline on every OOS timestamp, preserve:

`timestamp, candidate_id, baseline_id, prediction, position, turnover, gross_return, commission, spread, slippage, impact, borrow_or_funding, net_return`

plus data snapshot/version, training cutoff, label horizon, execution convention, and configuration/seed.

The comparison must be paired on identical timestamps and repeated under stressed costs. The final holdout remains single-use.

## Status

This is a new falsifiable hypothesis and attribution control, not a project alpha result. The current repository still lacks the immutable candidate-level OOS matrix and corrected forward-label-overlap validation required for numerical promotion.
