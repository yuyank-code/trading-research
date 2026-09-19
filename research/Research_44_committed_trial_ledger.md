# Research 44 — Committed Trial Ledgers for Multiplicity Control

## Question
Can the trading research process make its multiple-testing correction auditable by freezing the complete candidate-generation history before confirmation evaluation?

## Literature update
A July/August 2026 SSRN paper, *Who Counts the Trials? A Committed Trial Ledger for Enforcing the Deflated Sharpe Ratio in Zero-Knowledge*, identifies a structural weakness of DSR: the number of trials is normally supplied by the same researcher whose result is being corrected. The paper argues for a committed trial ledger and demonstrates a strategy whose DSR falls below its stated significance threshold after selection correction.

A 2026 study, *Unstable Gains: Multiplicity-Aware Evaluation of Financial Deep Reinforcement Learning*, extends the same logic to stochastic training: multiple random seeds generate multiple learned policies, and reporting the best seed creates a selection problem. Its recommendation is multi-run evaluation with uncertainty quantification and explicit multiplicity control.

A 2026 large-scale financial time-series benchmark also evaluates robustness to random seed, transaction-cost break-even, tail risk, and computational efficiency rather than reporting a single training run.

## Research implication
The existing project already treats seeds, execution choices, null searches, leakage fixtures, and selection-aware inference as separate controls. Research 44 combines them into one auditable **trial ledger**. The ledger is itself a versioned research artifact and must be frozen before confirmation.

## Proposed schema
Each trial receives a monotonically assigned ID and records:

- timestamp and parent experiment ID
- data/universe version
- feature and label version
- model family and hyperparameters
- training window and validation protocol
- seed
- portfolio/position rule
- execution and cost model
- benchmark
- status: attempted / failed / invalid / retained
- reason for invalidation, if applicable
- OOS artifact hash

Invalid technical trials remain in the ledger. They are not silently deleted from the multiplicity count; however, trials that never generated a candidate performance statistic can be separately classified so the statistical definition remains explicit.

## Test protocol
Run matched searches under IID and block-dependent null environments. For each search:

1. generate candidates using the same search budget as the real workflow;
2. record every attempted candidate and seed;
3. select the apparent winner using the pre-registered selection rule;
4. calculate DSR from the committed trial count;
5. compare against a null distribution generated under the same search process;
6. repeat with a deliberately incomplete ledger to quantify the optimism introduced by under-counting trials.

## Expected result
The incomplete-ledger version should produce more optimistic significance and more apparent discoveries than the committed-ledger version. If this is not observed, the ledger may add little incremental value for the project's current search design.

## Falsification / promotion rule
Research 44 is a pipeline finding only. It cannot promote a trading model. A candidate still requires clean point-in-time data, corrected forward-label-overlap validation, purged/embargoed OOS evaluation, realistic spread/slippage/impact/borrow costs where relevant, benchmark incrementality, leakage fixtures, null-search separation, DSR/PBO/SPA/Reality Check/MCS controls, and untouched confirmation.

## Current status
Protocol committed. Numerical experiment pending the validated candidate-level OOS prediction/return matrix and corrected validation implementation.
