# H60 — Point-in-Time Availability Contract

## Status
Proposed hard gate; implementation pending executable market-data artifacts.

## Hypothesis
A trading workflow that enforces a machine-checkable `available_time <= decision_time` contract for every feature and execution input will prevent a class of false OOS improvements caused by publication/availability-time leakage.

## Motivation
Recent financial-ML research shows that apparently rigorous walk-forward results can remain spurious when the research workflow is adaptive or when future information enters through preprocessing or market-data availability. The relevant information boundary is not merely observation timestamp; it is when the information could actually have been known to the trading process.

## Test design
For every feature/input, store:
- event_time
- available_time
- decision_time
- order_time
- fill_time
- source/version identifier

Hard invariant:
`available_time <= decision_time <= order_time <= fill_time`

The test suite must contain adversarial fixtures in which:
1. `available_time` is shifted into the future;
2. next-bar OHLC/spread is exposed to the signal or execution layer;
3. a revised historical observation replaces its original point-in-time value.

The audit must fail each contaminated fixture and pass a clean fixture.

## Empirical promotion test
After the causal audit passes, candidate strategies must be evaluated with:
- purged/embargoed walk-forward OOS;
- fold-local preprocessing;
- explicit spread, commission and slippage assumptions;
- cost stress of +25%, +50% and +100%;
- complete trial registry;
- family-level multiple-testing correction (Reality Check/SPA where applicable);
- DSR/PBO or equivalent search-adjusted analysis;
- untouched confirmation period.

## Falsification criteria
Reject the pipeline if:
- any feature violates the availability contract;
- adversarial future inputs do not trigger the sentinel;
- OOS results depend on revised rather than point-in-time data;
- apparent edge disappears under modest execution-cost stress;
- the full searched family fails multiple-testing correction.

## Current evidence boundary
No strategy is promoted by H60. A numerical OOS claim requires frozen, timestamped market-data/prediction artifacts and a reproducible execution specification. Until those exist, this hypothesis is an engineering/statistical gate rather than evidence of profitability.
