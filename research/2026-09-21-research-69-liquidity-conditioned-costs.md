# Research 69 — Liquidity-Conditioned Costs and Economic Model Selection

**Date:** 2026-09-21  
**Hypothesis:** H120

## Literature synthesis

### Jo & Kim (2026), *Financial Analysts Journal*

The authors report that in-sample ML variable importance can overfit, while economic evaluation changes conclusions. They also find that conventional ML portfolios can be dominated by microcaps whose returns are expensive to trade. The implication for this project is that liquidity cannot be treated as a cosmetic post-hoc filter; it can change whether predictive content is economically usable.

### Bysik & Ślepaczuk (2026), BTC walk-forward study

The study evaluates hourly BTC forecasts under explicit fees, spreads and slippage. Naive sign strategies lose their economics under a 10-bps cost assumption, while a cost-aware forecast-magnitude filter reduces turnover and restores profitability in selected configurations. The reported XGBoost advantage is descriptive rather than formally established.

### Kim (2026), VALID framework

The study reports a disconnect between statistical validation and economic usefulness across hundreds of cryptocurrency strategy variants. It emphasizes that transaction costs and validation architecture must be part of the evaluation protocol rather than appended after model selection.

## New research implication

The project's cost model should itself be treated as a research-design variable. A flat cost can be acceptable as a controlled benchmark, but it is insufficient as the sole promotion environment when candidates have different turnover or liquidity exposure.

## Experimental protocol

Run the frozen candidate universe through identical OOS folds with four execution specifications:

- flat cost baseline;
- liquidity-conditioned spread/slippage;
- liquidity-conditioned impact/participation cost;
- 1.5x and 2x stressed versions of the variable-cost model.

The candidate model, features, portfolio construction, rebalance schedule and decision timestamps must not change across cost specifications.

## Leakage controls

Liquidity inputs must be available at the decision timestamp. Future volume, spread, realized volatility or end-of-day liquidity measures cannot enter an earlier decision. Cost calibration must occur inside training/validation windows only. OOS predictions and realized returns must be immutable and linked to the exact execution-cost specification used.

## Metrics

Primary: net OOS utility and candidate promotion stability.  
Secondary: turnover, gross-to-net decay, break-even cost, maximum drawdown, tail loss, and rank correlation of candidate performance across cost specifications.

## Expected outcomes

There are three informative outcomes:

1. **Stable ranking:** liquidity conditioning does not change candidate ordering — evidence that the existing flat-cost approximation is adequate for the tested universe.
2. **Ranking compression:** high-turnover candidates lose their apparent edge — evidence that execution economics were masking model fragility.
3. **Promotion reversal:** a previously promoted candidate fails variable-cost stress — direct evidence against that candidate's economic robustness.

No outcome is treated as evidence of alpha until the immutable OOS artifact chain and corrected forward-label-overlap validation are in place.

## Sources

- Jo, Y. & Kim, Y.H. (2026), *Rethinking Variable Importance in Machine Learning: An Economic Perspective on Empirical Asset Pricing*, Financial Analysts Journal, 82(2), 92–135. DOI: 10.1080/0015198X.2026.2621646.
- Bysik, A. & Ślepaczuk, R. (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*, arXiv:2606.00060.
- Kim, J. (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, SSRN 6508779.
