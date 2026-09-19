# Research 48 — Robustness Scores: Audit Layer, Not Alpha Evidence

## Date

2026-09-20

## Question

Can a composite robustness score safely replace the project's primary statistical and structural validation gates?

## Literature synthesis

A recent 2026 paper, *Equity Strategy Backtesting: Luck or Edge? The MinervaScore as a Statistical Robustness Grade*, combines Deflated Sharpe Ratio, Probability of Backtest Overfitting, Superior Predictive Ability, Minimum Track Record Length, and regime stability. Its synthetic calibration reports strong separation between planted signal and lucky backtests, but its pre-registered unseen real-market test found no significant forward relationship between the score and subsequent outcomes (reported Spearman rho = 0.013, one-sided permutation p = 0.40). The authors therefore frame the score as an auditable validation/reporting layer rather than evidence of demonstrated real-market predictability.

A separate 2026 study on leakage-safe, search-aware strategy discovery reaches an even more important methodological conclusion: structural leakage controls are not redundant with statistical corrections. In that work, a deliberately leaky oracle could produce an extreme Sharpe while still passing DSR and PBO, demonstrating that multiple-testing correction cannot repair an invalid information set.

A 2026 large-scale deep-learning benchmark also evaluates financial models using OOS risk, statistical significance, breakeven transaction costs, random-seed robustness, and computational efficiency rather than a single predictive metric. This supports keeping the project's gates modular and auditable.

## Implication for this project

Do not introduce a new composite score as a promotion shortcut. A score may summarize evidence after the fact, but every candidate must independently satisfy the structural gates:

1. point-in-time information availability;
2. corrected forward-label-overlap validation;
3. immutable candidate-level OOS predictions and realized returns;
4. realistic commissions, spread, slippage, impact and capacity assumptions;
5. selection-aware trial accounting and multiplicity correction;
6. stability across seeds, subperiods and regimes;
7. comparison against a transparent baseline under the identical execution layer.

## Proposed experiment

H98 freezes a candidate composite score and evaluates it on three datasets: a synthetic null, a synthetic planted-signal environment, and an untouched real-market confirmation set. The score's calibration performance is reported separately from future trading performance. No confirmation data are used to tune the score.

The decisive comparison is incremental predictive value: does the composite score explain future net OOS performance beyond the primary gates themselves? If not, it remains a reporting convenience rather than a source of evidence.

## Current result

No new numerical alpha result was generated in this run. The repository's corrected label-overlap validation and immutable candidate-level OOS prediction/return matrix remain prerequisites for trusting numerical model comparisons.

## Verdict

Meaningful methodological progress: **yes**.

New testable hypothesis: **H98**.

Robust trading alpha established: **no**.

Model promotion: **no**.

## Sources

- Santoni, Jouanne & Scullin (2026), *Equity Strategy Backtesting: Luck or Edge? The MinervaScore as a Statistical Robustness Grade*, arXiv:2608.23808.
- Gençay (2026), *What survives honest evaluation? Leakage-safe, search-aware assessment of LLM-driven trading strategy discovery*, arXiv:2608.27734.
- Saly-Kaufmann, Wood, Calliess & Zohren (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*, arXiv:2603.01820.
