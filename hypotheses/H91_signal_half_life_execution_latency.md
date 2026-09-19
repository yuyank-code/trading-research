# H91 — Signal Half-Life Must Exceed Execution Friction

## Status
Pre-registered; not yet passed.

## Motivation
Recent FX and trading literature reinforces that predictive information can be real but economically unusable when it decays faster than execution can monetize it. Recent ML trading work also finds that gross predictability can disappear after transaction costs, while microstructure studies find weak short-horizon information that is not necessarily exploitable at realistic fees. The project therefore needs to measure *signal persistence* and *net value decay*, rather than assuming that a forecast at timestamp t can be executed at the same economic value.

## Hypothesis
For a fixed causal predictor, the economically useful component of the signal is concentrated in horizons where forecast decay remains large relative to spread, slippage, and impact. Strategies whose predictive edge decays faster than execution friction will not retain positive net utility after realistic execution.

## Null
There is no systematic relationship between forecast persistence and net economic value after costs; apparent horizon differences are sampling noise.

## Design
1. Freeze the feature set, model family, training procedure, and candidate search budget.
2. Generate strictly chronological, purged/embargoed OOS forecasts.
3. For each forecast, measure predictive persistence over pre-registered horizons without using confirmation outcomes to choose the horizon.
4. Estimate signal half-life/decay using validation data only; never tune execution horizon on confirmation.
5. Evaluate matched holding/execution horizons with identical position-sizing logic.
6. Apply spread, commission, slippage and nonlinear impact assumptions, including adverse-cost stress.
7. Report gross forecast decay separately from net economic decay so costs cannot be hidden inside predictive metrics.
8. Compare against simple momentum/zero-signal benchmarks and matched null forecasts.
9. Apply DSR/PBO, SPA/Reality Check, Model Confidence Set, embargo sensitivity, subperiod/regime analysis, capacity stress, and the synthetic-zero-alpha workflow.
10. Preserve an immutable candidate-level OOS prediction/return matrix with the execution timestamp and assumed fill price for auditability.

## Pass criteria
The hypothesis may be supported only if the relationship between forecast persistence and net economic value is stable across confirmation subperiods and cost scenarios, survives multiple-testing controls, and is materially stronger than matched null forecasts. A shorter horizon cannot be preferred solely because its gross Sharpe is higher if its net utility is less robust.

## Failure conditions
- Signal decay is estimated using confirmation data.
- Execution horizon is selected after observing confirmation returns.
- Net value disappears under modest adverse costs/slippage.
- The apparent decay relationship is reproduced by null forecasts.
- Results depend on one regime or one currency pair.

## Literature motivation
Recent evidence includes walk-forward ML trading under explicit transaction costs, where naive high-frequency direction trading loses money at 10 bps and cost-aware thresholds improve selected configurations; a 2026 FX microstructure study finding weak information that fails realistic-fee tests; and FX research showing that market efficiency has increased as algorithmic trading has become more prevalent.

## Key implementation artifact
`candidate_oos_predictions.parquet` (or equivalent immutable candidate-level OOS prediction matrix) must exist before numerical promotion.
