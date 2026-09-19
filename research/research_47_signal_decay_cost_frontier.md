# Research 47 — Signal Decay / Cost Frontier

Date: 2026-09-20

## Motivation

Recent financial ML evidence reinforces that gross predictive performance is not enough: transaction costs can erase naive trading rules, while cost-aware execution thresholds can materially reduce turnover. Large-scale benchmarks increasingly report break-even transaction costs and seed robustness alongside OOS risk metrics.

## New hypothesis H97

**H97 — Net-alpha survives a cost frontier and execution-latency perturbation.**

A candidate signal should retain economically meaningful incremental value versus a frozen baseline across a pre-registered grid of execution frictions. The signal should also decay monotonically or plausibly as execution is delayed; a discontinuous or unusually favorable response is a diagnostic for timing leakage or fragile microstructure dependence.

## Test protocol

1. Freeze candidate, features, labels, universe, and portfolio construction before the test.
2. Generate immutable OOS predictions first; never tune on the confirmation period.
3. Evaluate identical candidate and baseline portfolios at cost levels spanning zero-cost through conservative stressed assumptions.
4. Add execution-latency perturbations (same-bar, next-bar, and delayed execution where economically applicable) without changing the model.
5. Report net Sharpe, CAGR, turnover, max drawdown, break-even cost, and incremental alpha versus the frozen baseline.
6. Require the candidate to beat the baseline under the pre-registered cost/latency frontier rather than only at a single chosen cost.
7. Run the same frontier on matched null-search winners to detect selection-induced apparent robustness.
8. Apply leakage, label-overlap, purged/embargoed OOS, DSR/PBO, SPA/Reality Check, and MCS gates before promotion.

## Literature anchor

Bysik & Ślepaczuk (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs*, reports that naive sign-based BTC ML strategies fail at 10 bps while cost-aware forecast thresholds restore profitability in selected configurations; formal statistical dominance is not established. arXiv:2606.00060.

Saly-Kaufmann et al. (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*, evaluates OOS Sharpe, downside/tail risk, break-even transaction costs, random-seed robustness, and computational efficiency on 2010–2025 daily futures data.

Arian, Norouzi Mobarekeh & Seco (2024), *Backtest overfitting in the machine learning era*, finds CPCV superior to traditional OOS methods in a controlled synthetic setting for mitigating backtest overfitting.

Nikolopoulos (2026), *Spurious Predictability in Financial Machine Learning*, proposes falsification of complete adaptive workflows against zero-predictability and microstructure placebo reference classes.

## Promotion criterion

H97 is a robustness gate, not an alpha claim. Failure at realistic costs or under small latency perturbations blocks promotion even if gross OOS Sharpe is positive.
