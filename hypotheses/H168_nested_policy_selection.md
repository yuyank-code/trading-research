# H168 — Nested Policy Selection Beats Single-OOS Threshold Selection

## Hypothesis

A trading policy whose execution threshold is selected only inside a development/calibration block will produce lower but more honest OOS performance than selecting the best threshold on the same outer OOS period used for final reporting.

## Null

There is no systematic inflation from threshold selection on the outer OOS sample after accounting for the number of thresholds tried.

## Candidate protocol

- finite predeclared threshold family: 0.55, 0.57, 0.60, 0.63, 0.66;
- model fit: strictly before calibration and separated by the full label horizon;
- calibration: most recent development block only;
- threshold selection: calibration net Sharpe only, with a fixed tie-break;
- outer test: threshold frozen for the complete fold;
- final holdout: untouched until all development choices are frozen.

## Comparators

A. current single-OOS threshold sweep;
B. nested threshold selection;
C. fixed threshold baseline;
D. cost-aware threshold using a predeclared break-even rule.

## Primary metric

Paired outer-OOS net return difference versus the frozen baseline, evaluated before and after 1.5x and 2x cost/slippage stress.

## Secondary metrics

Sharpe, maximum drawdown, turnover, trade count, profit factor, threshold stability across folds, and the fraction of folds in which the selected policy beats the fixed baseline.

## Promotion rule

No candidate is promoted unless the nested policy remains positive on paired incremental net utility, survives 1.5x and 2x costs, has no material execution-lag collapse, and passes the project's search-aware inference and final-holdout gates.

## Falsification

H168 is supported against the null if the single-OOS sweep shows materially larger performance than nested selection and that gap is stable across folds/cost stress. The pipeline itself is considered suspect if the single-OOS method generates strong alpha while nested selection does not.
