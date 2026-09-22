# H150 — Economic promotion gate vs prediction-based selection

Date: 2026-09-22

## Question

Does selecting models by net trading utility with multiplicity-aware validation produce candidates that remain superior to models selected by prediction metrics alone?

## Arms

A. Prediction-metric selection (AUC/R2/loss)
B. Gross-return selection
C. Net-return / net-utility selection with realistic execution costs
D. Net-utility selection plus PBO/DSR-style multiplicity gate
E. Identical search workflow on shuffled/synthetic null data

## Falsification criteria

Reject the economic-selection claim if the net-utility/PBO arm does not beat the strong baseline on untouched OOS after costs, or if comparable gains appear under null data.

## Required controls

- point-in-time data
- purged/embargoed OOS
- no final-OOS tuning
- commissions, spread, slippage, impact and capacity
- 1x/1.5x/2x cost stress
- execution-lag stress
- all-seed reporting
- regime/tail analysis
- complete research-search ledger

## Status

Protocol added. Numerical result pending corrected validation; older results remain blocked by the known forward-label-overlap issue.
