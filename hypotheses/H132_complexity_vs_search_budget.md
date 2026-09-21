# H132 — Model Complexity vs Research Search Budget

## Hypothesis
Higher model capacity can improve genuine OOS trading utility, but only when the added capacity is specified before evaluation and its advantage survives the same search budget, leakage controls and execution stresses. Apparent gains that arise only after a larger adaptive search should disappear under search-aware evaluation.

## Falsification
H132 is rejected if a higher-capacity model class does not beat the best lower-capacity class on untouched OOS net utility after selection adjustment, or if its advantage is reproduced by matched-noise/placebo searches.

## Experimental arms

A. Low-capacity baseline
B. Medium-capacity model
C. High-capacity model
D. Strong non-ML baseline
E. Matched-noise search control

All arms use identical timestamps, universe, label horizon, execution and cost engine.

## Required controls

- point-in-time feature availability;
- corrected purging/embargo for forward labels;
- immutable final OOS;
- full trial ledger and search-budget accounting;
- commission, spread, slippage, impact and borrow/funding;
- 1x / 1.5x / 2x cost stress;
- execution-lag perturbation;
- regime and tail slices;
- DSR/PBO/SPA or an equivalent selection-aware procedure;
- row-level prediction -> position -> execution -> turnover -> gross P&L -> cost -> net P&L artifact.

## Promotion threshold

Do not promote based on standalone Sharpe. Require incremental net OOS utility over the lower-capacity winner and strong baseline, plus stability across cost models and selection-aware evidence.

## Status

OPEN. No numerical result yet.
