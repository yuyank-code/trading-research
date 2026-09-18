# H62 — Cost-aware signal threshold

## Status
PRE-REGISTERED — empirical execution pending frozen OOS artifacts

## Motivation
Recent 2026 evidence on hourly BTC trading reports that naive sign-based ML strategies can lose their apparent edge once transaction costs are imposed, while a forecast-magnitude threshold that requires expected return to clear trading costs can sharply reduce turnover and recover performance in selected configurations. This motivates testing execution policy separately from predictive model complexity.

## Hypothesis
For a fixed forecasting model and frozen feature set, trading only when the forecasted economic edge exceeds an ex-ante estimate of round-trip transaction cost plus a safety margin will improve net OOS risk-adjusted performance and reduce turnover relative to unconditional sign trading.

## Falsification criteria
The hypothesis fails if the cost-aware threshold does not improve net OOS Sharpe/Sortino or drawdown after costs, or if its apparent benefit disappears under adverse cost/slippage stress, alternative reasonable cost estimates, or disjoint confirmation windows.

## Protocol
1. Freeze model, features, training schedule, and execution timing before threshold selection.
2. Estimate costs using only information available at decision time.
3. Pre-register a small threshold grid based on estimated round-trip cost: 0.75x, 1.0x, 1.25x, 1.5x, 2.0x.
4. Select threshold only in development folds using purged/embargoed walk-forward validation.
5. Evaluate untouched OOS windows with explicit spread, fees, slippage, and latency.
6. Stress all costs by +25%, +50%, and +100%.
7. Compare against sign trading, no-trade, and simple volatility-scaled baselines.
8. Preserve every threshold trial in the registry and include the full family in Reality Check/SPA and DSR/PBO analysis where applicable.
9. Repeat with multiple seeds if the model is stochastic.

## Required artifacts
- fold-level predictions
- timestamped cost inputs
- threshold/trial registry
- net return series
- turnover and trade counts
- cost breakdown
- drawdown/tail metrics
- break-even cost
- stress-test matrix
- final untouched confirmation result

## Promotion gate
No promotion from this hypothesis alone. A thresholded strategy must also pass point-in-time availability, stateful preprocessing leakage, execution causality, workflow-null, selection-stability, research-design sensitivity, and family-level multiple-testing gates.
