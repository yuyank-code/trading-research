# H77 — Nested Selection and Final-Test Quarantine

## Hypothesis
A model selected after repeated walk-forward/model/feature/cost experiments will show materially weaker performance on a genuinely untouched final confirmation block than on the last validation block. Explicitly separating selection data from a one-time confirmation set should reduce this hidden-selection bias.

## Motivation
Recent empirical work shows that look-ahead and repeated specification search can manufacture apparent alpha. The research process must therefore treat every adaptive comparison as a source of statistical exposure, not merely treat the final model as one isolated test.

## Test design
- Freeze the candidate family and all feature definitions before evaluation.
- Use chronological train/validation splits with purge and embargo determined from the maximum label horizon.
- Allow model/hyperparameter/cost-objective selection only on the development set.
- Lock the selected specification before opening the confirmation block.
- Evaluate the locked specification once on the untouched confirmation block.
- Report the full distribution of fold returns, not only the aggregate Sharpe.
- Compare development-to-confirmation degradation in Sharpe, Sortino, hit rate, turnover and drawdown.
- Apply realistic spread, commission, slippage and impact assumptions and adverse-cost stress.
- Apply DSR/PBO and SPA/Reality Check using the complete recorded search history.
- Run the H67 synthetic-null workflow through the same selection procedure.

## Falsification criteria
Fail H77 if any of the following occur:
1. the confirmation result materially reverses sign relative to development;
2. the result depends on a single validation block or parameter choice;
3. the strategy loses economic viability under plausible cost stress;
4. the null workflow produces comparable apparent winners;
5. final-test observations influence any selection decision.

## Promotion rule
No candidate is promoted merely because it wins the development set. Promotion requires a locked specification, untouched confirmation evidence, statistical correction for the recorded search, and stable net performance across plausible execution assumptions.

## Status
Pre-registered. No empirical pass claimed until the frozen candidate-level OOS return/prediction matrix and point-in-time dataset are available.
