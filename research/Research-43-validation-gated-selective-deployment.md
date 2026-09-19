# Research 43 — Validation-Gated Selective Deployment

## Research question
Can a model-aware abstention/deployment gate convert weak or friction-sensitive forecasts into more robust net trading performance without introducing a new source of look-ahead or selection bias?

## Literature synthesis
A September 2026 SSRN paper on volatility-gated inference reports that an always-trade EUR/USD forecasting strategy with negative test Sharpe became positive after a volatility gate reduced trade switches. This is a useful hypothesis generator, but it is a single study and should not be treated as established evidence. A July 2026 SSRN study on leakage-aware selective factor rotation similarly proposes rolling-origin validation gates and reports lower turnover and improved net Sharpe in its baseline experiment. These results motivate testing abstention, not accepting them as proof.

A stronger counterweight is the July 2026 leak-free, cost-aware US-equity benchmark: its promoted MLP only marginally exceeded a no-ML Black-Litterman prior and incurred more than three times the cumulative transaction cost. This suggests that a deployment gate must demonstrate incremental value over a transparent fallback, not merely improve a model's own backtest.

A May 2026 BTC walk-forward study also finds that naive sign-based strategies fail under 10 bps costs and that cost-aware execution thresholds can restore profitability in selected configurations, although formal dominance is not established. This makes turnover and break-even cost first-class endpoints for H92.

## Testable prediction
If the model contains conditional information that is economically useful but not worth trading continuously, a validation-only gate should improve benchmark-relative net utility, reduce turnover, and retain performance under adverse cost/slippage stress. If the apparent signal is spurious, the same gate should not separate reliably from matched null searches.

## Experimental design
1. Freeze the candidate model specifications and transparent fallback.
2. For every training/validation origin, estimate the candidate's incremental net utility over the fallback using only data available at that origin.
3. Calibrate one of a small pre-registered set of gate forms (utility margin, confidence margin, or volatility/cost-normalized margin) inside training/validation only.
4. Produce causal decisions for the next OOS block.
5. Evaluate always-trade, gated, and fallback portfolios on the same untouched OOS blocks.
6. Apply realistic commission/spread/slippage and nonlinear impact stress.
7. Compare against matched zero-alpha/null-search winners using the same search budget.
8. Report DSR/PBO and SPA/Reality Check or equivalent selection-aware inference; include MCS where the candidate set supports it.
9. Report subperiod/regime stability, break-even cost, turnover, capacity proxy, and worst-seed results.

## Failure modes to watch
- Gate threshold chosen from confirmation performance.
- Gate indirectly using future volatility or future realized costs.
- Repeatedly searching gate forms until one works.
- Comparing gated candidate to an unfairly executed fallback.
- Mistaking reduced turnover for alpha.
- Gate improvement disappearing under 2x cost/slippage stress.

## Current status
Design-only. No empirical pass is claimed. The repository's existing blockers remain: corrected forward-label-overlap validation and an immutable candidate-level OOS prediction/return matrix are required before model-performance conclusions can be trusted.
