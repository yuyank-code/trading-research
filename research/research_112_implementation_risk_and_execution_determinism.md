# Research 112 — Implementation Risk and Execution Determinism

Date: 2026-09-22

## Question

Can two implementations of the same trading rule produce materially different conclusions once transaction costs and execution conventions are applied?

## Literature

Yin, Miki, Lesnichenko & Gural (2026), *Implementation Risk in Portfolio Backtesting*, formalize implementation risk: different backtest engines can diverge even when the logical strategy is identical. Their benchmark finds zero-cost agreement but nonzero-cost divergence, with larger differences for high-turnover strategies. This implies execution semantics are part of the experiment, not a post-processing detail.

Koijen & Levy (2026), *Assessing the Benefits of Optimized Agentic AI Systems for Asset Pricing*, emphasize real-time information availability as a requirement for valid historical evaluation. Kelly et al. (2026), *Scaling Point-in-Time Language Models*, similarly show that point-in-time construction can preserve economic signal while preventing temporal leakage.

## Testable hypothesis H163

**H163 — Execution-Determinism / Implementation-Risk Test**

For every promoted candidate, independently implement the identical signal and portfolio rule in two execution paths. Under zero costs they should match to numerical tolerance. Under realistic costs they must remain within a pre-registered implementation uncertainty interval and must not change the sign of candidate-minus-baseline economic conclusions.

### Pass criteria

1. Same input artifact hash and same decision timestamps.
2. Zero-cost equity curves agree within 1e-10 relative tolerance.
3. Cost-inclusive cumulative net return difference <= 25 bps annualized OR <= 0.5% cumulative, whichever is stricter for the test horizon.
4. Candidate-minus-baseline sign is unchanged across implementations.
5. No implementation changes are permitted after observing OOS results.

### Stress matrix

- commissions: 0, 1x, 1.5x, 2x
- spread/slippage: 0, base, 1.5x, 2x
- execution: next-bar, explicit delay stress
- turnover: natural and turnover-matched placebo

### Failure interpretation

If implementations disagree materially, the model is **BLOCKED**, not rejected. The implementation ambiguity must be resolved before interpreting alpha.

## Decision rule

Do not promote a model unless it passes PIT information lineage, purge/embargo, search-adjusted inference, seed stability, realistic cost stress, and H163 implementation-determinism checks.

## Status

Protocol committed. No candidate is promoted by this research note.
