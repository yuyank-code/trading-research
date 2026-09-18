# H72 — Research-Process Stability Under Repeated Evaluation

## Motivation

The project has accumulated multiple validation gates, but repeated research passes can themselves become a source of selection bias. The next audit therefore treats the *research protocol* as the object of testing.

## Hypothesis

If a candidate trading edge is genuine, its promotion decision should remain materially stable when the same pre-specified evaluation is repeated across independent time partitions, random seeds, and reasonable implementation choices. If the edge is mostly research-selection noise, the selected winner and/or sign of OOS performance will be unstable.

## Test design

1. Freeze the feature set, label horizon, cost model, search budget, and promotion criteria before evaluation.
2. Generate candidate-level OOS return series for every searched candidate; never retain only the winner.
3. Repeat the complete pipeline across non-overlapping chronological confirmation blocks.
4. Repeat model training across multiple random seeds where stochastic algorithms are used.
5. Compare the selected candidate's rank, net Sharpe, drawdown, turnover, break-even cost, and sign consistency across blocks.
6. Apply the existing PBO/DSR and SPA/Reality-Check controls to the full candidate family rather than to the winner alone.
7. Run the same protocol on synthetic zero-alpha data as a falsification control.

## Primary decision rule

Do not promote a model if its apparent advantage depends on one chronological block, one random seed, one cost specification, or one arbitrary implementation choice. A model that is statistically indistinguishable from a simpler baseline remains unpromoted.

## Literature basis

Bailey et al. show that repeated configuration search materially increases the probability of backtest overfitting and propose CSCV/PBO for measuring it. Recent ML trading research also demonstrates that transaction-cost assumptions can change both absolute performance and model rankings, reinforcing the need to treat the evaluation protocol itself as part of the robustness test.

## Status

Pre-registered. Numerical evaluation is blocked until the repository contains the frozen candidate-level OOS prediction/return matrix and the corresponding point-in-time market/execution data.
