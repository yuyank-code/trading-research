# H75 — Embargo-Length Sensitivity and Validation Fragility

## Status
Pre-registered hypothesis. No pass/fail result yet.

## Motivation
The project has previously identified forward-label overlap at walk-forward boundaries as a material validation risk. A single embargo choice can itself become a hidden researcher degree of freedom. If conclusions change materially when the embargo is varied over a defensible range, the apparent edge is validation-fragile.

## Hypothesis
A genuinely predictive strategy should retain broadly consistent out-of-sample conclusions across embargo lengths that are sufficient to remove label/feature overlap, while a leakage-sensitive strategy will show unusually large degradation or rank changes as the embargo is tightened.

## Test
For every frozen candidate and every chronological OOS fold:

1. Derive the maximum information horizon from the exact feature/label construction.
2. Define a minimum valid embargo from that horizon.
3. Evaluate a pre-specified sensitivity grid: minimum valid embargo, 1.5x, 2x, and 3x the minimum where sample size permits.
4. Keep model hyperparameters, features, candidate family, costs, execution rules, and final untouched confirmation block fixed.
5. Record OOS net return, Sharpe, Sortino, maximum drawdown, turnover, break-even cost, and candidate rank for each embargo setting.
6. Compare the distribution of fold-level results rather than selecting the best embargo.

## Acceptance criteria
- No embargo setting below the causal minimum is allowed.
- The primary result must be reported at the pre-specified minimum valid embargo.
- A strategy is validation-robust only if conclusions are qualitatively stable across the sensitivity grid and no isolated embargo produces the promotion decision.
- Any material rank reversal or sign reversal is recorded as a fragility finding, not tuned away.

## Leakage / overfitting controls
- Chronological splits only.
- Purging and embargo are applied before fitting or feature selection.
- Final confirmation data remain untouched until all research decisions are frozen.
- The sensitivity grid is fixed before observing OOS results.
- Apply existing DSR/PBO, SPA/Reality Check, MCS, null-workflow, cost, and capacity gates.

## Primary outcome
Validation stability, not maximum performance. The hypothesis passes only if the candidate's economic conclusion is insensitive to reasonable embargo perturbations.
