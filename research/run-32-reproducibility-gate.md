# Run 32 — Reproducibility Gate and Trial Accounting

Date: 2026-09-03

## Meaningful finding

The research repository is healthy and current, but it is still a **research record rather than an executable reproduction package**. The latest repository commit remains the Run 31 audit (`596aa248b31179f683c0889ecbfac46dd687bbfe`). No executable market-data snapshot, production model engine, or frozen prediction artifact is present in this repository.

This means a new Sharpe, PBO, or cost-stress number cannot be independently reproduced from this repository alone. That is a reproducibility blocker, not evidence for or against the strategy.

## Literature update

Bailey et al. show that a relatively small number of alternative strategy configurations can generate apparently exceptional backtests by chance, and that the probability of overfitting rises with the number of configurations tested. Their PBO/CSCV work specifically motivates estimating the probability that the selected backtest is overfit rather than treating a conventional holdout as sufficient.

Bailey and López de Prado's Deflated Sharpe Ratio further motivates adjusting the selected Sharpe for multiple testing and non-normal returns.

A recent 2026 BTC-USDT walk-forward study independently reinforces the economic side: positive gross forecast performance can disappear at realistic transaction costs, while a pre-specified cost-aware trade filter can materially reduce turnover.

## New testable hypotheses

### H18 — Complete trial accounting

Every materially evaluated model, feature set, target definition, threshold grid, cost assumption, and execution rule must receive a trial identifier. Discarded or failed variants remain in the ledger. DSR/PBO inputs must use the documented trial count rather than only the final shortlist.

### H19 — Artifact sufficiency

A promoted result must be reproducible from versioned: (1) source-data snapshot/hash, (2) feature code/version, (3) event-label definition, (4) split/embargo specification, (5) model configuration, (6) execution/cost configuration, and (7) frozen OOS predictions/trades. Missing any required artifact blocks promotion.

### H20 — Selection stability

The final candidate must be selected without using the untouched final holdout. Re-running the selection process on earlier research periods should not systematically produce a different class of strategy merely because of small changes in the training/validation boundary.

## Required next experimental gate

1. Bring the executable engine and exact data snapshot under version control or attach immutable content hashes.
2. Implement the event-time target (`signal_time`, `entry_time`, `event_end_time`) and interval-based purging.
3. Make external features point-in-time (`available_at <= signal_time`) and preserve vintage identifiers where revisions exist.
4. Freeze candidate predictions before cost/threshold analysis.
5. Run a predeclared cost/slippage grid.
6. Resolve or bound intrabar stop/target ambiguity.
7. Run CPCV/PBO and DSR using the complete trial ledger.
8. Only then expose the final untouched holdout.

## Verdict

No new profitability claim is justified in Run 32. The robust result is methodological: **reproducibility and complete trial accounting are promotion gates, not documentation afterthoughts.**
