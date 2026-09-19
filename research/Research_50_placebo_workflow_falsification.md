# Research 50 — Placebo-Workflow Falsification

## Question

Can the full trading-research workflow distinguish genuine predictive structure from artifacts that arise under zero-alpha and placebo data?

## Literature synthesis

Recent 2026 work on spurious predictability reports that adaptive specification search can create significant walk-forward evidence even under martingale-difference nulls. Its proposed response is a falsification audit against synthetic zero-predictability and microstructure-placebo reference classes. This is a useful complement to selection-adjusted metrics because DSR/PBO operate on performance selection, while a placebo audit tests whether the workflow itself manufactures apparent predictability.

A 2026 BTC walk-forward study independently reinforces the need for economic rather than predictive evaluation: naive sign-based ML strategies failed after a 10-bps transaction-cost assumption, while cost-aware filtering restored profitability only in selected configurations; descriptive XGBoost superiority over neural models was not supported as formal statistical dominance. A separate 2026 live-deployment report found a large gap between strong walk-forward predictive metrics and near-random live trading outcomes, highlighting execution mismatch and non-stationarity as deployment risks.

## Pipeline change

Add a mandatory placebo stage before any candidate can enter confirmation:

- zero-alpha synthetic returns;
- feature-shuffled placebos;
- timestamp-preserving target permutations;
- deliberately irrelevant control features;
- matched search budgets and random seeds.

Record every attempted placebo trial in the committed trial ledger. Run the same purging/embargo, feature-transform causality checks, execution-cost frontier, baseline comparison, DSR/PBO, SPA/Reality Check and MCS gates used for real candidates.

## Decision criterion

The workflow passes only if its observed placebo-promotion rate is consistent with the pre-specified false-positive tolerance. A failure is treated as a pipeline defect, not as an interesting trading result.

## Important limitation

This research pass adds the hypothesis and audit design but does not claim that the placebo suite has already been executed. The repository still requires the immutable candidate-level OOS prediction/return matrix and corrected forward-label-overlap validation before numerical candidate promotion.

## Sources

- Nikolopoulos (2026), “Spurious Predictability in Financial Machine Learning,” arXiv:2604.15531.
- Bysik & Ślepaczuk (2026), “Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting,” arXiv:2606.00060.
- Zhai (2026), “The Prediction Paradox: Why Machine Learning Models Fail to Predict Cryptocurrency Prices in Live Trading,” SSRN 6566940.
