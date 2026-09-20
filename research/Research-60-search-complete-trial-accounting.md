# Research 60 — Search-Complete Trial Accounting

**Date:** 2026-09-20

## Executive finding

Recent research strengthens a point that is easy to miss in otherwise rigorous backtests: the statistical penalty must reflect the **research process that produced the reported candidate**, not merely the final parameter grid.

A 2026 study of LLM-driven strategy discovery reports that every strategy evaluation should be recorded and search intensity incorporated into inference; it also demonstrates that statistical correction alone does not rescue a deliberately leaky oracle. The study evaluates hundreds of point-in-time instruments with transaction, impact, and borrow costs and reports rejection of the discovered strategies after leakage and search-aware evaluation.

A separate 2026 robustness framework proposes combining Deflated Sharpe Ratio, Probability of Backtest Overfitting, Superior Predictive Ability, minimum track-record length, and regime stability into an auditable validation layer. Importantly, its authors present it as a reporting/validation device rather than evidence that the score itself predicts future profits.

Large-scale 2026 financial ML benchmarking also reinforces the need to evaluate statistical significance, downside/tail risk, break-even transaction costs, and random-seed robustness rather than selecting models by average Sharpe alone.

## Testable hypothesis

**H110:** Complete immutable accounting of the search history will materially reduce false promotions relative to counting only final-stage candidates, while preserving detection of genuinely injected signal.

## Protocol

Use two identical evaluation paths over the same frozen candidate universe.

### Path A — incomplete accounting

Count only candidates that reach final scoring/promotion.

### Path B — complete accounting

Count every attempted evaluation, including:

- model architectures;
- feature sets;
- hyperparameter configurations;
- forecast thresholds;
- execution rules;
- benchmark choices;
- random seeds;
- failed or aborted evaluations;
- candidates rejected before final scoring.

For each candidate store an immutable record containing candidate ID, parent experiment, timestamp, code/data version, dataset hash, configuration hash, seed, OOS window, status, and resulting prediction/return artifact reference.

## Statistical evaluation

Run DSR, PBO/CSCV and SPA/reality-check style inference under both accounting paths. Estimate both nominal and effective trial counts because highly correlated candidates do not constitute independent bets.

Run the same protocol on:

1. pure null/placebo returns;
2. synthetic data containing a known moderate edge;
3. realistic historical data under frozen execution costs.

The confirmation period remains untouched by all exploratory search.

## Acceptance criteria

The pipeline passes H110 only if:

- false-promotion rate falls materially on null/placebo data;
- known injected signal remains detectable at an appropriate power level;
- final confirmation data are never used to choose the candidate;
- the complete trial ledger can reconstruct the exact search path;
- reported inference is unchanged when the ledger is independently replayed.

## Failure interpretation

If incomplete and complete accounting produce materially different promotion decisions, that is evidence that prior selection-adjusted significance was under-penalized.

If complete accounting still permits frequent placebo promotions, the problem is deeper than trial counting and the validation stack must be tightened before any model is promoted.

## Current project implication

No alpha conclusion is changed by this research. The project still requires an immutable candidate-level OOS prediction/return matrix and corrected forward-label-overlap validation before historical numerical results are treated as trustworthy.

## Sources

- Gençay (2026), *What survives honest evaluation? Leakage-safe, search-aware assessment of LLM-driven trading strategy discovery*, arXiv:2608.27734.
- Santoni, Jouanne & Scullin (2026), *Equity Strategy Backtesting: Luck or Edge? The MinervaScore as a Statistical Robustness Grade*, arXiv:2608.23808.
- Saly-Kaufmann et al. (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*, arXiv:2603.01820.
