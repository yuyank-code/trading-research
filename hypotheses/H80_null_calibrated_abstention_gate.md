# H80 — Null-Calibrated Abstention Gate

## Status
Pre-registered research hypothesis. No promotion claim.

## Motivation
A model does not have to trade on every forecast. Recent selective-trading research proposes a leakage-aware rule that compares the candidate signal with a transparent fallback and abstains when validation evidence is insufficient. This is especially relevant when transaction costs make weak forecasts uneconomic. The key risk is that an abstention threshold becomes another tuning parameter and creates a hidden selection channel.

## Hypothesis
A pre-specified, validation-only abstention rule can improve net risk-adjusted performance by suppressing low-conviction trades, but only if the improvement survives null-calibrated threshold selection, untouched confirmation data, and the existing multiple-testing controls.

## Falsification
Reject H80 if:
- the gate improves only before realistic costs;
- the selected threshold changes materially across validation folds without stable economic rationale;
- a matched-count random gate performs similarly;
- the advantage disappears on the locked confirmation block;
- performance requires repeated threshold tuning after observing confirmation results;
- abstention merely concentrates returns into a small number of periods/trades.

## Pre-registered experiment
Keep the underlying candidate model, features, labels, model family, hyperparameters, holding period, universe, validation scheme, embargo and confirmation set frozen.

Within each training/validation origin, compare:
1. always-trade baseline;
2. fixed no-trade threshold derived only from the pre-specified cost model;
3. validation-calibrated abstention threshold selected from a small pre-registered grid.

The grid size must be recorded before evaluation. Threshold selection is performed independently inside each training/validation origin and never on confirmation observations.

Report:
- net annualized return;
- net Sharpe and Sortino;
- maximum drawdown and tail losses;
- turnover and trade count;
- fraction of periods abstaining;
- gross-to-net performance degradation;
- break-even transaction cost;
- fold-level stability;
- confirmation performance;
- DSR/PBO and SPA/Reality Check;
- Model Confidence Set where multiple candidates remain;
- synthetic zero-alpha and matched-count random-gate controls.

## Null calibration
The gate must be tested on placebo forecasts with identical validation windows and an identical threshold-search budget. The false-deployment rate is recorded. A gate that frequently activates on null signals is considered invalid even if the real candidate improves.

## Leakage controls
- The threshold cannot use future realized costs, returns, spreads, volumes or confirmation outcomes.
- Any cost estimate used by the gate must be point-in-time available.
- Threshold selection and fallback comparison are performed inside the causal validation loop.
- Confirmation is locked before the gate is run on it.

## Interpretation
The objective is not to maximize the number of profitable trades. A successful gate should reduce economically weak trading while preserving a statistically defensible edge. If the improvement comes entirely from threshold search, it is treated as selection bias rather than model improvement.

## Evidence standard
No candidate is promoted from H80 alone. Promotion still requires the corrected forward-label validation, frozen candidate-level OOS prediction/return matrix, realistic execution costs, leakage audit, multiple-testing controls, and independent confirmation.
