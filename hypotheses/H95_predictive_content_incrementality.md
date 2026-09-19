# H95 — Predictive-Content Incrementality

## Claim
A candidate ML signal should only be considered economically useful if its incremental contribution survives comparison with a transparent, pre-specified economic baseline under the same universe, portfolio construction, execution model, costs, and OOS splits.

## Motivation
Recent quantitative research increasingly finds that model complexity and prediction metrics can look strong while the incremental trading value after costs is small. A 2026 leak-free large-cap benchmark reported only a marginal ML improvement over a no-ML baseline while incurring substantially higher transaction costs. A 2026 study of 5,376 ML portfolios also found large sensitivity to research-design choices.

## Test
1. Freeze a transparent baseline before candidate scoring.
2. Run candidate and baseline through exactly the same portfolio construction and execution layer.
3. Use point-in-time features and corrected forward-label overlap handling.
4. Use purged/embargoed OOS evaluation and a quarantined confirmation period.
5. Apply the same commissions, spread, slippage, market-impact and capacity assumptions.
6. Report gross and net returns, Sharpe/Sortino, drawdown, turnover, break-even cost, and benchmark-relative net value.
7. Estimate the incremental return and incremental utility attributable to the candidate signal.
8. Repeat across pre-specified subperiods/regimes without selecting favorable periods after inspection.
9. Apply selection-aware inference using the committed trial ledger, DSR/PBO and null-calibrated selection controls.

## Falsification
Reject H95 if the candidate's apparent advantage disappears after identical execution costs, is concentrated in one pre-specified subperiod, or cannot separate from matched null-search winners after multiplicity adjustment.

## Promotion criterion
No model promotion from absolute Sharpe alone. A candidate must demonstrate economically meaningful incremental net value versus the frozen baseline with statistical and robustness evidence.

## Status
Protocol only. No empirical result is claimed until the immutable candidate-level OOS prediction/return matrix and corrected forward-label-overlap validation are available.
