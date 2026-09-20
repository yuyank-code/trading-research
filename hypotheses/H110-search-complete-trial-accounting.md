# H110 — Search-Complete Trial Accounting

## Hypothesis

If every candidate evaluation, including failed, discarded, aborted, and intermediate configurations, is immutably recorded and included in the multiple-testing/search budget, then apparent strategy significance will be materially reduced relative to naive reporting that counts only promoted candidates.

## Motivation

Recent 2026 work on leakage-safe, search-aware strategy discovery shows that structural leakage prevention and search accounting are complementary: a deliberately leaky oracle can evade statistical correction, while honest evaluation requires recording the full search history. A separate 2026 robustness framework combines Deflated Sharpe Ratio, Probability of Backtest Overfitting, Superior Predictive Ability, minimum track-record length, and regime stability as an auditable validation layer.

## Test design

Compare two reporting paths on the same frozen candidate universe:

1. **Incomplete accounting:** count only candidates that reach the final scoring/promotion stage.
2. **Complete accounting:** count every model, feature set, threshold, execution rule, benchmark, seed, and discarded candidate evaluated before the final choice.

For both paths preserve identical OOS returns and apply the same DSR/PBO/SPA procedures.

## Required controls

- Immutable candidate ID and parent experiment ID.
- Timestamp and code/data version for every evaluation.
- Explicit status: completed, failed, aborted, rejected, or promoted.
- No deletion or rewriting of prior trial records.
- Separate exploratory and locked confirmation datasets.
- Search budget declared before confirmation.
- Effective-trial estimate in addition to nominal trial count where candidate returns are correlated.

## Primary outcomes

- Difference between naive and search-complete DSR.
- Difference between naive and search-complete PBO/SPA conclusions.
- Number of previously 'significant' candidates rejected after complete accounting.
- Whether conclusions remain unchanged on a final untouched confirmation period.

## Falsification

H110 is supported only if complete accounting materially changes inferential calibration without introducing a corresponding degradation in genuine-signal detection on synthetic data with known non-zero edge.

If complete accounting does not reduce false promotions on null/placebo data, the audit is inadequate.

## Promotion gate

No candidate may be promoted if its search history cannot be reconstructed from immutable trial records.
