# Research 71 — Single-Use Final Holdouts and Multi-Gate Promotion

Date: 2026-09-21

## Executive finding

The literature continues to support a stricter distinction between model development and final evaluation. The practical implication for this project is to make the final out-of-sample period a **single-use measurement instrument**, not another tuning surface.

## High-quality evidence reviewed

### Mroziewicz & Ślepaczuk (2026)

A 2026 arXiv study evaluates walk-forward parameter-window choices on intraday Bitcoin data. It tests 81 combinations of training/testing window lengths, then applies the two best parameter sets to a separate 21-month out-of-sample period that is used once. The study includes a 0.1% per-transaction cost assumption and reports a break-even sensitivity analysis. This is directly relevant to our separation of development-window design from final evaluation.

Source: https://arxiv.org/abs/2602.10785

### Santoni, Jouanne & Scullin (2026)

A recent arXiv paper proposes MinervaScore as a post-selection robustness/reporting layer combining Deflated Sharpe Ratio, Probability of Backtest Overfitting, Superior Predictive Ability, minimum track-record length, and regime stability. Importantly, the authors report that their pre-registered test on unseen real-market data did not show a significant forward relationship in a population with limited surviving edge. That negative result is valuable: a robustness score should be treated as an audit layer, not as evidence of future profitability.

Source: https://arxiv.org/abs/2608.23808

### Kim (2026)

Kim's VALID framework reports that AUC-only validation can have substantial false-positive rates and that candidates passing a permutation test can still fail combinatorial purged cross-validation and economic validation. Multiple-testing corrections and Deflated Sharpe Ratio further reduce apparently successful variants. This supports requiring multiple independent promotion gates.

Source: https://doi.org/10.2139/ssrn.6508779

### Bysik & Ślepaczuk (2026)

A 27-fold hourly BTC walk-forward study finds that naive sign-based ML strategies fail after 10-bps transaction costs in tested configurations, while cost-aware execution filtering can improve selected configurations. XGBoost was descriptively stronger in their study, but bootstrap evidence did not establish formal statistical dominance. The relevant lesson for our project is that the execution transformation must remain inside the locked evaluation protocol.

Source: https://arxiv.org/abs/2606.00060

## Project implication

H122 therefore adds a **single-use final holdout + multi-gate promotion protocol**. The final holdout cannot be used to choose a model, threshold, feature set, execution rule, cost assumption, or portfolio construction. All such decisions must be frozen before final evaluation.

## Required immutable artifact

For every final-holdout candidate, preserve:

`timestamp, candidate_id, model_version, prediction, target, position, turnover, gross_return, commission, spread, slippage, impact, borrow_cost, net_return`

plus the exact data snapshot, feature-generation version, training cutoff, label horizon, and random seed/configuration.

## Status

This is a protocol improvement, not an alpha result. The repository still lacks a trustworthy immutable candidate-level OOS performance artifact and corrected forward-label-overlap validation, so no new Sharpe, CAGR, alpha, or promotion claim is made.
