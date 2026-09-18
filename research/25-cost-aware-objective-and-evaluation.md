# Research 25 — Cost-Aware Model Selection

## Literature update

A 2026 benchmark of deep learning for financial time series evaluates daily futures across commodities, equity indices, bonds, and FX from 2010–2025. Its evaluation explicitly includes OOS risk-adjusted performance, downside/tail risk, break-even transaction costs, random-seed robustness, and computational efficiency. This supports treating economic utility and robustness as first-class evaluation targets rather than optimizing prediction metrics in isolation.

A 2026 study of hourly BTC trading under transaction costs reports a disconnect between prediction improvements and net trading performance: naive sign-based strategies fail under a 10-bps cost assumption in its setting, while cost-aware forecast-magnitude filtering can materially reduce turnover and recover profitability in selected configurations. These results are not evidence of FX alpha, but they motivate a directly testable FX experiment.

## Research implication

The next model-selection layer should distinguish forecast quality from executable economic value. A model should not receive selection credit for improving MSE/MAE/directional accuracy if the improvement does not survive the execution layer.

## Experiment

For frozen causal features, compare model selection by:

- forecast loss;
- gross trading utility;
- net trading utility after explicit execution costs.

Use identical model families, search budgets, folds, seeds, and final confirmation periods. Cost assumptions must be determined without using the final OOS block.

## Robustness matrix

Every selected candidate is evaluated under:

- base execution costs;
- +25%, +50%, +100% adverse costs;
- delayed execution;
- liquidity/impact-conditioned costs where data permit;
- volatility-normalized sizing where pre-registered;
- synthetic zero-alpha controls.

Statistical controls remain DSR/PBO, SPA/Reality Check, Model Confidence Set, and rank/seed/period stability.

## Decision rule

Promotion requires a net OOS advantage that is economically meaningful, statistically defensible, and stable across plausible execution assumptions. If the net OOS distributions cannot distinguish complex and simple candidates, retain the simpler model.

## Current result

No numerical result is claimed in this research pass. The repository README still identifies the corrected-validation requirement and the need for frozen candidate-level OOS data before historical model results can be treated as trustworthy.
