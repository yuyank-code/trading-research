# H84 — Cost-Model Uncertainty Robustness

## Hypothesis
A candidate strategy that is genuinely economically viable should retain its qualitative OOS conclusion across a pre-registered range of plausible transaction-cost and market-impact specifications. If profitability depends on one favorable cost model, the result is execution-model fragile and should not be promoted.

## Motivation
Fixed-bps costs are useful controls but can understate execution uncertainty. Almgren–Chriss frames execution as a trade-off between execution-cost risk and market impact; later work connects transaction costs with regularization and parameter uncertainty. Recent 2026 work on realistic market-impact environments reports that changing the cost model can materially change both trading behavior and the relative ranking of algorithms. Nonlinear price-impact research also motivates testing beyond purely linear costs.

## Test design
1. Freeze the candidate model, features, hyperparameters, signal horizon, universe, and confirmation dates before cost-model selection.
2. Evaluate identical OOS trades under a pre-registered cost grid:
   - proportional spread/commission: 0.5x, 1x, 2x baseline;
   - temporary impact: linear and square-root forms;
   - adverse execution/slippage stress: 0.5x, 1x, 2x baseline;
   - optional permanent-impact component where supported by the data.
3. Cost parameters must be estimated only from information available before each OOS decision; no confirmation-period calibration.
4. Report net Sharpe, Sortino, max drawdown, turnover, implementation shortfall, cost/gross-PnL ratio, and break-even cost.
5. Require sign consistency across cost specifications rather than optimizing a single cost curve.
6. Repeat the comparison against frozen simple benchmarks and matched-count placebo strategies.
7. Apply the existing multiple-testing controls (DSR/PBO, SPA/Reality Check, MCS) to the candidate-selection stage, not merely the final cost scenario.

## Falsification criteria
Reject H84 if:
- the candidate changes from economically positive to negative under modest, pre-specified cost perturbations;
- performance is concentrated in a single impact specification;
- the cost model uses future liquidity information;
- a placebo or benchmark shows comparable robustness;
- confirmation results require retuning cost assumptions.

## Required artifacts
- immutable candidate-level OOS predictions/returns;
- point-in-time spread/liquidity/volume inputs;
- versioned cost-model specification;
- trade-level execution ledger;
- scenario-level summary with no hidden optimization.

## Status
PRE-REGISTERED — no empirical result yet. Promotion remains blocked until corrected forward-label-overlap validation and the frozen candidate-level OOS matrix are available.
