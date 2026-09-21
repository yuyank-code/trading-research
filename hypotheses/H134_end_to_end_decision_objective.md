# H134 — End-to-End Decision Objective vs Two-Stage Prediction

## Claim to test

A model trained directly on the downstream trading objective can improve net out-of-sample utility relative to a matched model trained only for return prediction and converted to positions afterward.

## Null

There is no incremental economic value from direct decision-aware training once the two-stage model receives the same information, portfolio constraints, execution model, search budget, and OOS evaluation.

## Alternative

Decision-aware training produces higher candidate-minus-baseline net OOS utility and/or a larger break-even cost buffer without materially higher turnover.

## Required controls

- Purged/embargoed walk-forward validation.
- Fold-local preprocessing and hyperparameter selection.
- Immutable final OOS period.
- Identical information cutoff and execution timing.
- Full transaction-cost stack: commission, spread, slippage, impact and borrow/funding where relevant.
- 1x / 1.5x / 2x cost stress.
- Execution-lag perturbation.
- Strong non-ML baseline.
- Matched-capacity placebo or shuffled-label control.
- Trial/search ledger and selection-aware inference.

## Promotion rule

Do not promote unless the decision-aware model's incremental net OOS advantage survives realistic costs, cost-model perturbation, lag stress, and selection correction, while remaining stable across economically distinct subperiods.

## Current status

UNTESTED. Numerical results are blocked until the repository's immutable prediction-to-execution-to-net-return artifact and corrected forward-label-overlap validation are operational.
