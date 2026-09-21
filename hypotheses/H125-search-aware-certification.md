# H125 — Search-Aware Certification of the Final Candidate

## Hypothesis

A candidate that survives a realistic, search-aware evaluation with explicit accounting for the number and adaptiveness of research trials will retain positive incremental net OOS utility against strong frozen baselines. If apparent performance is primarily selection luck, it will collapse under search-aware inference or fail to beat the baseline on untouched data.

## Motivation

Recent 2026 research on leakage-safe, search-aware strategy discovery reports that realistic-cost evaluation can reject apparently promising strategies after accounting for selection luck, rank degradation, and OOS collapse. This is directly relevant to a research program that has accumulated many candidate hypotheses and design choices.

## Test design

1. Freeze the final candidate universe and all baseline definitions before opening the final holdout.
2. Record the complete research-trial count, including model variants, feature sets, windows, gates, cost assumptions, and design perturbations that informed selection.
3. Evaluate every candidate on identical timestamps and the same execution/cost engine.
4. Preserve row-level immutable records: information cutoff, prediction, position, execution, turnover, gross return, commissions, spread, slippage, impact, borrow/funding, and net return.
5. Apply search-aware inference (DSR/PBO or an equivalent predeclared correction) and paired candidate-vs-baseline tests.
6. Stress transaction costs at 1x, 1.5x, and 2x and perturb execution timing.
7. Keep the final holdout single-use; no candidate, threshold, or cost model may be changed after seeing it.
8. Run a null/placebo workflow with the same research-selection machinery to estimate how often the process manufactures winners.

## Promotion criterion

Promotion requires all of: leakage/overlap pass; positive incremental net OOS utility; survival under cost stress; no material collapse under execution-lag perturbation; search-aware significance; and evidence that the result is not explained by a strong non-ML baseline.

## Failure criteria

Reject if the candidate loses its advantage after selection correction, realistic costs, baseline comparison, or null calibration, even if raw OOS Sharpe remains positive.

## Status

Protocol committed. Numerical evaluation is pending the immutable candidate-level OOS artifact and corrected forward-label-overlap validation.
