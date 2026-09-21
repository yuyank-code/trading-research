# Research 74 — Search-Aware Certification and the Cost of Selection

## Literature synthesis

### 1. Leakage-safe, search-aware strategy discovery (2026)

A recent 2026 study evaluates LLM-discovered trading strategies across point-in-time U.S. equity and multi-asset universes using realistic transaction, market-impact, and borrow costs. Its central methodological contribution is to treat strategy discovery as a search process rather than evaluating the selected winner as if it had been specified ex ante. The reported application rejects the discovered strategies after accounting for selection luck, predicted-rank degradation, and OOS collapse, while passive benchmarks remain certifiable.

This is not evidence that all ML trading strategies fail. It is evidence that the evidential bar must rise with search breadth and adaptiveness.

### 2. Empirical asset pricing via ML: research-design choices (European Financial Management, 2025/2026)

Lalwani, Meshram, and Jindal evaluate 5,376 ML portfolios across training windows, data filters, portfolio construction choices, and seven models. They find large variation induced by research design; nonstandard errors can be several times conventional standard errors, and only about one-third of portfolios remain significant after transaction costs. This supports explicit accounting for design-search uncertainty rather than reporting a single chosen specification.

### 3. Deep-learning financial time-series benchmark (2026)

Saly-Kaufmann et al. benchmark linear, recurrent, transformer, state-space, and representation-learning models on daily futures from 2010–2025. Evaluation includes statistical significance, downside/tail risk, break-even transaction costs, seed robustness, and computational efficiency. The key lesson for this project is not a particular winning architecture; it is the breadth of the evaluation contract required before a model ranking is credible.

### 4. ML Bitcoin trading under transaction costs (2026)

Bysik and Slepaczuk evaluate XGBoost, LSTM, and iTransformer using a 27-fold hourly walk-forward BTC protocol. Naive sign-based trading fails under 10-bps costs, while a cost-aware execution filter can improve selected configurations. The authors do not establish formal statistical dominance for XGBoost. This reinforces the distinction between forecast quality and net tradable economics.

### 5. Cost-aware multiwindow FX evaluation (2026)

Grigoriev, Musaev, and Grigorieva evaluate transparent multiwindow ensembles on synchronized one-minute FX quotes using nonoverlapping walk-forward blocks and a utility objective incorporating transaction costs, drawdown, and turnover. This supports testing time-scale diversity and cost-aware execution while avoiding an architecture-only search.

## Implication for the project

The project's accumulating hypotheses, design perturbations, gates, cost models, and baselines create a nontrivial research-selection process. H125 therefore adds search-aware certification as a promotion gate.

The project must distinguish:

- performance of a predeclared hypothesis;
- performance discovered after adaptive search;
- performance of the selected winner after accounting for the search that produced it.

Only the third is relevant for deciding whether the research program has produced a credible deployable candidate.

## New testable prediction

If the candidate's economic edge is genuine, search-aware correction should reduce statistical confidence but should not eliminate the candidate's incremental net OOS advantage versus strong frozen baselines. If the edge is primarily selection luck, the advantage should shrink toward zero under the same correction and null workflow.

## Decision

H125 committed. No candidate is promoted until the immutable OOS accounting artifact exists and forward-label-overlap validation has been corrected.
