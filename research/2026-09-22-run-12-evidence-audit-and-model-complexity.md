# Research 111 — Evidence Audit and Complexity-After-Information

Date: 2026-09-22

## Executive finding

The current repository contains a strong OOS evaluation contract and a large hypothesis ledger, but the accessible tree does not contain the immutable candidate-level OOS artifact required by that contract. There is therefore no project-level numerical model result that can honestly be promoted from this run.

This is a meaningful failure of research execution, not evidence that the model is bad.

## New literature

1. Saly-Kaufmann, Wood, Calliess & Zohren (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*. The benchmark evaluates linear models, recurrent models, transformers, state-space models and representation methods on daily futures from 2010–2025, and explicitly includes transaction-cost breakeven, downside/tail risk, seed robustness and computational efficiency. The project takeaway is to rank models jointly on OOS economics, friction tolerance and stochastic stability.

2. Kelly, Malamud, Schwab & Xu (NBER 35247, 2026), *Scaling Point-in-Time Language Models*. Their strict point-in-time economic evaluation reinforces the repository's information-cutoff invariant.

3. Cong, Tang & Wang (NBER 35195, 2026), *AlphaPortfolio*. The paper directly optimizes portfolio objectives and incorporates transaction costs. Its reported OOS results remain hypothesis-generating for this project until reproduced under our information and execution constraints.

4. Da, Nagel & Xiu (NBER 33070), *The Statistical Limit of Arbitrage*. Weak and rare alphas create a statistical limit even for optimal learners. This supports establishing adequate effective sample size and signal-to-noise before adding model complexity.

## Testable hypothesis

H162: once the information set and effective sample size are held fixed, increasing model/feature complexity will not reliably improve paired net OOS utility after realistic costs unless the improvement survives search-aware validation and stochastic-seed aggregation.

## Required experiment

Use one frozen PIT dataset and one frozen decision/execution contract. Compare a shrinkage/regularized linear baseline, tree-based nonlinear model, sequence model, and higher-capacity sequence/attention model. Record every trial. Evaluate paired candidate-minus-baseline net returns, 1x/1.5x/2x cost stress, seed dispersion, regime stability and selection-adjusted inference.

## Promotion rule

No candidate is promoted unless the immutable row-level artifact satisfies `experiments/oos_evaluation_contract.md` and all required evidence fields are present.

## Status

H162 registered. Numerical test: BLOCKED until the PIT-clean candidate artifact and executable evaluation pipeline are present. No performance claim is made.
