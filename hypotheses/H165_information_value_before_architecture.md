# H165 — Information Value Before Architecture

## Hypothesis
After enforcing point-in-time availability, label-overlap purging/embargo, realistic execution costs and a frozen baseline, incremental economic value from a candidate information set should be established before additional model complexity is allowed to consume search budget.

## Falsification
The hypothesis is falsified if a higher-capacity model consistently produces significant incremental net OOS utility over the frozen baseline even when the corresponding simple/regularized model does not, under the same PIT-safe features, execution assumptions, search budget, and untouched holdout.

## Test design

Compare, on identical observations:

1. frozen baseline;
2. regularized linear model;
3. tree ensemble;
4. sequence/deep model;
5. higher-capacity model only if the preceding information test passes.

All candidates must use:

- identical PIT-safe feature snapshots;
- identical label definitions;
- purge and embargo sized to the forward horizon;
- identical execution timestamps;
- explicit commissions, spread, slippage and impact;
- 1x, 1.5x and 2x cost stress;
- fixed search/trial budget;
- seed aggregation for stochastic models;
- paired candidate-minus-baseline inference;
- untouched final holdout;
- trial-count / multiplicity accounting;
- turnover and capacity checks.

## Primary endpoint
Paired net OOS utility improvement over the frozen baseline, not prediction accuracy and not raw in-sample Sharpe.

## Secondary endpoints
Breakeven cost, turnover, drawdown/tail risk, regime stability, seed dispersion, and implementation agreement.

## Promotion rule
No candidate is promoted unless it demonstrates incremental net OOS value, survives the pre-specified cost and execution stresses, passes leakage audits, and remains credible after accounting for the complete research/search history.

## Rationale
Recent 2026 evidence repeatedly finds a gap between predictive metrics and net trading economics, while large-scale studies show that research-design choices and search multiplicity can materially alter reported performance. Therefore model complexity should be conditional on demonstrated information value rather than used as the first optimization target.
