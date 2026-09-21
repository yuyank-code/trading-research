# H129 — Cost-Model Rank Stability

## Hypothesis

If a candidate's economic advantage is genuine rather than an artifact of an overly favorable execution assumption, its incremental net out-of-sample utility should remain positive relative to the frozen baseline across a pre-specified family of plausible transaction-cost and market-impact models.

## Falsification

Reject H129 if the candidate's advantage disappears, reverses, or becomes statistically/economically negligible under reasonable alternative cost specifications, especially when the alternatives use execution-time liquidity information and nonlinear impact.

## Arms

1. Candidate model
2. Strong frozen baseline
3. Matched-noise/placebo candidate

All arms use identical timestamps, portfolio construction, execution timing and cost calculations.

## Cost family

- fixed bps;
- spread + slippage;
- liquidity-conditioned spread/slippage;
- nonlinear market impact;
- 1.5x and 2x stress for every specification.

## Required OOS outputs

- row-level prediction and position;
- executed price/price impact;
- turnover and participation;
- commission, spread, slippage, impact and borrow/funding separately;
- gross and net P&L;
- break-even cost;
- incremental utility versus baseline;
- stability/rank statistics across cost models.

## Controls

- point-in-time features;
- purge + embargo for overlapping labels;
- fold-local cost calibration;
- untouched final holdout;
- no final-period tuning;
- selection-aware inference and placebo search.

## Promotion gate

No promotion unless the candidate remains economically superior to the frozen baseline across the pre-declared cost family and passes leakage, statistical and selection controls.
