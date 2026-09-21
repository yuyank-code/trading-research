# H137 — Economic Feature Pruning vs Full Feature Sets

## Hypothesis
A feature set pruned using a pre-declared, training/validation-only economic rule will produce higher and more stable net out-of-sample utility than an otherwise identical full feature set, after realistic trading costs and selection controls.

## Null
Feature pruning does not improve net OOS utility, or any observed improvement disappears under the random-pruning placebo or outer OOS evaluation.

## Arms

- **A:** Full pre-specified feature set.
- **B:** Pre-declared economic-group pruning.
- **C:** Validation-only pruning using a fixed negative-value rule.
- **D:** Matched random-pruning placebo with the same feature-count reduction.

## Primary metric
Net final-OOS certainty-equivalent utility (or the project's pre-declared net utility metric), with Sharpe and drawdown as secondary diagnostics.

## Promotion criteria

The pruning arm must:

1. beat the full-feature baseline on untouched OOS net utility;
2. beat the matched random-pruning placebo;
3. survive 1x/1.5x/2x transaction-cost stress;
4. remain directionally stable across regimes and tail periods;
5. pass leakage and label-overlap audits;
6. show no dependence on one selected pruning threshold or architecture;
7. be evaluated with the complete prediction → position → execution → turnover → gross P&L → cost → net P&L ledger.

## Anti-overfitting constraints

- Pruning decisions are made only inside the inner training/validation layer.
- Outer OOS observations cannot influence feature ranking, thresholds or feature groups.
- Every attempted pruning rule counts against the research/search budget.
- No post-hoc feature deletion based on final OOS performance.
- The strong non-ML baseline remains a mandatory comparator.

## Falsification

Reject H137 if the full feature set is as good or better after costs, if pruning loses to the matched random placebo, or if the advantage vanishes after realistic execution costs or outer OOS evaluation.
