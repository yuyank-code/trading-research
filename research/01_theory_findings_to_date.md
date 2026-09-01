# Theoretical Research — Findings to Date

## Purpose

Consolidated record of the meaningful theoretical findings developed before this repository was initialized. This file is a synthesis, not a claim that every source in the literature has been exhausted.

## Momentum and trend

Momentum has strong historical empirical support, but the literature also documents momentum crashes and substantial conditionality. Therefore the research target is not simply `momentum predicts returns`; it is whether momentum remains useful after conditioning on volatility, liquidity, valuation, market state and implementation costs.

**Research direction:** test medium-term momentum, time-series trend, and momentum interactions separately, with pre-specified horizons and regime analysis.

## Reversal / mean reversion

Short-horizon reversal is a major competing explanation to momentum. It may reflect temporary price pressure, liquidity provision, bid/ask effects or behavioral overreaction. It must therefore be tested with realistic spread/slippage assumptions and distinguished from mechanical microstructure effects.

**Research direction:** compare short-horizon reversal against longer-horizon momentum and test whether the apparent edge survives execution costs.

## Factor investing

CAPM and multifactor models provide useful economic baselines, but factor definitions and empirical explanations remain contested. The project should compare hand-specified economic factors with statistically extracted factors and test incremental information rather than assume any published factor is universally valid.

## Liquidity and transaction costs

Liquidity is both a risk characteristic and an implementation constraint. Transaction costs can eliminate high-turnover anomaly profits. Portfolio construction should therefore incorporate costs from the beginning, including spread, slippage, market impact, turnover, borrow and capacity where applicable.

**Research direction:** compare immediate rebalancing, no-trade bands and partial adjustment.

## Statistical arbitrage

Pairs, cointegration, relative value and cross-sectional arbitrage require careful treatment of non-stationarity, structural breaks, estimation windows and execution costs. Apparent mean reversion can disappear after costs or after a regime change.

**Research direction:** test stability and break sensitivity before optimizing entry/exit rules.

## Volatility and derivatives

Volatility is both a predictor and a risk state. Options introduce additional information such as implied volatility, skew and term structure, but also much more difficult execution and data-quality issues. Options should be treated as a separate research branch until the core equity/time-series framework is validated.

## Macro and cross-asset research

Returns may be influenced by rates, inflation, currencies, commodities, credit and policy regimes. Relative-return prediction may be more learnable than absolute-return prediction in some settings. Cross-asset experiments should preserve publication timestamps and avoid hindsight regime labels.

## Behavioral finance

Underreaction, overreaction, attention, herding, disposition effects and limits to arbitrage provide competing economic explanations for return patterns. These mechanisms should be tested as explanations rather than used as post-hoc stories for successful backtests.

## Machine learning

ML can capture nonlinear interactions that linear factor models miss. Evidence also indicates that regularization can be especially valuable when signals are weak and predictors are numerous. Model choice should therefore proceed from strong baselines toward nonlinear models, not from a presumption that deep learning is superior.

**Benchmark ladder:** naive → linear → Ridge/Elastic Net → interactions → random forest/boosting → regularized neural network → sequence/transformer models.

## High-dimensional models

Recent asset-pricing work provides evidence that high-dimensional factor models can sometimes improve out-of-sample performance. This is an important counterweight to simplistic anti-complexity rules. Complexity should be treated as an experimental variable and must demonstrate incremental OOS value.

## Theory-guided ML

Synthetic data generated from structural economic models may improve learning under small samples or unstable environments. This is a later-stage research direction, after ordinary statistical baselines have been established.

## Portfolio and risk theory

Prediction is not the same as portfolio construction. The project must separately test position sizing, risk constraints, volatility targeting, turnover controls, drawdown behavior and capacity. A model with slightly better prediction can still produce a worse portfolio after costs and concentration.

## Regimes and structural breaks

Financial relationships can change through time. Information-processing improvements can reduce some historical anomalies. Regime detection must therefore be causal-in-time: regimes used for a prediction must be inferred using information available at that date.

## Causal inference

Predictive association does not establish mechanism. Causal methods may help distinguish structural relationships from correlations, but they should be treated as an additional research layer rather than a guarantee of trading profitability.

## Backtesting and overfitting

The project treats look-ahead bias, survivorship bias, data snooping, multiple testing, selection bias and model-search overfitting as first-class risks. Purged/embargoed validation, untouched final tests, PBO/DSR-style diagnostics and experiment ledgers are required for serious claims.

## Critical implementation lesson

An earlier model runner used six-bar forward labels but did not fully purge training observations whose labels overlapped the test period. That contaminates the evidence even when the feature matrix itself uses only past data. This has been recorded as a project failure and is a prerequisite to resolve before trusting older model results.

## Overall conclusion

The theoretical evidence does not point to one universally best strategy. It points toward a research process that tests economically motivated hypotheses, permits complexity when justified, and rejects results that fail point-in-time, OOS, cost, robustness or multiple-testing gates.
