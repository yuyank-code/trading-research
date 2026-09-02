# Run 30 — Validation priority: freeze the research surface

Date: 2026-09-03

## Meaningful findings

1. The linked trading engine (`bitcoin-ml-trading`) has not advanced past commit `7345a3f` since the last recorded validation work. The main scientific blockers therefore remain executable-event alignment, point-in-time external data, event-interval purging/embargo, and intrabar execution ambiguity.
2. The strongest methodological literature continues to support treating the selected backtest as a post-selection object rather than a simple forecast test. Bailey et al.'s PBO/CSCV framework was designed because ordinary holdouts can be unreliable for investment backtests; Bailey & López de Prado's DSR corrects selected Sharpe for multiple testing and non-normality.
3. A 2024 controlled comparison reports CPCV outperforming conventional OOS methods on overfitting controls (lower PBO / stronger DSR). This supports using CPCV after the executable event definition is frozen, not before.
4. A 2026 paper proposing a composite robustness score is useful as a reporting layer but explicitly reports no significant forward relationship on its preregistered unseen real-market test. We therefore should not replace the individual statistical/economic gates with a single score.

## New testable hypothesis

**H14 — Research-surface freeze:** once executable labels, point-in-time joins, and execution ambiguity handling are implemented, further feature/model/threshold changes should be evaluated only on frozen OOS predictions and counted as trials. If the apparent winner changes materially under the frozen evaluation protocol, prior rankings are classified as selection-sensitive rather than robust.

## Required next experiment

- Freeze an explicit event schema: signal_time, entry_time, event_end_time, available_at for external features.
- Generate immutable OOS predictions for the candidate baseline ensemble and simple baselines.
- Apply predeclared cost/slippage grid.
- Resolve or bound intrabar stop/target ambiguity.
- Run CPCV/PBO and DSR with the complete trial ledger.
- Reserve one untouched final holdout for a single confirmatory evaluation.

## Decision

Do not add complex architectures until the existing baseline survives the above gates. No profitability claim is made in this run.
