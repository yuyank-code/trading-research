# Research 63 — Complexity Tax and Shrinkage Baselines

**Date:** 2026-09-20

## Executive finding
A fresh 2026 preprint provides a useful negative-control design for our project: in a leak-free, cost-aware large-cap US-equity benchmark, the promoted MLP only marginally exceeded a no-ML Black-Litterman prior while incurring more than three times the cumulative transaction cost; an equally weighted portfolio was also close in Sharpe. The authors conclude that much of the observed risk-adjusted performance came from covariance regularization and Bayesian shrinkage rather than predictive content. This is a preprint/working-paper result and is treated as hypothesis-generating, not established fact.

## Why this matters
Our research program has repeatedly tested model complexity, cost sensitivity, and benchmark-relative alpha separately. This evidence motivates combining them into a single decisive question: does a complex model add incremental economic information once the portfolio construction and shrinkage machinery is held fixed?

## New hypothesis
H113 tests whether nonlinear/complex models outperform a transparent shrinkage/prior-only baseline after identical risk controls and realistic costs. A candidate that wins only before costs, only under a favorable optimizer, or only against a weak benchmark is not considered evidence of model alpha.

## Experimental design
- Freeze the universe and point-in-time data snapshot.
- Construct a transparent prior-only/shrinkage baseline.
- Add regularized linear and nonlinear candidates without changing the portfolio engine.
- Fit every transformation and covariance object only on information available at each decision time.
- Apply purging/embargo to overlapping labels.
- Preserve immutable OOS predictions, positions, turnover, gross returns, each cost component, and net returns.
- Stress transaction costs/slippage using the existing preregistered grid.
- Compare incremental utility, not only Sharpe or forecast loss.
- Count all model/feature/portfolio/threshold/validation attempts in the search ledger.

## Literature synthesis
The large-scale 2026 deep-learning benchmark emphasizes OOS risk-adjusted performance, significance, tail risk, break-even transaction costs, and seed robustness rather than prediction metrics alone. The 2026 BTC walk-forward literature similarly reports that naive sign strategies can fail at 10 bps while cost-aware filtering can materially reduce turnover; however, the reported XGBoost advantage is descriptive rather than statistically established. A 2026 FX paper likewise uses net-of-cost utility, turnover penalties, volatility gating, and nonoverlapping walk-forward evaluation. These findings converge on the same principle: the execution/portfolio layer must be held constant when attributing incremental value to the predictive model.

## What is not established
No new numerical OOS alpha is claimed in this research pass. The repository still requires the immutable candidate-level OOS matrix and corrected forward-label-overlap validation before legacy model results can be treated as trustworthy.

## Decision
Add H113 to the candidate promotion queue. Do not promote any model from this literature review alone.
