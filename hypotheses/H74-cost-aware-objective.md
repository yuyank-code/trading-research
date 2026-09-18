# H74 — Optimize for Net OOS Utility, Not Forecast Loss

## Status
Pre-registered research hypothesis. No empirical pass claimed.

## Motivation
Recent 2026 evidence indicates that improvements in prediction error or directional accuracy can fail to survive transaction costs, while cost-aware trade filtering can be more economically important than incremental model complexity. A large 2026 financial time-series benchmark also evaluates models using OOS risk-adjusted returns, downside/tail risk, break-even transaction costs, seed robustness, and computational efficiency rather than prediction loss alone.

## Hypothesis
For the same causal information set and candidate model family, selecting/training with an execution-aware objective based on net trading utility should generalize better out of sample than selecting only by forecast loss.

## Test design
Compare three selection objectives:
1. forecast loss only;
2. gross trading utility;
3. net trading utility after spread, commission, slippage and impact.

Keep the candidate architecture/search budget fixed. Any threshold or sizing parameter must be selected inside the training/validation partition only.

## Required controls
- point-in-time features and labels;
- purging and embargo for overlapping forward labels;
- untouched final confirmation block;
- fixed candidate/search budget;
- realistic execution costs and adverse cost stress;
- synthetic zero-alpha/null workflow;
- DSR/PBO and family-level SPA/Reality Check;
- Model Confidence Set where multiple candidates remain statistically indistinguishable;
- seed and period stability checks.

## Primary endpoints
- net OOS Sharpe/Sortino;
- maximum drawdown and tail loss;
- break-even transaction cost;
- turnover;
- implementation shortfall;
- stability of model rank across OOS blocks.

## Falsification
H74 fails if cost-aware selection does not improve net OOS economics, or if its apparent advantage disappears under plausible cost stress, independent confirmation data, or multiplicity controls.

## Important limitation
This repository currently lacks the frozen candidate-level OOS prediction/return matrix needed for numerical execution of this test. Therefore this document is a protocol, not a profitability result.
