# H61 — Research-design sensitivity and researcher-degrees-of-freedom gate

**Status:** pre-registered; not yet numerically executed

## Motivation

A strategy can survive ordinary walk-forward validation while remaining dependent on arbitrary research-design choices: training-window length, feature filters, portfolio construction, rebalance timing, universe rules, or objective function. If those choices were selected after inspecting outcomes, the apparent OOS result is still selection-contaminated.

Recent empirical work is especially relevant: a 2026 European Financial Management study evaluates 5,376 ML portfolios and finds that research-design choices can materially change reported returns; its nonstandard errors are substantially larger than conventional standard errors. This motivates treating research-design choices as part of the searched family rather than as innocuous implementation details.

## Hypothesis

**H61:** A candidate's economic edge should remain directionally and economically stable across a pre-declared neighborhood of reasonable research-design choices, without using the final confirmation period to select the design.

## Design perturbations

Freeze the model family and data version, then vary only pre-registered design dimensions:

- expanding vs fixed-length training windows;
- several plausible retraining frequencies;
- forecast horizon / holding-period alignment;
- signal normalization method, fitted fold-locally;
- rebalance schedule and minimum holding period;
- universe/liquidity filters;
- position-sizing cap and volatility target;
- cost/slippage assumptions.

Do not choose the best perturbation after looking at the final confirmation period.

## Validation

1. Point-in-time availability contract.
2. Fold-local stateful preprocessing.
3. Purged/embargoed walk-forward or CPCV where label spans overlap.
4. Nested selection: design choices are selected only inside the training/validation layer.
5. Untouched confirmation period.
6. Net returns after commissions, spread, slippage and market-impact proxy.
7. Report every tested design, including failures.
8. Apply family-level Reality Check/SPA and DSR/PBO where the trial family is large enough.
9. Repeat on zero-alpha null data with the same research freedom.

## Promotion criteria

A candidate is **not promoted** merely because the best design has a high Sharpe. Promotion requires that:

- the median and lower-tail OOS performance across the pre-registered design neighborhood remain economically meaningful;
- the edge survives adverse cost stress;
- the selected design does not owe its result to a single narrow choice;
- family-level inference is not rejected by data-snooping controls;
- the same search process does not routinely discover comparable winners under the null.

## Failure interpretation

If performance varies sharply with training window, rebalance timing, universe filter or another design choice, record that as evidence of research-design fragility even if the best configuration remains profitable.

## No-look policy

The final confirmation period is used once. It cannot be used to choose the model, design, cost assumptions, threshold, or reporting window.
