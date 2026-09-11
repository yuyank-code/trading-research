# Nested Benchmark and Cost-Aware Promotion Gate — 2026-09-11

## Meaningful update

The production engine in `yuyank-code/bitcoin-ml-trading` currently trains three classifiers (logistic, random forest, HistGradientBoosting) and averages their probabilities in each walk-forward experiment. It evaluates seven feature-source configurations. The label is a six-bar forward-close direction and training is purged by six bars. The backtest enters on the next bar and applies explicit fees/slippage; ambiguous stop/target bars are now recorded. This makes the experiment substantially more auditable, but it still does not resolve the label/execution horizon mismatch. See `production_research.py` at the current main-branch revision.

## New literature signal

Bysik & Ślepaczuk (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting* (arXiv:2606.00060), evaluates roughly 70,000 hourly BTC-USDT observations with 27 walk-forward folds. Their key result for this project is methodological: naive sign-based trading fails at 10 bps, while cost-aware forecast filtering can rescue selected configurations; model differences are not formally established as statistically dominant.

Huang, Wang & Jiang (2026), *Research on Machine Learning High-Frequency Trading Strategies Under Transaction Cost*, reports a similar prediction-to-trading disconnect and emphasizes explicit fees, spread and slippage plus walk-forward evaluation. Treat this as supporting evidence rather than definitive proof because it is a recent venue and should not outrank stronger peer-reviewed/primary sources.

Kim (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, reports substantial false-positive risk from AUC-only validation and argues for CPCV/PBO plus economic validation. Treat this as a preprint/working-paper signal, not settled consensus.

## H47 — Incremental predictability beyond a nested naive benchmark

A candidate model must be compared with a properly nested naive/random-walk benchmark before model complexity is treated as evidence of edge.

Required tests:

1. Random-walk / no-change benchmark.
2. Historical-mean/drift benchmark where economically appropriate.
3. Production ensemble.
4. Candidate model.
5. Clark–West for nested forecast comparison.
6. Diebold–Mariano/HLN where the loss-comparison assumptions are appropriate.
7. Economic comparison after the same fees, spread and slippage.
8. Multiple-testing correction across the full registered candidate family.

A better AUC alone is insufficient. A better Sharpe alone is insufficient. Promotion requires incremental predictive information plus economically meaningful, cost-aware OOS performance.

## H48 — Cost-threshold stability

The current engine already rejects trades when expected gross payoff does not exceed a cost threshold. This should be treated as a pre-registered execution policy and evaluated over a fixed cost grid rather than optimized on the final holdout.

Required grid: 0.5x, 1x, 1.5x, 2x and 3x baseline all-in execution cost, with the same frozen signals. Report turnover, net return, Sharpe/Sortino, max drawdown, trade count and break-even cost. Do not select the best cost cell.

## Critical implementation observation

The production engine currently creates `future_return = Close[t+6]/Close[t]-1` and purges six bars, but the trading simulator monetizes the signal from the next bar's OHLC. Therefore the predictive event and executable event remain different objects. The next implementation gate is to define explicit `signal_time`, `entry_time`, and `event_end_time`, then compare 1-bar, six-bar and event/triple-barrier labels under the same frozen execution rules.

## Literature interpretation

Recent 2026 evidence reinforces a conservative research hierarchy: transaction costs can erase apparent ML alpha; cost-aware filtering may matter more than architectural complexity; and high predictive metrics do not guarantee live economic value. These findings support the pipeline order rather than proving that any particular model will work.

## Decision

No model promotion and no new profitability claim from this run. The repository does not currently expose a committed frozen OOS report/dataset for an independently reproducible numerical rerun. The next valid numerical run must produce and preserve the OOS predictions, trade ledger, equity curve and exact configuration manifest together.

## Sources

- Bysik & Ślepaczuk (2026), arXiv:2606.00060.
- Huang, Wang & Jiang (2026), Journal of the European Academy Open University, 2(4), DOI 10.71411/eaou.2026.v2i4.1672.
- Kim (2026), SSRN 6508779, *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*.
- Clark & West (2007), *Approximately Normal Tests for Equal Predictive Accuracy in Nested Models*, Journal of Econometrics.
- Diebold & Mariano (1995), *Comparing Predictive Accuracy*, Journal of Business & Economic Statistics.
