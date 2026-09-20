# H104 — Benchmark-Relative Incremental Alpha

## Status

Proposed; not yet numerically evaluated.

## Question

Does a candidate ML trading signal retain economically and statistically meaningful net out-of-sample performance after controlling for transparent benchmark exposures, or is the apparent edge primarily a repackaging of known systematic returns?

## Motivation

Recent asset-pricing research shows that apparently sophisticated ML strategies can overlap substantially with established anomaly/factor portfolios, while out-of-sample comparisons against strong ML and factor benchmarks can materially change the interpretation of alpha. Interacting Anomalies (Review of Asset Pricing Studies, 2025) explicitly compares a simple out-of-sample strategy with ML anomaly strategies and reports that benchmark controls reduce, but do not necessarily eliminate, its alpha. A 2026 working paper on fund-return prediction likewise reports strong contemporaneous explanatory power without robust forward trading signal after multiple-testing adjustment.

The project therefore needs a direct incremental-value test rather than treating raw Sharpe as evidence of novel alpha.

## Falsifiable hypothesis

H1: After point-in-time construction, purged/embargoed OOS validation, realistic execution costs, and complete trial accounting, the candidate's residual return relative to pre-specified transparent benchmarks has positive expected net value and survives the project's promotion gates.

H0: The candidate's apparent net performance is fully explained by the benchmark exposures and/or disappears after cost and multiplicity adjustment.

## Required benchmarks

At minimum, use only benchmarks that are frozen before confirmation:

1. market/broad-risk benchmark;
2. simple momentum/trend benchmark where economically appropriate;
3. transparent volatility/risk-control benchmark;
4. the project's current production baseline;
5. any directly comparable published strategy used to motivate the candidate.

## Protocol

1. Freeze the candidate predictions before benchmark comparison.
2. Estimate benchmark exposures using only information available by each OOS decision time.
3. Evaluate raw and residual net returns on identical OOS dates.
4. Apply the same commissions, spread, slippage, impact, borrow and capacity assumptions to every strategy where applicable.
5. Preserve the complete candidate-by-date return matrix.
6. Apply the existing label-overlap, purging/embargo, placebo, seed, search-ledger, DSR/PBO and power gates.
7. Report incremental annualized return, Sharpe, downside risk, turnover, drawdown, cost break-even and benchmark alpha with uncertainty intervals.
8. Treat benchmark specification as pre-registered search space; changing it after seeing results counts as a new trial.

## Failure criteria

Reject the hypothesis if:

- residual net performance is not positive and economically material;
- the candidate loses its edge under realistic cost/slippage assumptions;
- benchmark selection materially changes the conclusion without a pre-specified reason;
- placebo workflows produce comparable residual alpha;
- the result fails multiplicity-adjusted significance or power requirements;
- any information-set or label-overlap violation is detected.

## Promotion rule

No candidate is promoted because it has positive raw alpha. Promotion requires independent evidence of incremental, net, out-of-sample value after all existing hard gates pass.
