# Research 64 — Selective Abstention and Cost-Gated Execution

## Date
2026-09-20

## Literature synthesis

Two recent 2026 results are directly relevant.

1. Bysik & Ślepaczuk, *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting* (2026) reports that naive sign-based ML trading can fail under 10 bps transaction costs, while a forecast-magnitude filter tied to transaction costs can sharply reduce turnover and restore profitability in selected configurations. The authors do not establish formal statistical dominance for XGBoost.

2. Guo, *When Not to Trade: Leakage-Aware Selective Machine Learning for Factor Rotation* (2026 preprint) proposes a rolling-origin selective rule that deploys ML only when validation improvement over a transparent fallback exceeds a calibrated threshold; its reported baseline experiment is promising but remains preprint evidence and therefore is not treated as established fact.

The common mechanism is economically important: the trading decision should include the **option not to trade** when expected incremental edge is too small relative to friction and uncertainty.

## Testable contribution to this project

H114 turns that mechanism into a preregistered falsification test. The model is not allowed to choose a favorable OOS threshold. Gate calibration occurs only on historical information available at each decision date, and the final OOS period remains untouched.

## Experimental matrix

| Arm | Signal | Gate | Fallback | Costs |
|---|---|---|---|---|
| A | candidate | none | none | full realistic model |
| B | candidate | cost + safety margin | frozen fallback | full realistic model |
| C | none | n/a | frozen fallback | full realistic model |
| D | placebo signal | same gate | frozen fallback | full realistic model |

The key estimand is B minus A in net OOS utility, with B minus C required to establish that the gate does not merely recreate the fallback.

## Stress tests

- reference transaction-cost model;
- 1.5x and 2x friction stress;
- execution-lag perturbation;
- predefined subperiod/regime partitions;
- turnover and capacity limits;
- seed variation for stochastic candidates.

## Leakage audit

The gate must never consume realized returns from the period it decides on. Validation calibration is rolling-origin. Any overlapping forward labels are purged with an embargo. Preprocessing is fit inside each training fold. Every attempted threshold/calibration configuration is entered into the trial ledger.

## Current result

No numerical result is claimed. The repository still lacks the immutable candidate-level OOS prediction/position/return/cost matrix required for credible execution of this experiment. This research therefore adds a protocol, not an alpha claim.

## Decision rule

Do not promote unless the selective rule improves net OOS utility over always-trade, survives cost stress and subperiod tests, beats the frozen fallback, and does not show placebo significance or search-induced inflation.
