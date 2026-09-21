# H140 — Stochastic Seed Robustness vs Best-Seed Performance

## Hypothesis

For stochastic trading models, the median and lower-tail net OOS performance across independently trained seeds will provide a more reliable estimate of deployable economic value than the best-seed result.

## Null

After correcting for seed multiplicity, the candidate model has no systematic net OOS advantage over the strong non-ML baseline.

## Experiment arms

1. Locked candidate model, independent seeds.
2. Strong non-ML baseline, deterministic or independently repeated where applicable.
3. Matched-capacity candidate with shuffled labels/features as a placebo.
4. Best-seed reporting as a deliberately marked selection-bias diagnostic, not a promotion criterion.

## Controls

- exact point-in-time information timestamps;
- corrected purged/embargoed validation for overlapping labels;
- untouched outer OOS;
- fixed architecture/features/objective after development lock;
- no seed chosen using outer OOS;
- complete trial ledger including every seed and failed run;
- commission, spread, slippage, nonlinear market impact, borrow and capacity where relevant;
- 1x/1.5x/2x cost stress;
- execution-lag stress;
- regime and tail-period analysis;
- statistical comparison against the strong baseline;
- no promotion from best-seed performance alone.

## Promotion rule

A candidate can only be considered robust if the pre-specified aggregate OOS distribution (primary: median net utility; secondary: lower-tail utility and fraction of seeds beating baseline) shows a meaningful advantage over the baseline and remains positive under cost and execution stress. The best seed is reported only as a multiplicity diagnostic.

## Falsification

Reject H140 if the candidate's apparent advantage disappears when evaluated across independent seeds, or if only a small minority of seeds generate the claimed edge.

## Current status

Untested. The repository's corrected forward-label-overlap requirement and immutable prediction-to-net-P&L ledger remain prerequisites for numerical conclusions.
