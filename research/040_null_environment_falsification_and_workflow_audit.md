# Research 40 — Null-Environment Falsification and Workflow Audit

## Date
2026-09-19

## Question
Can the trading research pipeline itself be falsified before trusting real-market candidate results?

## Literature update
A 2026 preprint, *Spurious Predictability in Financial Machine Learning*, proposes falsification audits against synthetic zero-predictability reference classes and microstructure placebos. Its central methodological point is that adaptive specification search can generate significant walk-forward results even under martingale-difference nulls, so the complete workflow should be tested for false-discovery generation rather than only correcting the final Sharpe ratio. citeturn0search12

A separate 2026 study on hidden leakage reports large Sharpe inflation from forward contamination in rolling feature normalization, illustrating that apparently rigorous OOS evaluation can remain invalid when feature construction violates information availability. citeturn0search9

The 2024 controlled comparison of backtest-overfitting methods finds CPCV materially stronger than conventional approaches on PBO/DSR in synthetic financial environments, supporting its continued use here, but it does not remove the need for structural and null-workflow tests. citeturn0search10

Recent cost-aware crypto research reaches a complementary execution conclusion: frictionless predictive improvements can disappear after realistic costs, while cost-aware signal filtering can materially reduce turnover; however, reported gains remain configuration-sensitive and formal dominance is not established. citeturn0academia36turn0search0

A 2026 large-scale financial time-series benchmark likewise evaluates models using OOS risk-adjusted performance, downside/tail risk, break-even transaction costs and seed robustness, reinforcing the project's multi-dimensional evaluation standard. citeturn0academia34

## Pipeline change
Research 40 turns the null from a passive statistical control into a **workflow-level acceptance test**. The same research code path must be run against four pre-specified null/reference environments:

1. IID return null.
2. Block/bootstrap null preserving local dependence without predictive alignment.
3. Causal feature-permutation null.
4. Microstructure/execution placebo preserving turnover and holding mechanics while removing predictive alignment.

The test must preserve the same search budget, model families, purging/embargo, costs, slippage, benchmark comparisons, DSR/PBO and statistical decision rules used for real candidates.

## Why this is a meaningful upgrade
The project's earlier H88 adversarial fixtures test whether explicit future information can be detected. H89 goes one level higher: even with clean-looking information boundaries, the **whole discovery workflow must fail gracefully on data containing no exploitable predictive structure**. This directly targets adaptive search and evaluator-induced false positives.

## Planned experiment
For each null environment, generate a pre-registered number of independent realizations and run the full candidate-search protocol without changing the search budget. Record:

- best gross and net Sharpe;
- benchmark-relative return;
- turnover and cost burden;
- maximum drawdown and expected shortfall;
- DSR/PBO;
- SPA/Reality Check outcomes;
- MCS membership;
- number of candidates crossing each promotion threshold;
- distribution of the selected-best statistic.

The key comparison is the **selected-best null distribution**, not the performance of one arbitrary null strategy. This accounts for the same selection pressure that exists in real research.

## Decision rule
If null runs repeatedly cross promotion thresholds, the workflow is considered falsified and real-data model promotion is blocked until the cause is identified. If the null suite behaves as expected, that is evidence about pipeline validity only; it is **not** evidence of market alpha.

## Current empirical status
No trustworthy candidate-level OOS matrix is currently present in the repository, and the README still records the forward-label-overlap correction as a prerequisite. Therefore this run does **not** claim a model-performance result. The contribution is a concrete, literature-backed falsification experiment that can be executed once the corrected OOS matrix and candidate runner are available.

## Conclusion
The highest-value next empirical step is no longer another architecture search. It is to prove that the existing research machinery cannot manufacture attractive strategies from controlled nulls. Only after that test passes should candidate models consume additional confirmation budget.
