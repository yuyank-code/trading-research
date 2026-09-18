# Research 20 — Selective deployment and double out-of-sample validation

## Date
2026-09-18

## Evidence reviewed

1. Mroziewicz & Ślepaczuk (2026), *A Novel Approach to Trading Strategy Parameter Optimization, using Double Out-of-Sample Data and Walk-Forward Techniques*. The study evaluates 81 combinations of walk-forward window lengths on intraday Bitcoin data and reports that performance depends materially on the chosen window; it emphasizes a final single-time OOS test.
2. Guo (2026), *When Not to Trade: Leakage-Aware Selective Machine Learning for Factor Rotation*. The preprint proposes a rolling-origin deployment gate that abstains when a learned signal does not beat a transparent fallback by a calibrated margin. Reported results are hypothesis-generating and are not treated as evidence for FX profitability.
3. Bysik & Ślepaczuk (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*. Their walk-forward experiments report that naive sign trading can fail under 10 bps costs and that cost-aware forecast thresholds can materially reduce turnover in selected configurations.
4. Saly-Kaufmann et al. (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*. The benchmark evaluates OOS risk-adjusted returns, tail risk, break-even costs, seed robustness and computational efficiency rather than prediction accuracy alone.

## Research implication

The project should distinguish **forecast quality** from **deployment quality**. A model may have useful conditional information but still lose money when every prediction is converted into a trade. A selective gate is therefore a testable economic layer, not a new forecasting model.

## Experimental design

Use a frozen model and preserve a strict hierarchy:

`training -> validation/calibration -> untouched OOS confirmation`

Within each rolling-origin fold, estimate the cost hurdle only from information available at the decision time. Never tune the abstention threshold against the final OOS period.

Primary comparison:

`always trade` vs `cost-aware abstain` vs `fixed threshold` vs `matched-count placebo abstention`.

All variants must use identical signals and execution assumptions. Report gross and net results, turnover, trade count, drawdown, break-even cost, and performance under adverse cost stress.

## Current conclusion

No empirical FX result is claimed yet. The repository does not contain the frozen OOS prediction/return matrix required for a numerical H65 evaluation. This note therefore records literature evidence and a falsifiable protocol only.

## References

- Mroziewicz, T. & Ślepaczuk, R. (2026). SSRN 6217160 / arXiv 2602.10785.
- Guo, Y. (2026). SSRN 7021298, *When Not to Trade: Leakage-Aware Selective Machine Learning for Factor Rotation*.
- Bysik, A. & Ślepaczuk, R. (2026). arXiv 2606.00060.
- Saly-Kaufmann, A., Wood, K., Peter-Calliess, J. & Zohren, S. (2026). arXiv 2603.01820.
