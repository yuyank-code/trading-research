# H109 — Cost-Stress Survival of Candidate Alpha

## Status
Pre-registered / awaiting immutable candidate-level OOS return matrix.

## Motivation
Recent 2026 evidence shows a recurring disconnect between predictive metrics and tradable net returns: complex ML forecasts can lose their apparent edge once commissions, spread and slippage are applied, while simple cost-aware execution rules can matter more than architecture changes. See Bysik & Ślepaczuk (2026) and Huang, Wang & Jiang (2026).

## Hypothesis
A genuinely economically useful candidate should retain positive benchmark-relative OOS alpha across a pre-specified range of plausible execution-cost assumptions, with degradation that is economically coherent rather than an abrupt collapse at a single assumed cost.

## Test
For every frozen candidate and the transparent baseline, replay the identical immutable OOS prediction/return stream under cost multipliers:

- 0.5x reference cost
- 1.0x reference cost
- 1.5x reference cost
- 2.0x reference cost
- 3.0x reference cost

The reference model must include commissions/fees, bid-ask spread, slippage, market impact where applicable, borrow/funding where applicable, and turnover/capacity constraints.

Report at each multiplier:
- annualized net return;
- Sharpe and downside risk;
- max drawdown;
- turnover;
- benchmark-relative alpha;
- break-even cost (cost at which alpha reaches zero).

## Leakage / selection controls
The cost grid is fixed before looking at candidate results. No candidate-specific cost multiplier may be selected. The same cost assumptions and execution semantics must be applied to all candidates and benchmarks. If execution parameters are optimized, that optimization is a separate trial family and must enter the multiple-testing ledger.

## Promotion criterion
Cost robustness is necessary but not sufficient. A candidate must satisfy the project's existing leakage, purging/embargo, placebo, power, multiplicity, seed-stability and benchmark-relative gates. A candidate that is profitable only at an unusually optimistic cost assumption is rejected as economically fragile.

## Falsification
Reject H109 if candidate alpha disappears at the reference cost or under a modest pre-specified adverse-cost stress, or if placebo strategies exhibit comparable cost robustness.
