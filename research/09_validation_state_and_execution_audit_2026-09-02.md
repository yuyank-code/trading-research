# Validation state and execution audit — 2026-09-02

## Status

This pass audits the current executable Bitcoin ML research path and the latest literature. No new performance claim is promoted because the repository does not currently contain a reproducible frozen OOS prediction artifact/results table that can be independently recomputed from checked-in data.

## Important correction to the previous audit

The current `bitcoin-ml-trading/production_research.py` is no longer the same implementation that was previously flagged for label overlap. The current reference path explicitly sets `train_end = start - horizon_bars` inside its walk-forward routine. For the 6-bar target, the final training label therefore ends before the first test label begins. This is a material implementation improvement and supersedes the earlier statement that the current production file was still using all rows through the test boundary.

The separate `research_v2.py` also implements the same horizon-based purge. These two implementations should now be regression-tested against each other before either becomes the sole authority.

## Remaining executable risks

1. **Backtest decision/evaluation separation:** `trading_bot.py` contains a backtest routine that checks `row.future_return` as an entry condition. That is invalid for a production-style simulation because `future_return` is only known after the signal timestamp. It must not be used for trade selection. The research runner does not need this condition because it can use model-derived expected edge instead.
2. **Event-time validation:** a fixed `horizon_bars` purge is correct for the current fixed six-bar label, but the pipeline should store `prediction_time` and `label_end_time` explicitly so that any future variable-horizon or event-based label can be purged by interval rather than by row count.
3. **Execution assumptions:** current simulations use fixed fee/slippage parameters. A promotion-grade experiment needs a predeclared cost grid and, where data permit, spread/impact sensitivity. A single favorable cost assumption is insufficient.
4. **Search accounting:** `research_v2.py` searches 3 model families × 5 feature sets × 5 thresholds = 75 configurations before any additional future experiments. The entire trial family must be recorded when applying DSR/PBO/CSCV-style selection adjustments.
5. **Fold stability:** pooled OOS metrics are insufficient. Candidate promotion should require fold-level distributions, worst-fold behavior, and concentration diagnostics.
6. **Calibration:** Brier score is already computed, but probability calibration has not yet been isolated as a frozen-prediction policy experiment. Calibration must be fit only inside training data if added.

## Literature update

### Bailey et al. — Probability of Backtest Overfitting

CSCV/PBO exists because ordinary holdouts can be unreliable for investment simulations. The framework estimates how likely the selected backtest is to be overfit. Source: SSRN 2326253.

### Bailey & López de Prado — Deflated Sharpe Ratio

The observed Sharpe should be deflated for multiple testing and non-normality. This is especially relevant after the 75-configuration search in the current research runner. Source: SSRN 2460551.

### Bysik & Ślepaczuk (2026) — ML Bitcoin trading under transaction costs

Their 2018–2026 hourly BTC-USDT study reports that naive sign-based ML strategies can fail after transaction costs, while a forecast-magnitude/cost-aware execution filter can reduce turnover and recover profitability in selected configurations. They report no formal statistical dominance of XGBoost over neural alternatives. Source: arXiv:2606.00060.

## New hypotheses

**H25 — Fixed-horizon purge equivalence:** the two current purged walk-forward implementations produce identical train/test boundary rules for the fixed six-bar target.

**H26 — No future-derived decision variables:** removing all future-return-derived entry conditions from the execution simulator does not materially change the intended model-policy evaluation because the decision should depend only on frozen OOS predictions and information available at signal time.

**H27 — Cost-grid robustness:** a candidate must remain economically meaningful across a predeclared fee/slippage grid rather than at one cost point.

**H28 — Fold robustness:** a candidate with strong pooled OOS performance but concentrated in a small number of folds is rejected or downgraded despite a high pooled Sharpe.

**H29 — Search-adjusted survival:** after accounting for the full 75-configuration research family, the selected strategy remains statistically credible under DSR/PBO-oriented diagnostics.

## Next gate

Do not expand the model family. First:

1. remove future-derived execution conditions from `trading_bot.py`;
2. add explicit `prediction_time`/`label_end_time` fields;
3. add regression tests for purging and timestamp monotonicity;
4. generate and freeze OOS predictions from one declared experiment family;
5. run the cost grid and fold diagnostics;
6. only then evaluate calibration/uncertainty policies;
7. apply search-adjusted inference to the complete experiment registry.

## Evidence status

**Robust finding:** the current research reference paths now contain horizon-based purging, correcting the previously identified label-overlap mechanism.

**Failure still open:** the general-purpose backtest code contains a future-return-based trade filter and therefore cannot be treated as a clean execution simulator.

**No new trading edge is claimed.** The repository currently lacks checked-in frozen OOS artifacts sufficient for an independent numerical performance claim in this pass.
