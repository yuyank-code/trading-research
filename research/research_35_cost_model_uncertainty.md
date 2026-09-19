# Research 35 — Cost-Model Uncertainty and Execution Robustness

## Literature synthesis

Execution-cost uncertainty is not a cosmetic backtest parameter. Almgren & Chriss (2001) formulate optimal execution as a trade-off between volatility risk and temporary/permanent market impact. Olivares-Nadal & DeMiguel (2018, *Operations Research*) show that transaction costs can be interpreted as regularization that limits excessive rebalancing in the presence of estimation error. Hautsch & Voigt (2019, *Journal of Econometrics*) similarly show that transaction costs interact with parameter uncertainty and that turnover penalization can materially affect portfolio construction.

Recent evidence strengthens the practical case. A 2026 study of realistic market-impact modelling reports that replacing a fixed 10-bps assumption with a nonlinear impact model materially changes trading behavior and algorithm rankings. A 2025 *Mathematical Finance* paper studies realistic nonlinear price impact and finds that appropriately chosen effective quadratic costs can approximate nonlinear-impact optimal performance. These results imply that a strategy should be tested against a family of plausible execution models rather than a single convenient haircut.

A 2026 walk-forward Bitcoin study is also directly relevant: naive sign-based strategies became uneconomic at 10 bps, while a cost-aware forecast-magnitude filter reduced turnover and restored profitability in selected configurations. Importantly, the authors did not establish statistical dominance of the preferred model, reinforcing the need to separate descriptive improvements from robust evidence.

## Research implication

The project should distinguish **prediction robustness** from **execution-model robustness**. A signal can be statistically stable while its trading implementation remains economically fragile. Cost uncertainty therefore becomes a falsification test: if modest plausible execution changes reverse the economic conclusion, the candidate should not be promoted.

## Testable extension

H84 pre-registers a cost-model sensitivity experiment using the same frozen OOS candidate trades across proportional costs, linear impact, square-root impact, and adverse-slippage scenarios. The execution specification is frozen before confirmation and cannot be tuned against confirmation performance.

## Key sources

- Almgren, R. & Chriss, N. (2001), *Optimal Execution of Portfolio Transactions*, Journal of Risk.
- Olivares-Nadal, A. V. & DeMiguel, V. (2018), *A Robust Perspective on Transaction Costs in Portfolio Optimization*, Operations Research.
- Hautsch, N. & Voigt, S. (2019), *Large-Scale Portfolio Allocation Under Transaction Costs and Model Uncertainty*, Journal of Econometrics.
- Brokmann (2025), *Tackling nonlinear price impact with linear strategies*, Mathematical Finance.
- Riera Abbade & Reali Costa (2026), *Realistic Market Impact Modeling for Reinforcement Learning Trading Environments*.
- Bysik & Ślepaczuk (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*.

## Status
Literature synthesis complete; empirical execution is pending the repository's frozen candidate-level OOS prediction/return matrix and corrected forward-label-overlap validation.
