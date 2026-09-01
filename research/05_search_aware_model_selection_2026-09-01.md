# Research Update 05 — Search-Aware Model Selection

Date: 2026-09-01

## Purpose

This update tightens the model-selection protocol before expanding the BTCUSDT candidate-model search.

## Literature findings

### Gu, Kelly & Xiu (2020)

Their comparative asset-pricing study finds that trees and neural networks can improve return prediction primarily through nonlinear predictor interactions, while deeper networks do not automatically improve performance. Their experimental design uses chronological training/validation/test periods. This supports testing nonlinear interactions, but does not justify assuming a complex model will work for BTCUSDT.

Source: https://academic.oup.com/rfs/article/33/5/2223/5758276

### Bailey et al. — Probability of Backtest Overfitting

Combinatorially symmetric cross-validation (CSCV) is proposed to estimate the probability that a selected backtest is overfit. This is directly relevant once our experiment registry contains enough alternative model/configuration trials.

Source: https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2326253

### Bailey & López de Prado — Deflated Sharpe Ratio

DSR adjusts the apparent Sharpe ratio for multiple testing and non-normal returns. A high raw Sharpe is therefore insufficient when many configurations have been searched.

Source: https://papers.ssrn.com/sol3/Delivery.cfm/SSRN_ID2460551_code87814.pdf?abstractid=2460551

### Bailey et al. — Backtest overfitting

The literature demonstrates that high simulated performance can arise surprisingly easily after testing multiple configurations. This makes the research-search count an input to evidence evaluation rather than an implementation detail.

Source: https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2308659

### Harvey & Liu — Evaluating Trading Strategies

The evaluation problem should account for the number of discoveries attempted and should demand stronger evidence for strategies found after broad searches.

Source: https://papers.ssrn.com/sol3/Delivery.cfm/SSRN_ID2474755_code87814.pdf?abstractid=2474755

### López de Prado — Optimal Trading Rules Without Backtesting

This provides a useful conceptual warning: repeatedly calibrating stop/target rules through historical simulation can itself become a source of overfitting. Where feasible, economically motivated rule ranges should be specified before evaluation rather than selected from the final OOS period.

Source: https://papers.ssrn.com/sol3/Delivery.cfm/SSRN_ID2504302_code434076.pdf?abstractid=2502613

## Testable hypotheses

### H13 — Nonlinear incremental value

A tree/boosting model must improve the untouched OOS economic objective relative to a frozen regularized-linear benchmark after the same cost assumptions. Predictive metrics alone are insufficient.

### H14 — Interaction stability

If nonlinear interactions are real, their contribution should remain directionally useful across multiple chronological OOS windows rather than being concentrated in one regime.

### H15 — Cost-aware model ranking

The model with the highest predictive score need not be the model with the highest net trading value. Candidate ranking should therefore be performed on net, risk-adjusted economic metrics after costs.

### H16 — Threshold neighborhood robustness

A viable signal should not require a single finely tuned probability threshold. Performance should remain acceptable across a pre-declared neighborhood around the selected threshold.

### H17 — Search-adjusted significance

A candidate that looks strong before accounting for the number of trials may fail after DSR/PBO-style correction. The model-selection record must therefore preserve every meaningful candidate and configuration tested.

## Required experimental protocol

1. Freeze the feature definition before final OOS evaluation.
2. Split chronology into training, validation, and untouched OOS periods.
3. Purge observations whose label/event intervals overlap the test interval.
4. Apply an embargo after the test boundary when dependence/overlap requires it.
5. Tune hyperparameters only inside training/validation data.
6. Freeze model and decision threshold before untouched OOS.
7. Evaluate with fees, spread/slippage assumptions, turnover and capacity constraints.
8. Repeat under a pre-declared cost sensitivity grid.
9. Record every meaningful trial, including failures.
10. Apply search-aware diagnostics such as DSR/PBO/SPA where the trial set permits.

## Important implementation correction

The existing research code contains a leak-free robustness path, but the research record must distinguish between two different concepts:

- **signal-label leakage:** future-return information influencing entry decisions;
- **selection leakage:** repeatedly changing the model/rules after observing historical test-like performance.

Eliminating the first does not eliminate the second. The new trial registry is therefore a research-control requirement, not merely bookkeeping.

## Current result

No new trading edge is claimed in this update. The meaningful result is methodological: the next candidate-model comparison must be conducted only after the search-aware experiment ledger and frozen OOS protocol are in place. Adding more models before this point would increase the probability of selecting a spurious winner.

## Next experiment

Compare a frozen regularized-linear baseline against one shallow tree/boosting candidate and one shallow neural-network candidate, using identical information sets and identical chronological splits. Evaluate both prediction quality and net trading performance under multiple pre-declared transaction-cost assumptions. Do not select the final model from the untouched OOS period.
