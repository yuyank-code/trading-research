# Research 51 — Power-Calibrated Promotion and Minimum Detectable Edge

## Question

How much confirmation evidence is actually required to distinguish a candidate's incremental net trading edge from noise or economically trivial performance?

## Literature synthesis

Recent research on leakage-safe automated strategy discovery shows that credible certification of moderate edges requires explicit accounting for search intensity, realistic transaction/impact/borrow costs, and complementary out-of-sample controls. A 2026 large-scale financial time-series benchmark evaluates models using statistical significance, downside/tail risk, breakeven transaction costs, random-seed robustness, and computational efficiency rather than Sharpe alone. A 2026 crypto-factor audit reports large inflation of naive Sharpe relative to nested walk-forward, explicit-cost, multiplicity-adjusted evaluation.

These results motivate a separate power layer: after leakage and multiplicity are controlled, the remaining question is whether the confirmation sample can resolve an economically meaningful candidate-minus-baseline effect with adequate probability.

## Proposed experiment

Build a synthetic calibration suite with the same temporal dependence, volatility clustering, turnover, and execution-cost model as the real pipeline. Plant known incremental effects at several magnitudes, including zero and economically trivial effects.

Run the exact frozen promotion procedure without changing search budget, purging/embargo, seed accounting, cost model, or confirmation protocol.

Record:

- empirical power by planted effect size;
- false-promotion rate under zero/trivial effects;
- confidence-interval coverage;
- effective sample size under serial dependence;
- break-even transaction cost;
- sensitivity to overlapping labels/positions;
- degradation across regimes.

## Decision use

The result becomes a calibration report for the promotion gate. A candidate cannot be promoted merely because p < alpha or DSR exceeds a threshold. Its uncertainty interval must also support a pre-registered economically meaningful incremental edge.

## Status

Design committed. No empirical power result is claimed until the controlled planted-effect suite and immutable candidate-level OOS matrix are executable.

## Sources

- Saly-Kaufmann, Wood, Peter-Calliess & Zohren (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*.
- Gençay (2026), *What survives honest evaluation? Leakage-safe, search-aware assessment of LLM-driven trading strategy discovery*.
- Nefedov (2026), *How Much Sharpe is Illusory? Quantifying Backtest Overfitting in Crypto Factor Strategies*.
- Bailey et al. (2016), *Backtest Overfitting in Financial Markets*.
