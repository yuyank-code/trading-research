# Research 49 — Pre-registration, Search Intensity, and Evidence Burden

## Research question

Does limiting adaptive search before confirmation evaluation improve the reliability of discovered trading signals after realistic execution costs and selection-aware inference?

## Evidence reviewed

- Bailey & López de Prado (2014), *The Deflated Sharpe Ratio*: multiple testing and non-normal returns inflate reported Sharpe; trial count must affect inference.
- Arian, Norouzi Mobarekeh & Seco (2024), *Backtest overfitting in the machine learning era*: controlled synthetic experiments report CPCV outperforming conventional OOS procedures on overfitting diagnostics.
- Santoni, Jouanne & Scullin (2026), *Equity Strategy Backtesting: Luck or Edge?*: a composite robustness score combining DSR, PBO, SPA, minimum track record and regime stability is useful as an audit/reporting layer, but a preregistered real-market test found no significant forward relationship with subsequent performance (Spearman rho 0.013, one-sided permutation p=0.40).
- Gençay (2026), *What survives honest evaluation?*: leakage-safe, search-aware LLM strategy discovery recorded every strategy evaluation and applied realistic transaction, impact and borrow costs; passive benchmarks were certified while the searched LLM-discovered strategies were rejected under the stated evaluation framework. The study also demonstrates that statistical correction does not repair a structurally leaky information set.

## Pipeline change

The project now distinguishes **hypothesis budget** from **adaptive-search budget**. A trial ledger must record every candidate-producing evaluation, including failed candidates and seed variants. Confirmation-period data remain untouched until the arm is frozen.

The research pipeline should report:

1. pre-registered hypothesis count;
2. adaptive candidate count;
3. effective independent-trial estimate where applicable;
4. all candidate OOS predictions in immutable form;
5. net performance after spread/commission/slippage/impact/borrow;
6. DSR/PBO and other selection-aware tests;
7. baseline incrementality;
8. confirmation rank degradation;
9. cost and latency sensitivity.

## Important limitation

No new alpha result is claimed in this pass. The repository's existing blocker remains: corrected forward-label-overlap validation and an immutable candidate-level OOS prediction/return matrix must be completed before historical model-performance numbers can be treated as trustworthy.

## Interpretation

The literature increasingly supports treating strategy discovery as an experiment with a measurable search budget, not as a sequence of independent backtests. This makes negative results first-class evidence and reduces the risk that increasingly sophisticated search simply increases the chance of finding a lucky historical winner.
