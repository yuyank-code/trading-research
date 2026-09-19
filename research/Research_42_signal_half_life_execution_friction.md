# Research 42 — Signal Half-Life, Execution Latency, and Economic Decay

## Research question
Does the persistence of a model forecast determine whether its predictive information remains economically tradable after execution friction?

## Literature synthesis
Recent evidence points to a recurring distinction between predictive information and executable alpha. A 2026 walk-forward study of hourly BTC forecasting reports that naive sign-based ML strategies collapse under 10 bps costs, while cost-aware forecast thresholds can restore profitability in selected configurations. A 2026 microstructure study across crypto assets finds stable short-horizon feature selection but severe model overfitting under leakage controls and no strategy surviving realistic exchange fees. Recent FX ML research also reports that market efficiency has increased and that model complexity does not automatically translate into better practical trading performance. Classical FX microstructure work documents that transaction costs vary with liquidity, volatility, trading frequency and information conditions, making a constant-cost assumption inadequate.

These results motivate a causal execution hypothesis rather than another architecture search: if the signal decays before it can be executed, higher raw predictive accuracy may have little or no economic value.

## Testable hypothesis
H91: For a fixed causal predictor, horizons with slower forecast decay relative to execution friction should have more stable positive net utility than horizons where predictive information decays rapidly.

## Experimental design
- Freeze predictor, feature set, training protocol and candidate budget.
- Produce chronological purged/embargoed OOS forecasts.
- Estimate persistence only from training/validation windows.
- Evaluate pre-registered execution/holding horizons.
- Include spread, commission, slippage and nonlinear impact.
- Stress costs upward and preserve exact fill assumptions.
- Compare gross predictive decay with net PnL decay.
- Include simple benchmarks and matched null forecasts.
- Apply DSR/PBO, SPA/Reality Check, MCS, subperiod/regime tests, capacity stress and the synthetic-null workflow.
- Keep confirmation untouched until the specification is frozen.

## Decision rule
Support H91 only if persistence predicts net economic utility across confirmation subperiods and cost scenarios, remains significant after search-aware controls, and is not reproduced by null forecasts. Otherwise retain the simpler execution rule and record the hypothesis as failed.

## Current status
Pre-registered. No numerical pass claimed. The immutable candidate-level OOS prediction/return matrix and corrected forward-label-overlap validation remain prerequisites for model promotion.
