# Research 78 — Cost-Model Rank Stability and Execution-Model Risk

**Date:** 2026-09-21  
**Status:** hypothesis-generating; no candidate promotion

## Question

Can a trading candidate retain its economic advantage when transaction costs are modeled as a function of execution conditions rather than as a single fixed bps charge?

## Literature synthesis

1. **Huang, Wang & Jiang (2026), Journal of the European Academy Open University** study hourly BTC trading with fees, spread and slippage in walk-forward evaluation. They report a large gap between predictive accuracy and net trading performance and find that simple transaction-cost-aware filtering can matter more than iterating model architectures. This is useful evidence for testing execution separately from forecast quality, but it is not treated as proof of generalizable alpha.  
   https://ojs.shiharr.com/index.php/eaou/article/view/1672

2. **Huang, Wang & Jiang (2026), transaction-cost-aware filtering** evaluates XGBoost, LSTM and iTransformer with 10 bps full-dimensional costs and a 27-fold walk-forward framework. Their reported results show naive strategies becoming uneconomic after costs and cost-aware filtering materially reducing turnover. The magnitude of the reported returns is treated cautiously because it is a single crypto market and requires independent replication.  
   https://ojs.shiharr.cn/index.php/eaou/article/view/1673

3. **Riera Abbade & Reali Costa (2026), MACE** shows in RL environments that replacing fixed costs with nonlinear market-impact models can materially change both trading behavior and relative algorithm rankings. The important methodological implication is that cost-model choice is itself an evaluation dimension.  
   https://arxiv.org/abs/2603.29086

4. **Jo & Kim (2026), Financial Analysts Journal** show that in-sample feature importance can overfit and that economically meaningful evaluation requires attention to costly segments such as microcaps. This supports testing whether a model's apparent advantage survives execution restrictions rather than relying on predictive or attribution metrics alone.  
   https://doi.org/10.1080/0015198X.2026.2621646

5. **Kim (2026), Beyond Accuracy** reports that permutation-based success can still fail combinatorial purged cross-validation and economic tests, and that net Sharpe deteriorates with trading frequency. This supports treating cost and validation as joint gates.  
   https://doi.org/10.2139/ssrn.6508779

## New hypothesis

A candidate that is genuinely economically useful should preserve its **relative ranking versus strong baselines** across a reasonable family of pre-specified execution-cost models.

A candidate whose ranking changes materially when moving from fixed bps to liquidity/impact-aware costs should be classified as execution-model dependent, not robust.

## Protocol

For every frozen OOS prediction stream, compute identical positions under:

- fixed cost baseline;
- spread + slippage model;
- liquidity-conditioned spread/slippage;
- nonlinear market-impact model;
- 1.5x and 2x stressed versions of each model.

The cost model must use only information available at execution time. Any parameters estimated from historical market data are fit inside the training/validation period for each fold.

Report:

- gross return;
- each cost component separately;
- turnover and participation;
- net return and Sharpe;
- break-even cost;
- candidate-vs-baseline incremental utility;
- rank correlation of candidates across cost models;
- worst-case and median net utility across models.

No cost model may be selected after viewing final OOS results.

## Leakage / overfitting controls

- purged and embargoed folds for overlapping labels;
- fold-isolated cost-parameter estimation;
- immutable final OOS period;
- no retuning after final-OOS inspection;
- matched placebo strategy evaluated through the same cost pipeline;
- complete row-level accounting: information cutoff -> prediction -> position -> execution -> turnover -> gross P&L -> costs -> net P&L.

## Current result

**No numerical result is claimed.** The repository still lacks the complete immutable candidate-level OOS accounting artifact and corrected forward-label-overlap implementation required for trustworthy model performance claims.

## Decision rule

A candidate can only advance if its incremental net OOS utility remains positive versus the frozen baseline across the pre-declared cost family and survives multiple-testing/selection controls. Otherwise the apparent edge is rejected as cost-model sensitive.
