# Research 102 — Selective Deployment / No-Trade Gate

Date: 2026-09-22

## Research question

Can a trading model improve net out-of-sample performance by abstaining from trades when the forecast is unlikely to clear a cost-adjusted economic hurdle, without turning the gate itself into an overfit parameter search?

## Literature

Recent 2026 work on selective forecasting shows that forecast difficulty varies materially by observation and that abstention can improve accuracy at controlled coverage levels. A 2026 finance-oriented preprint, *When Not to Trade: Leakage-Aware Selective Machine Learning for Factor Rotation*, proposes a rolling-origin deployment gate that falls back to a transparent benchmark when the ML signal does not clear a validated improvement threshold. Its reported empirical results are treated as provisional because the work is a preprint.

A stronger established economic foundation is the transaction-cost literature. Murthy & Wald (Quantitative Finance, 2023) derive optimal dynamic trading rules when returns are predictable and transaction costs are present. Their results reinforce that the economically relevant decision is not simply whether expected return is positive, but whether the expected benefit justifies the cost of moving the position.

Recent BTC walk-forward research (2026) provides a directly relevant empirical result: naive sign-based ML strategies that look attractive gross can fail after 10-bps transaction costs, while a cost-aware forecast threshold can reduce turnover and recover profitability in selected configurations. The reported model differences are not statistically decisive, so the execution rule is the more important transferable hypothesis.

## Evidence classification

- Theory: transaction costs imply a no-trade region / hurdle rather than continuous trading.
- Empirical: selective forecasting can improve performance at lower coverage; trading-specific evidence remains preliminary.
- Transferable project claim: only test whether abstention improves *net* OOS utility after all costs and multiplicity controls.
- Not established: that any specific threshold, model, or asset class will be profitable.

## Proposed experiment

Compare four frozen procedures:

1. Always trade the baseline model signal.
2. Fixed cost hurdle specified before OOS.
3. Validation-calibrated selective gate, with the calibration window strictly preceding OOS.
4. Coverage/turnover-matched placebo gate that receives no predictive information.

The selective gate may choose {trade, reduce, or abstain}, but all gate parameters must be fixed before the final OOS period. No threshold may be tuned on final OOS.

## Economic evaluation

Report gross return, net return, Sharpe, downside risk, max drawdown, turnover, hit rate, average edge per trade, realized spread/slippage, market impact, borrow where relevant, capacity, and breakeven cost.

Stress at 1x, 1.5x, and 2x baseline costs and with one-period execution delay. Do not retune under stress.

## Leakage / overfitting controls

- Point-in-time features and universe membership.
- Purging/embargo based on the maximum label horizon.
- Calibration data must precede evaluation data.
- Final OOS remains untouched until the complete procedure is frozen.
- Record every gate/threshold trial.
- Use PBO/CSCV and Deflated Sharpe or equivalent multiple-testing correction before promotion.
- Run the complete workflow on shuffled-label and zero-predictability null data.

## Promotion criterion

Promote only if the selective procedure beats the always-trade baseline and the turnover-matched placebo on net OOS utility, remains positive under 1.5x cost stress, does not fail the null workflow, and survives multiplicity-aware significance. A reduction in turnover alone is not evidence of predictive value.

## Current status

Protocol addition only. No numerical alpha claim is made because the repository still identifies the historical forward-label-overlap issue as a blocker for trusting older model results. The corrected validation implementation must precede any promotion.
