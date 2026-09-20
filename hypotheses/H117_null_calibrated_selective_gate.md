# H117 — Null-Calibrated Selective Trading Gate

## Status
Proposed / preregistered for the next executable candidate evaluation.

## Hypothesis
A deployment gate calibrated only on past information and validated against placebo/null signals can improve net out-of-sample utility by avoiding low-edge trades, without merely selecting lucky periods.

## Primary comparison
1. Candidate model, always trade.
2. Same candidate + frozen selective gate + fallback.
3. Fallback alone.
4. Placebo signal + identical gate.

## Required controls
- Point-in-time features and labels.
- Correct forward-label-overlap purge and embargo.
- Fold-isolated preprocessing/calibration.
- No threshold selection on final OOS observations.
- Complete trial accounting, including rejected gates and failed runs.
- Explicit commissions, spread, slippage and impact.
- Cost stress at 1.5x and 2x reference costs.
- Execution-lag perturbation.
- Predefined subperiod/regime evaluation.
- Multiple-testing adjustment / DSR-PBO reporting where applicable.

## Primary endpoint
Incremental net OOS utility versus the fallback, with turnover and break-even cost reported alongside it.

## Failure criteria
Reject the gate if it only improves gross or in-sample metrics, if placebo gates pass at a material rate, if gains disappear under modest cost stress, or if the effect is concentrated in a single preselected period/path.

## Literature context
Bysik & Ślepaczuk (2026), "Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting" reports that naive sign-based strategies fail under 10 bps in selected BTC experiments and that cost-aware forecast filtering can restore profitability in some configurations; it does not establish formal model dominance. A 2026 selective-ML preprint proposes leakage-aware abstention against a transparent fallback. Both are treated as hypothesis-generating evidence, not confirmation.
