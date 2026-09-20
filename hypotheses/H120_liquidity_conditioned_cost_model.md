# H120 — Liquidity-Conditioned Cost Model vs Flat Transaction Costs

**Status:** preregistered / untested  
**Date:** 2026-09-21

## Hypothesis

A model ranking produced with a flat transaction-cost assumption is unstable once execution costs are conditioned on observable liquidity. Candidate models that appear attractive under constant costs will lose more net OOS utility when spread/slippage/impact rise with turnover and market illiquidity.

## Motivation

Recent 2026 asset-pricing evidence finds that ML portfolio performance can be concentrated in microcaps and costly-to-trade stocks, and that economic restrictions materially change which predictors appear useful. A separate 2026 cost-aware BTC study finds that gross predictive improvements can disappear after realistic trading frictions. These results motivate testing the execution-cost model itself rather than treating costs as one fixed scalar.

## Test design

Compare the same frozen candidate set under:

1. flat baseline cost;
2. liquidity-conditioned spread/slippage;
3. liquidity-conditioned impact increasing with participation/turnover;
4. 1.5x and 2x stressed versions of (2)-(3).

All signal, model, portfolio, rebalance and OOS dates remain identical.

## Required controls

- point-in-time liquidity features only;
- no use of future volume, spread or realized volatility;
- purged/embargoed validation where labels overlap;
- cost parameters frozen before final OOS;
- candidate-level prediction, position, turnover, cost and realized-return artifacts;
- complete trial accounting;
- placebo signals with the same execution engine.

## Primary outcome

**Net OOS utility after execution costs**, plus the rank correlation of candidate models between flat-cost and liquidity-conditioned evaluation.

## Falsification criteria

Reject H120 if model rankings and promotion decisions remain materially unchanged under all pre-specified liquidity-conditioned and cost-stressed specifications.

## Promotion rule

No candidate may be promoted because it survives only the flat-cost specification. Promotion requires survival under the liquidity-conditioned base case and both cost-stress cases, without leakage or selection-control violations.
