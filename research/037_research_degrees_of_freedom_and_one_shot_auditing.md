# Research 37 — Research Degrees of Freedom and One-Shot Auditing

Date: 2026-09-19

## Executive summary

The latest literature strengthens a central project conclusion: financial ML evaluation should be treated as an audit of the entire research process, not merely a model-score comparison. Recent work reports large false-positive rates when validation relies on conventional predictive metrics, while CPCV plus PBO/DSR can eliminate apparent discoveries. A new AlphaAudit benchmark explicitly freezes a one-shot verifier, uses a survivorship-free universe and audited candidate corpus, and treats leakage and multiple testing as first-class failure modes.

## High-quality evidence reviewed

1. **Kim (2026), Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading.** Monte Carlo experiments report 27–30% false-positive rates for AUC-only validation, reduced to zero in the reported experiments by CPCV with PBO. The paper also reports that multiple-testing survivors can still have PBO=1 and fail DSR. This is a strong warning against interpreting predictive metrics as economic evidence.
2. **Jain (2026), AlphaAudit.** Proposes an audit benchmark with a survivorship-free Indian-equity environment, verified transaction-cost model, leaky/clean fixtures, an audited 1,550-candidate corpus, and a frozen one-shot evaluation protocol. The useful transferable design principle is evaluator quarantine: the verifier must be fixed before candidates are judged.
3. **Mehndiratta (2026), More Strategies, Same Zero.** Studies LLM-scale alpha search and explicitly combines causal next-bar execution, transaction costs, worst-of-regime OOS scoring and a deflated-Sharpe multiple-testing haircut. The relevant lesson is that cheap strategy generation increases the multiple-testing burden rather than creating evidence of alpha.
4. **Saly-Kaufmann et al. (2026), Deep Learning for Financial Time Series.** Large-scale futures benchmarking evaluates OOS risk-adjusted performance together with significance, tail risk, break-even costs, random-seed robustness and computational efficiency. This supports the project's multidimensional evaluation rather than single-metric ranking.
5. **Cotturo, Liu & Proner (2026), Multifactor Timing with Deep Learning, Journal of Financial Econometrics.** Reports that a constrained deep-learning timing model retained an advantage under transaction-cost assumptions up to 14 bps in its factor-timing setting. This is useful positive evidence, but the asset/factor design differs from our FX objective, so it is not direct evidence for our candidate.

## New testable implication

The project should explicitly log the **research degrees of freedom** consumed by every candidate: feature set, label horizon, universe, model family, hyperparameters, holding period, threshold, execution rule, cost model and benchmark. A candidate selected after many unrecorded alternatives is not equivalent to a candidate surviving a small pre-registered search.

## Pipeline change

H86 adds a research-degrees-of-freedom audit and a one-shot confirmation gate. Candidate promotion now requires:

- immutable candidate/search ledger;
- corrected forward-label-overlap handling;
- point-in-time data and universe construction;
- purged/embargoed OOS evaluation;
- realistic costs/impact/borrow/capacity;
- frozen simple benchmarks;
- DSR/PBO and SPA/Reality Check;
- matched-count placebo/null controls;
- no confirmation-driven tuning.

## Important limitation

No new model-performance claim is made in this research pass. The repository still lacks the immutable candidate-level OOS prediction/return matrix required for trustworthy numerical promotion, and the previously identified forward-label-overlap validation issue must be corrected first.

## Sources

- https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6508779
- https://papers.ssrn.com/sol3/papers.cfm?abstract_id=7215321
- https://papers.ssrn.com/sol3/Delivery.cfm/7257858.pdf?abstractid=7257858&mirid=1
- https://arxiv.org/abs/2603.01820
- https://academic.oup.com/jfec/article/24/3/nbag006/8658726
