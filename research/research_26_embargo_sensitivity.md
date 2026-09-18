# Research 26 — Embargo Sensitivity as a Validation-Falsification Test

## Literature synthesis

Financial machine-learning research increasingly treats temporal leakage and repeated validation as first-order threats rather than implementation details. The 2026 VALID framework reports that apparent statistical success can coexist with failure under combinatorial purged cross-validation and PBO, and emphasizes fixed reporting order and economic gates. A 2025 Review of Financial Studies replication also shows that look-ahead bias can create large apparent machine-learning trading alpha that disappears after correcting the information set. These results motivate testing the stability of the validation protocol itself.

## New research question
Does the candidate ranking and economic conclusion remain stable when the embargo is increased beyond the minimum needed to prevent label/feature overlap?

## Why this matters
Choosing an embargo is a potential hidden researcher degree of freedom. If one particular embargo produces the favorable result while nearby defensible choices reverse it, the strategy may be exploiting boundary contamination or validation sensitivity rather than robust predictability.

## Experimental design
Run the exact frozen candidate family under the H75 embargo grid. Do not re-optimize features or hyperparameters for each embargo. Preserve the same OOS dates and execution model as far as the larger embargo permits.

For each candidate, retain fold-level observations for:
- net return;
- Sharpe and Sortino;
- maximum drawdown;
- turnover;
- break-even transaction cost;
- rank among candidates;
- number of observations/folds retained.

Report both pooled and fold-level stability. Any material loss of folds caused by larger embargoes must be disclosed rather than silently compensated by changing the split design.

## Expected interpretation
- **Stable:** economic conclusion and relative ranking remain broadly consistent across defensible embargoes.
- **Fragile:** performance or rank changes substantially with modest embargo changes.
- **Invalid:** a result relies on an embargo below the causal minimum or disappears once the minimum valid embargo is enforced.

## Relationship to existing gates
H75 does not replace purging, DSR/PBO, SPA/Reality Check, Model Confidence Sets, null falsification, cost stress, capacity analysis, or the untouched confirmation period. It tests whether the validation conclusion is itself robust.

## Current result
No numerical result is claimed. The repository still requires the frozen candidate-level OOS prediction/return matrix before empirical promotion decisions can be made.

## Sources
- Kim, J. (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, SSRN 6508779.
- Zhang, Y., Zhu, Y., Linnainmaa, J. T. (2025), *Man versus Machine Learning Revisited*, Review of Financial Studies, 38(12), 3768–3790.
- López de Prado, M. (2018), *Advances in Financial Machine Learning*, Wiley — purging and embargo concepts.
