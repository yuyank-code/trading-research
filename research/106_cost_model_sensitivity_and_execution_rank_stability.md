# Research 106 — Cost-model sensitivity and execution-rank stability

Date: 2026-09-22

## Question

Does a candidate trading model remain economically preferred when the execution-cost model is changed within a pre-specified plausible range, without re-optimizing the signal?

## Literature signal

Recent 2026 work on ML Bitcoin trading finds that apparently profitable hourly signals can become strongly negative after 10 bps of trading friction, while a cost-aware trading filter can materially change turnover and net performance. The study also reports that model rankings are not statistically decisive. This supports treating the execution model as a first-class robustness dimension rather than a single fixed assumption.

A 2026 study of realistic market-impact models for RL environments similarly finds that changing the cost model materially changes both absolute performance and the relative ranking of algorithms; nonlinear impact can radically alter learned turnover and behavior.

These results are hypothesis-generating for this project, not evidence of transferable alpha.

## Protocol

Freeze the signal/model and portfolio-construction parameters before cost stress testing. Evaluate the identical signal under a pre-registered cost matrix:

- explicit commission/fee: baseline, +50%, +100%
- spread: baseline, 1.25x, 1.5x
- slippage: baseline, 1.25x, 1.5x
- market impact: linear and square-root forms where data permits
- execution delay: 0, 1 bar, 2 bars
- capacity/liquidity haircut: baseline and conservative haircut

Do not select the best cost assumption after observing results. Report the complete matrix.

## Primary hypothesis H157

A genuinely robust candidate should preserve its rank against strong baselines across the pre-specified cost matrix and should not require a single favorable friction assumption to remain positive in net OOS utility.

## Falsification criteria

Reject economic promotion if any of the following occurs:

1. the candidate only wins under the lowest-cost assumption;
2. rank reversals are large across plausible cost models;
3. performance is driven by a small number of high-turnover periods;
4. a turnover-matched placebo achieves comparable net utility;
5. the candidate requires post-hoc cost calibration;
6. any feature/execution input violates the decision-time information boundary.

## Leakage controls

Use point-in-time features, purge/embargo labels, frozen model parameters within each OOS fold, and a completely untouched final OOS segment. Cost parameters are part of the evaluation environment and must not be tuned on the final OOS sample.

## Interpretation

A model that survives cost-model uncertainty earns stronger evidence of implementation robustness. Survival is not proof of alpha: it still requires multiple-testing correction, adequate track record, regime analysis, and replication on an independent period/market.

## Status

H157 registered. No numerical result is promoted until the forward-label-overlap blocker and point-in-time validation layer are resolved.
