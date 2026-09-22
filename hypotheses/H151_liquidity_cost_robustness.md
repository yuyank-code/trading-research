# H151 — Liquidity/Cost Robustness Is Necessary for Economic Promotion

Date: 2026-09-22

## Hypothesis

A candidate trading signal that remains economically useful after point-in-time universe controls and realistic execution-cost stress is more likely to represent robust tradable structure than one whose performance is concentrated in illiquid assets or disappears under modest cost increases.

## Test

Compare each candidate model under:

- baseline tradable universe;
- liquidity-filtered universe;
- 1x base cost;
- 1.5x base cost;
- 2x base cost;
- one-bar execution lag stress where applicable.

Do not re-optimize the model for each scenario.

## Promotion rule

A model cannot be promoted if its apparent advantage is driven primarily by microcaps/illiquid observations, disappears at 1.5x cost, or requires scenario-specific retuning. Promotion requires positive incremental net utility over the strong baseline on untouched OOS data and stability across the pre-registered stress grid.

## Leakage controls

Universe membership, liquidity measures, spreads, and execution variables must be timestamped by their earliest usable time. No future volume, future spread, revised membership, or future execution outcome may enter features, labels, or selection.

## Null/control arms

Include a turnover-matched or exposure-matched baseline so that a lower-cost strategy is not automatically interpreted as superior prediction. Preserve all failed configurations.

## Evidence standard

Use purged/embargoed validation where labels overlap; keep the final OOS period untouched; account for the full search budget; and report multiplicity-aware inference. H151 is falsified if the cost/liquidity robustness disappears after correcting the forward-label-overlap issue.
