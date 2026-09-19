# Research 39 — Adversarial Leakage and Structural Validation

## Literature synthesis

The recent literature strengthens a key methodological conclusion: statistical corrections are necessary but cannot substitute for structural leakage prevention. A 2024 Knowledge-Based Systems study comparing out-of-sample validation methods found CPCV materially more resistant to backtest overfitting than conventional walk-forward procedures in controlled experiments, with lower PBO and stronger DSR statistics. The result supports purging/embargoing and multi-path evaluation, but does not prove that CPCV alone prevents implementation leakage.

A 2026 study of leakage-safe, search-aware trading-strategy discovery is more directly relevant. It reports that a deliberately leaky oracle can show extreme Sharpe while surviving DSR and PBO correction. Its central lesson is that look-ahead exclusion must be enforced by the data/feature registry itself, while trial counts must also be recorded for search-aware inference. The same work evaluates strategies with realistic transaction, impact and borrow costs and reports rejection of discovered strategies despite strong historical search results.

A 2026 large-scale financial time-series benchmark further supports evaluating models using OOS risk-adjusted performance, statistical significance, tail risk, break-even transaction costs, seed robustness and computational efficiency rather than prediction metrics alone.

## New testable research question

Can the trading-research evaluator reliably reject deliberately future-leaked fixtures before statistical performance is used for promotion?

## Experiment

Build paired clean/adversarial fixtures. Inject future one-period return, future volatility, and future cross-sectional rank into otherwise identical feature tables. Preserve timestamps and schema so the only intended difference is information availability.

Run the same frozen evaluator through:

- chronological walk-forward;
- purged/embargoed validation;
- CPCV where implemented;
- realistic transaction costs and slippage;
- benchmark-relative reporting;
- DSR/PBO and multiple-testing accounting.

The evaluator must fail closed when a feature's availability timestamp exceeds the decision timestamp. Performance-based heuristics are not acceptable as the primary detector.

## Expected outcome

This experiment is a pipeline-security test. Passing means the evaluator is robust to known adversarial leaks; it does not establish trading alpha. Failing blocks candidate promotion.

## Sources

- Arian, Norouzi Mobarekeh & Seco, *Backtest overfitting in the machine learning era*, Knowledge-Based Systems, 2024, DOI 10.1016/j.knosys.2024.112477.
- Bailey & López de Prado, *The Deflated Sharpe Ratio*, Journal of Portfolio Management, 2014.
- Gençay, *What survives honest evaluation? Leakage-safe, search-aware assessment of LLM-driven trading strategy discovery*, 2026 preprint.
- Saly-Kaufmann et al., *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*, 2026 preprint.

## Status

Design committed. No empirical alpha conclusion and no candidate promotion until the immutable candidate-level OOS matrix and corrected forward-label-overlap validation are available.
