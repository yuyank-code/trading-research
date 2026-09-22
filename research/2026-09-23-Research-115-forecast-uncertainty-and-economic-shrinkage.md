# Research 115 — Forecast Uncertainty and Economic Shrinkage

**Date:** 2026-09-23

## Question

Can explicit uncertainty estimates improve trading decisions more reliably than increasing model capacity, by shrinking or abstaining on forecasts whose expected economic value is not large relative to forecast uncertainty and trading costs?

## Literature

Liao, Ma, Neuhierl & Schilling (CEPR DP20080, 2025) develop confidence intervals for neural-network expected-return forecasts and show that incorporating forecast uncertainty into investment decisions can improve out-of-sample performance through uncertainty-averse/shrinkage portfolio construction.

Recent transaction-cost-aware Bitcoin work (Bysik & Slepaczuk, 2026) finds a strong disconnect between forecasting metrics and net trading returns: naive sign trading can fail after costs while forecast-magnitude filtering can materially reduce turnover and restore economics in selected configurations.

A 2026 validation study also reports that transaction costs can consume most apparent gross alpha in crypto ML strategies, reinforcing that signal selection should be evaluated at the decision layer rather than with prediction metrics alone.

## Synthesis

The useful combination is not simply "better uncertainty estimation." The testable economic claim is narrower:

> Given the same frozen PIT-safe forecasts, uncertainty-aware shrinkage/abstention should improve net decision utility by suppressing low-confidence trades, without requiring additional model complexity.

This is distinct from optimizing a validation score. The uncertainty rule must be frozen before the final holdout and must not be tuned on that holdout.

## Experimental implications

Compare a frozen model's raw position rule against:

1. raw forecast-to-position mapping;
2. cost-only threshold;
3. uncertainty-only shrinkage;
4. joint uncertainty + cost gate;
5. matched-capacity placebo gate.

All variants must use identical observations, execution timing, PIT constraints, purge/embargo, costs, slippage, impact and research-trial accounting.

The primary endpoint is paired net OOS decision utility versus the frozen baseline, not MSE/AUC.

## Failure criteria

Reject the hypothesis if the uncertainty-aware rule only wins on one cost assumption, depends on holdout tuning, increases turnover, loses its advantage under seed aggregation, or cannot outperform a simple cost threshold after search adjustment.

## Status

Literature-supported hypothesis; executable candidate-level evidence is still pending the project's PIT-clean artifact and corrected label-overlap validation.
