# H131 — Selective Abstention vs Always-Trade

## Research question

Does allowing a model to abstain when its expected net trading utility is weak improve genuinely out-of-sample economics relative to always trading the same forecast?

## Motivation

Recent 2026 work on leakage-aware selective ML proposes deciding whether a signal should be deployed by comparing it with a transparent fallback benchmark, with abstention calibrated only on past validation data. A separate 2026 BTC walk-forward study reports that naive sign trading can lose its economics under 10 bps costs while a cost-aware forecast-magnitude filter can reduce turnover and recover profitability in selected configurations. These findings motivate a controlled test, not an assumption that selective trading works.

## Experimental arms

1. Always-trade frozen candidate.
2. Selective candidate: trade only when predicted incremental net utility over the fallback exceeds a threshold calibrated inside the training/validation layer.
3. Fallback-only baseline.
4. Matched-noise selective placebo using the same gate-selection budget.

## Leakage controls

- Point-in-time features and labels.
- Gate thresholds selected only from information available before each OOS block.
- Purge/embargo whenever label horizons overlap observations used for gate calibration.
- No final-OOS threshold tuning.
- Preserve gate decisions row-by-row.

## Economic controls

Evaluate commission, spread, slippage, nonlinear impact, and borrow/funding where relevant. Stress all cost assumptions at 1x, 1.5x, and 2x. Add execution-lag perturbations.

## Primary endpoint

Incremental net OOS utility of selective deployment versus always-trade, paired on identical timestamps.

## Secondary endpoints

Turnover, cost fraction of gross P&L, maximum drawdown, tail loss, gate activation rate, performance by regime, break-even cost, and stability across cost models.

## Falsification criteria

Reject the selective mechanism if its advantage disappears against the matched-noise placebo, is confined to one cost model, requires final-OOS tuning, or vanishes after corrected purge/embargo handling.

## Promotion rule

No promotion from this hypothesis alone. A positive result must also pass the repository's selection-aware evidence standard and immutable final-OOS accounting.
