# Research 30 — Capacity, Market Impact, and Execution Robustness

## Literature synthesis

Capacity should be treated as an economic constraint, not merely a reporting statistic. Novy-Marx and Velikov (Review of Financial Studies, 2016) show that transaction costs materially change anomaly profitability and that low-turnover strategies generally support more capital; they also find that cost mitigation can materially affect net spreads. citeturn1search19

Recent OTC evidence is even more direct: a September 12, 2026 Review of Finance study using a dealer's complete trading record finds substantial dispersion in bid-ask spreads across client types and attributes much of the variation to execution efficiency, including platform choice, market-technology familiarity, negotiation conventions, and dealing relationships. citeturn1search3

A 2024 Review of Financial Studies study of bond-market trading costs finds both size discounts and size penalties: larger trades can obtain better prices across clients, but within-client trading costs increase with trade size, particularly during major macroeconomic surprises and stress periods. citeturn1search6

A 2025 Review of Financial Studies equilibrium model further shows that proportional transaction costs can affect equilibrium return variance and the incentives to trade. citeturn1search0

## Implication for the project

A backtest using a fixed bps-per-dollar cost can overstate scalability. The project therefore needs an explicit participation/impact layer after signal generation but before portfolio PnL. The layer must be causal: today's executable size may depend only on information available before execution.

## Testable prediction

If the strategy's economic edge is genuine, net performance should decay continuously rather than collapse immediately as capital and participation increase. If the edge is an artifact of unrealistic execution assumptions, the capacity curve will show a sharp break, high implementation shortfall, or unstable rankings across plausible impact parameters.

## Experimental design

Freeze the candidate family and all signal/model choices. Evaluate 0.25x, 0.5x, 1x, 2x, 4x, and 8x baseline notional, subject to a pre-defined participation cap. Use at least three plausible impact specifications: linear, square-root, and stressed nonlinear impact. Keep spread, commission, and slippage assumptions unchanged except for the scale-dependent impact component.

For every candidate and scale, store the complete OOS return series and execution diagnostics. Report net Sharpe, Sortino, drawdown, turnover, implementation shortfall, cost/gross-PnL ratio, break-even costs, and capacity utilization. Evaluate fold-by-fold stability and the full multiple-testing gate (DSR/PBO, SPA/Reality Check, Model Confidence Set, and synthetic-null controls).

## Guardrails

Do not infer capacity from future volume, future spreads, or future realized liquidity. Do not tune the participation cap on the confirmation block. If a trade exceeds the cap, apply the fixed mechanical clipping rule and record the unfilled quantity.

## Bottom line

The literature strengthens a project-wide rule: **a strategy is not economically robust merely because its Sharpe survives a constant transaction-cost haircut.** Scalability and execution conditions must be tested explicitly. This research motivates H79 but does not constitute evidence that the project's candidate models possess capacity.

## Sources

- Novy-Marx, R. & Velikov, M. (2016), *A Taxonomy of Anomalies and Their Trading Costs*, Review of Financial Studies. citeturn1search19
- *Who Pays the Most to Trade? Cross-client Dispersion in OTC Liquidity Prices*, Review of Finance, published September 12, 2026. citeturn1search3
- *Size Discount and Size Penalty: Trading Costs in Bond Markets*, Review of Financial Studies, 2024. citeturn1search6
- Loewenstein & Qin (2025), *Equilibrium Model of Imperfect Hedging: Transaction Costs, Heterogeneity in Risk Aversion, and Return Volatility*, Review of Financial Studies. citeturn1search0
