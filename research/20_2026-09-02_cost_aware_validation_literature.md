# Run 20 — Cost-aware validation and overfitting controls

Date: 2026-09-02

## Meaningful findings

1. The executable-event alignment gate remains unresolved in `yuyank-code/bitcoin-ml-trading`. Issue #7 is open. The current production target is Close[t+6]/Close[t]-1 while the simulator enters at Open[t+1]. No candidate performance should be promoted until the supervised event matches the executable event.
2. The repository's validation-harness repair is on main (commit 0c8e79c), and the latest research protocol is recorded. This is infrastructure progress, not evidence of trading profitability.
3. Fresh literature continues to support cost-aware signal filtering rather than architecture proliferation. Bysik & Slepaczuk (2026), using ~70k hourly BTC-USDT observations and 27 walk-forward folds, report that naive sign strategies fail at 10 bps while cost-aware forecast-magnitude filtering can restore profitability in selected configurations; formal model-family dominance was not established.
4. Huang, Wang & Jiang (2026) similarly report a disconnect between prediction accuracy and net trading returns after explicit fees, spreads and slippage, with transaction-cost-aware filtering outperforming iterative deep-learning optimization in their experiments. Treat this as supporting evidence, not replication.
5. Bailey & Lopez de Prado (2014) remains the core statistical control: Deflated Sharpe adjusts for multiple testing and non-normality. The project must count model/feature/threshold variants in its trial registry.
6. A 2024 Knowledge-Based Systems controlled study reports CPCV outperforming conventional OOS methods on PBO/DSR diagnostics. This supports adding CPCV after executable-event alignment, not before.

## Testable hypotheses

H1: Executable-event labels improve stability versus Close-to-Close proxy labels when evaluated on the same frozen OOS periods.

H2: A predeclared forecast-magnitude threshold based on estimated execution cost improves net expectancy primarily by reducing low-edge trades, without materially degrading gross edge.

H3: Any selected model that fails DSR/PBO controls after accounting for the complete trial registry is treated as a research failure even if raw Sharpe is positive.

H4: Performance should remain directionally positive across a fixed fee/slippage grid and under separate spread/impact shocks; otherwise the edge is execution-fragile.

## Next gate

Executable event definition -> event-time purge -> explicit embargo -> frozen OOS predictions -> fixed cost grid -> development selection -> untouched holdout -> DSR/PBO/CSCV.

No profitability claim is made in this run.
