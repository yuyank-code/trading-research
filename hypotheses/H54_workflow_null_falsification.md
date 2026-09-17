# H54 — Workflow-level null falsification

## Status
Proposed hard validation gate. No model promotion from this hypothesis alone.

## Question
Can the complete trading research workflow manufacture an apparently profitable strategy when directional predictability is removed but realistic financial dependence is retained?

## Motivation
Recent financial-ML research argues that adaptive specification search can create significant walk-forward evidence under zero-predictability nulls. The relevant object to falsify is therefore the whole workflow: feature construction, validation, model search, calibration, execution policy, costs, and selection—not only the final predictor.

Supporting literature:
- Spurious Predictability in Financial ML (2026), arXiv:2604.15531: workflow-level falsification against synthetic nulls and measurement of selection-induced inflation.
- Bysik & Ślepaczuk (2026), arXiv:2606.00060: hourly BTC ML trading; naive direction trading fails at 10 bps while cost-aware forecast filtering can recover selected configurations, but formal model dominance is not established.
- Saly-Kaufmann et al. (2026), arXiv:2603.01820: large-scale financial time-series benchmark emphasizing OOS risk-adjusted returns, downside/tail risk, break-even transaction costs, and seed robustness.
- Bailey, Borwein, López de Prado & Zhu: probability of backtest overfitting / CSCV framework.

## Null construction
Use synthetic series that preserve empirically relevant properties of the real asset while removing directional predictability. At minimum preserve:
- volatility clustering;
- heavy-tailed return distribution;
- realistic return autocorrelation where present;
- calendar/session structure where appropriate.

The null must not leak future information into feature construction or parameter fitting.

## Critical requirement
The null receives the same researcher degrees of freedom as the real experiment:
1. same feature library;
2. same model families and hyperparameter budget;
3. same walk-forward/purging/embargo rules;
4. same calibration and selective-execution choices;
5. same spread, fees, slippage, and latency assumptions;
6. same candidate-selection rule;
7. same number of trials recorded in the multiplicity ledger.

## Evaluation
For every null workflow winner, record:
- gross and net return;
- annualized Sharpe and Sortino;
- maximum drawdown;
- turnover and trade count;
- break-even transaction cost;
- performance by time block/regime;
- probability of backtest overfitting (PBO/CSCV where implemented);
- deflated Sharpe ratio using the complete trial count;
- seed sensitivity.

Compare the distribution of null-selected performance with the real-data candidate, not only the single best null run.

## Falsification criteria
The research workflow is considered falsified if it routinely produces economically attractive OOS results on zero-predictability data, especially if those results survive the same selection-adjustment procedures used on real data.

A passing result does NOT prove alpha. It only removes one important class of workflow-level false-positive risk.

## Promotion implication
No candidate can be promoted solely because it beats the null. It must additionally pass executable-horizon alignment, realistic cost/slippage stress, leakage audit, purged/embargoed OOS evaluation, multiplicity adjustment, and untouched confirmation.

## Reproducibility
The experiment must emit a machine-readable artifact containing the null-generation seed/configuration, trial registry, split definitions, model/policy configurations, costs, and all OOS metrics. The final confirmation set must remain untouched during null calibration and candidate selection.
