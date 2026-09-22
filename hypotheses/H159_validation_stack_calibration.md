# H159 — Validation-Stack Calibration on Nulls and Injected Signals

## Hypothesis
A validation stack that explicitly counts research trials and applies PIT controls, purged/embargoed OOS evaluation, realistic costs, and multiple-testing corrections will materially reduce false strategy promotions while retaining a known injected signal at a pre-specified effect size.

## Primary test
Run the complete research workflow on three controlled datasets:

A. **Null:** returns/features generated so that no predictable trading edge exists.

B. **Injected signal:** same null process plus a pre-specified, time-causal signal with known effect size and persistence.

C. **Historical data:** the real project dataset, evaluated only after the PIT/label-overlap audit passes.

For A and B, repeat the identical candidate-search budget and record every trial. No selection rule may inspect the final OOS segment.

## Required gates
- Point-in-time information lineage.
- Label-horizon purge and embargo.
- Frozen final OOS.
- Realistic commission, spread, slippage and impact assumptions.
- Cost stress at 1x, 1.5x and 2x baseline.
- Trial-count/effective-trial accounting.
- PBO/DSR or equivalent multiple-testing control.
- Economic comparison against strong simple baselines.
- Turnover-matched placebo where deployment rules change activity.

## Success criterion
The stack should show a substantially lower false-promotion rate on A than an uncorrected best-backtest workflow, while retaining a materially higher promotion rate on B than the null. Thresholds must be fixed before inspecting final OOS results.

## Failure interpretation
- If A produces frequent promotions, the validation stack remains unsafe.
- If B is routinely rejected despite adequate sample size and known effect, the stack is over-conservative or incorrectly implemented.
- If only the historical dataset fails, do not tune the gates to rescue it; record the failure and investigate data lineage/model specification separately.

## Literature motivation
The experiment is motivated by Bailey & Lopez de Prado's multiple-testing correction, the 2026 MinervaScore study's finding that a composite robustness score did not predict unseen real-market outcomes, and evidence that research-design choices materially alter ML asset-pricing results.

## Status
Registered hypothesis. Results pending controlled execution.
