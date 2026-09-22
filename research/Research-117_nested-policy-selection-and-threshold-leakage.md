# Research 117 — Nested Policy Selection and Threshold Leakage

## Date
2026-09-23

## Meaningful finding

An audit of the connected `bitcoin-ml-trading` code found that `research_v2.py` performs a fixed threshold sweep **after generating one outer purged walk-forward prediction set**. The same OOS observations are therefore reused to rank thresholds and report the best trading result. This is not a pure model-prediction leakage problem, but it is a **policy-selection / model-selection leakage problem**: the reported threshold is selected using returns from the period subsequently presented as evidence.

The repository already contains `nested_policy_research.py`, which implements the correct separation: fit on an older training block, select the threshold on a predeclared calibration block, then freeze that threshold for the outer test fold. This is materially safer than the current `research_v2.py` main sweep.

Recent evidence reinforces this distinction. Kim (2026) reports that conventional validation can produce false positives in crypto ML and that CPCV/PBO and economic gates are needed beyond prediction metrics; the study also reports substantial transaction-cost erosion. Li, Mulvey & Fabozzi (2026) report benefits from separating prediction/portfolio optimization from execution-cost management rather than allowing an unconstrained backtest to choose the trading rule.

## Testable implication

If threshold selection is contributing to reported performance, then:

1. ranking thresholds on the same outer OOS period will overstate performance relative to nested policy selection;
2. model/feature rankings may change once each threshold is selected only from a development/calibration block;
3. any economic advantage should shrink further under 1.5x and 2x transaction-cost/slippage stress.

## Required protocol

For every candidate model/feature family:

- preserve PIT-safe feature timestamps;
- purge at least the full forward-label horizon between fit, calibration and outer test;
- select the policy from a predeclared finite threshold family using calibration data only;
- freeze the selected threshold for the entire outer test fold;
- aggregate outer-fold results without re-selection;
- preserve every tried threshold and its trial count;
- evaluate net returns at baseline, 1.5x and 2x costs;
- include execution-lag stress and turnover;
- compare against a frozen baseline using paired OOS observations;
- reserve the final untouched holdout for one-time confirmation.

## Status

**Pipeline finding: confirmed by code audit.**

**Model performance claim: blocked.** No numerical candidate is promoted from this audit because the existing `research_v2.py` sweep does not yet provide a clean nested-policy result artifact.

## References

- Kim, J. (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, SSRN 6508779.
- Li, S., Mulvey, J. M., & Fabozzi, F. J. (2026), *Smart Trading Rule: A Modular Machine Learning Framework for Portfolio Optimization with Transaction Costs*, Journal of Financial Data Science, 8(2), 145–175.
- Bysik, A. & Ślepaczuk, R. (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*, arXiv:2606.00060.
