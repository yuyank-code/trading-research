# H156 — Real-Time Information Gate vs Conventional Historical Backtest

Date: 2026-09-22
Status: registered; not yet numerically evaluated

## Question

Does enforcing an explicit decision-time information boundary materially reduce apparent strategy performance or model-selection stability relative to a conventional historical pipeline?

## Controlled comparison

**A — Conventional pipeline:** historical feature tables and labels with ordinary chronological walk-forward splits.

**B — PIT pipeline:** every feature and universe decision is reconstructed from observations available by the decision timestamp; revised data are excluded until their publication/release time.

**C — PIT + purge/embargo:** additionally remove observations whose forward labels overlap the training/validation/test boundary, with embargo based on the maximum label horizon.

**D — PIT + purge/embargo + economic gate:** same as C, followed by untouched OOS evaluation with frozen cost/slippage assumptions and multiple-testing adjustment.

## Primary outcomes

- net OOS Sharpe;
- annualized net return;
- maximum drawdown;
- turnover;
- average and tail transaction cost;
- model-selection rank stability across folds;
- PBO / Deflated Sharpe where applicable.

## Failure conditions

The experiment fails if:

- any feature timestamp exceeds the decision timestamp;
- a label interval overlaps a training sample after purge;
- universe membership uses future survivorship information;
- cost assumptions are tuned after observing final OOS;
- model/hyperparameter selection touches the untouched final OOS;
- a strategy only survives because of one exceptional fold.

## Robustness grid

Run the final candidate under:

- baseline costs;
- 1.5× costs;
- 2× costs;
- one-period execution delay;
- conservative slippage;
- liquidity/capacity restriction.

Do not re-optimize under the stress scenarios.

## Promotion rule

No model is promoted merely because PIT enforcement lowers or raises performance. Promotion requires a positive incremental net OOS result versus the frozen baseline, stability across independent test paths, and survival of the pre-registered multiple-testing gate.

## Motivation

Recent 2026 evidence emphasizes real-time information boundaries and shows that conventional predictive validation can create economically irrelevant positives. This hypothesis tests the validation architecture directly rather than assuming that a better model architecture is the main source of improvement.
