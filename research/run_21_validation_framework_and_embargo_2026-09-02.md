# Run 21 — Validation framework and explicit embargo

Date: 2026-09-02

## Meaningful findings

1. The trading repository's research runner currently excludes training rows before `start - horizon_bars`. This protects against forward-label overlap, but it is a purge rule, not a separately parameterized post-test embargo.
2. A new repository issue (#8) was opened to require event-time interval validation and an explicit post-test embargo. The implementation must report purge and embargo separately and include regression tests proving that no training label interval overlaps a test event interval.
3. The existing executable-event alignment issue (#7) remains a hard gate. The supervised target must describe the same signal-to-entry-to-exit economic event that the simulator monetizes.

## Literature update

- Kim, *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading* (SSRN, revised Aug. 3, 2026): reports 340 crypto strategy variants and identifies directional prediction bias, statistical-economic disconnect, and transaction-cost omission as recurring failure modes. The proposed VALID framework reinforces fixed-order statistical and economic validation gates.
- Arian, Norouzi Mobarekeh & Seco, *Backtest overfitting in the machine learning era* (Knowledge-Based Systems, 2024): controlled experiments report CPCV as stronger than conventional OOS methods for mitigating backtest overfitting, with lower PBO and stronger DSR statistics.
- Bailey & Lopez de Prado, *The Deflated Sharpe Ratio* (Journal of Portfolio Management, 2014): multiple testing and non-normality inflate apparent Sharpe; trial counts must therefore be preserved and used in final inference.
- Bysik & Ślepaczuk, *Machine Learning-Based Bitcoin Trading Under Transaction Costs* (2026): hourly BTC-USDT ML strategies can lose their apparent edge under 10-bps costs; cost-aware forecast filtering is a testable economic hypothesis rather than proof of a universal edge.

## New testable hypotheses

H1: Event-aligned labels produce more stable OOS net performance than the current close-to-close target when execution begins at the next bar open.

H2: Adding a distinct post-test embargo reduces false confidence in settings with persistent features/returns, without materially reducing genuine OOS performance.

H3: Cost-aware abstention improves net expectancy primarily by reducing turnover; it should remain beneficial across a predeclared cost/slippage grid rather than only at one tuned cost.

H4: After accounting for all model/feature/threshold trials using DSR/PBO-style controls, any surviving edge should remain positive on an untouched final holdout.

## Current gate

Do not promote existing performance numbers as final evidence. First complete event alignment and interval-aware purge/embargo, then regenerate frozen OOS predictions and evaluate them under the fixed transaction-cost grid and multiple-testing controls.
