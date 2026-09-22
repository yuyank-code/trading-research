# Research 105 — Real-Time Event Information and Hierarchical Validation

Date: 2026-09-22

## Literature signal

Koijen & Levy (NBER Working Paper 35431, July 2026) emphasize that historical ML asset-pricing backtests can suffer look-ahead bias because models are trained on the full historical sample. Their real-time benchmark restricts each decision to information available at the contemporaneous earnings announcement. They report that optimized AI systems more than doubled explained variation relative to standard benchmarks in that setting, while explicitly framing real-time evaluation as necessary because markets are reflexive. [https://www.nber.org/papers/w35431]

Kim (2026, revised August 2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, reports 27–30% false-positive rates for AUC-only validation in Monte Carlo experiments, reduced to 0% in the reported experiments using combinatorial purged cross-validation with PBO. The paper also reports that transaction costs materially change strategy rankings and that several apparently significant variants fail Deflated Sharpe Ratio tests. [https://doi.org/10.2139/ssrn.6508779]

Chen, Wang & Huang (2026), *Variational Autoencoder Asset Pricing models with economic restrictions*, reports improved OOS results from economic restrictions and variational regularization. This is useful as a candidate modeling direction, but its reported alpha is not transferable evidence for our project until reproduced under our own PIT, cost and multiple-testing protocol. [https://doi.org/10.1016/j.iref.2026.105402]

## Research implication

The project should distinguish three validation layers:

1. **Information-set validity:** every feature, label, universe membership, corporate action, macro observation and execution variable must have an explicit availability timestamp.
2. **Path validity:** training/validation/test windows must be separated with purge and embargo periods derived from the maximum label horizon and feature lookback.
3. **Economic validity:** the untouched final OOS must be converted to executable P&L with spread, commission, slippage, market impact, borrow and capacity assumptions before promotion.

A model should not be allowed to select its own validation architecture, cost assumptions or final OOS boundary. These must be frozen before final evaluation.

## New pipeline requirement

Add a **decision-time audit table** to every experiment with:

- decision timestamp;
- latest permissible observation timestamp;
- maximum feature lookback;
- label start/end;
- purge interval;
- embargo interval;
- execution timestamp;
- execution price assumption;
- cost model version;
- universe snapshot identifier.

Any row violating these constraints should fail the experiment rather than being silently dropped.

## Key conclusion

The highest-value improvement is not another neural architecture. It is making the information boundary executable and auditable. Only after the forward-label-overlap blocker is eliminated should model comparisons be promoted to numerical findings.
