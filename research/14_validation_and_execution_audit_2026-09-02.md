# Run 14 — Validation and execution audit (2026-09-02)

## Scope
Fresh audit of the current Bitcoin ML trading reference engine plus additional literature on backtest overfitting, search-adjusted inference, and execution costs.

## Verified implementation status

`bitcoin-ml-trading/production_research.py` currently sets `HORIZON_BARS=6` and, for each walk-forward fold, trains through `start-horizon_bars`. This removes the direct six-bar forward-label overlap at the train/test boundary. The prior label-overlap defect should therefore no longer be treated as active in the current reference file, subject to regression testing.

The current `validation.py` still has two concrete defects:

1. `validate_predictions()` drops duplicate `Date` rows before measuring duplicates, so `duplicate_dates` is always zero. The validator must count duplicates before mutation and should fail rather than silently deduplicate research artifacts.
2. `stress_costs()` constructs a dynamic `StressConfig`, but the current `production_research.signal_backtest()` accepts scalar fee/slippage arguments. The advertised stress wrapper therefore does not actually exercise the authoritative execution function.

These are validation-infrastructure failures, not trading-edge evidence.

## Execution-model limitations found

The current signal backtest includes explicit fees and symmetric slippage, but it does not yet model spread or market-impact as independent components. The expected-gross trade filter also assumes the same stop/target path used by the execution simulator. This is acceptable for a controlled prototype, but not sufficient for a capacity claim.

The simulator should next expose a single explicit cost model:

`total_cost = commission + half-spread + adverse_slippage + market_impact`

with all components recorded per trade. Stress testing should vary each component independently and jointly.

## Literature update

Recent directly relevant evidence remains consistent with a cost-aware execution hypothesis. Bysik & Ślepaczuk (2026), using about 70,000 hourly BTC-USDT observations and 27 walk-forward folds, report that naive sign-based ML strategies can lose their apparent profitability under 10-bps transaction costs, while a forecast-magnitude cost filter can reduce turnover and recover profitability in selected configurations. They do not establish statistically significant dominance of XGBoost over neural alternatives.

The broader overfitting literature remains a hard constraint: Bailey et al. show that trying more configurations increases the probability of backtest overfitting; Bailey & López de Prado's DSR corrects performance inference for multiple testing and non-normality; CSCV/PBO provides a framework for estimating the probability that a selected backtest is overfit.

## New hypotheses

- H35: validation artifacts must fail closed on duplicate timestamps rather than silently deduplicating them.
- H36: cost stress results are invariant to the choice of execution-wrapper API once wired to the authoritative simulator.
- H37: an execution policy that survives fee + spread + slippage stress is more robust than one that survives fee-only stress.
- H38: adding market-impact assumptions should reduce high-turnover strategies disproportionately; a purported edge that survives only zero/low-impact assumptions is not production evidence.
- H39: final model selection must use a frozen configuration on an untouched holdout and report the full trial count for search-adjusted inference.

## Evidence status

No new profitability number is promoted. The repository currently does not contain the generated OOS prediction/equity artifacts required for an independently reproducible numerical claim. The correct next milestone is to repair the validator/stress API, generate immutable artifacts, then run the predeclared cost grid and final holdout once.
