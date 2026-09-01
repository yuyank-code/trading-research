# Research Run 12 — Nested OOS and Embargo Audit

Date: 2026-09-02

## Meaningful findings

1. The current `bitcoin-ml-trading/production_research.py` is horizon-purged: `train_end = start - HORIZON_BARS` with a 6-bar forward label. This prevents direct label-window overlap at each walk-forward boundary.
2. The production engine nevertheless generates multiple model/feature portfolios on the same OOS prediction stream and then reports each result. This is acceptable for exploratory diagnostics but is not a pristine final model-selection procedure. Final selection must be made on a development period and evaluated once on an untouched holdout.
3. The execution rule is cost-aware in the sense that it compares expected gross stop/target payoff with a round-trip fee/slippage hurdle. This is a useful hypothesis, but the cost hurdle itself must be predeclared before the final holdout and tested across a conservative cost grid.
4. The current purge is row/horizon based. The next validation hardening step is explicit event-time interval purging (`prediction_time`, `label_end_time`) plus an embargo. This matters if future experiments introduce variable horizons or longer information/execution windows.

## Literature update

- Bailey & López de Prado (2014), Deflated Sharpe Ratio: multiple testing and non-normality inflate reported Sharpe; the number of trials must enter inference.
- Bailey, Borwein, López de Prado & Zhu (2017), Probability of Backtest Overfitting: conventional holdouts can still fail after broad strategy search.
- Aparicio & López de Prado (2018): model-selection procedures can themselves be unreliable under multiple testing and weak signal-to-noise.
- Bysik & Ślepaczuk (2026), arXiv:2606.00060: in hourly BTC-USDT experiments, naive sign-based ML trading was vulnerable to transaction costs while forecast-magnitude/cost-aware filtering reduced turnover and recovered profitability in selected configurations; model dominance was not statistically established.

## New hypotheses

H35 — Explicit event-time purge and embargo produce equal-or-stricter training boundaries than the current six-bar purge.

H36 — Cost-aware abstention improves net performance with predictions frozen, rather than through retraining/model selection.

H37 — A candidate that survives only one favorable fee/slippage assumption is rejected.

H38 — The final policy selected on development OOS retains its sign and acceptable risk-adjusted performance on an untouched holdout.

H39 — DSR/PBO-adjusted evidence is materially weaker than raw Sharpe when all tried configurations are counted; any apparent edge must survive that haircut.

## Reproducibility gate

Do not promote numerical performance until the repository contains:
- immutable OOS prediction artifact;
- fold-level predictions/trades/equity;
- complete trial registry;
- data/code version manifest;
- explicit cost assumptions and sensitivity grid;
- final holdout identifier that was not used for selection.

No new trading edge is claimed in this run because the required generated OOS artifacts are not present in the repository.
