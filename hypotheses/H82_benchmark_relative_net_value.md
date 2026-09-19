# H82 — Benchmark-Relative Net Economic Value

## Status
Pre-registered hypothesis; not yet empirically evaluated because the repository does not yet contain the frozen candidate-level OOS prediction/return matrix required for honest confirmation.

## Motivation
A candidate can show positive OOS Sharpe while still adding no evidence beyond a transparent benchmark. Recent leakage-safe, search-aware trading research emphasizes that honest evaluation should compare discovered rules against passive/simple baselines under the same instruments, costs, and information set. Recent deep-learning financial benchmarks likewise evaluate statistical significance, downside/tail risk, break-even transaction costs, seed robustness, and computational cost rather than headline Sharpe alone.

## Hypothesis
After all selection is frozen, at least one candidate model will deliver **incremental net economic value** relative to a pre-specified transparent benchmark on untouched confirmation data, after realistic transaction costs, slippage, impact and turnover.

The null is that the candidate's apparent advantage is explained by benchmark exposure, risk scaling, trading intensity, or selection luck.

## Benchmarks
Use a fixed benchmark family selected before confirmation:

1. cash / zero-return baseline;
2. buy-and-hold or passive benchmark appropriate to the traded instrument;
3. simple lagged-return or moving-average rule where economically appropriate;
4. cost-aware sign/magnitude rule using only information available at decision time.

The benchmark specification and parameter budget are frozen before confirmation.

## Test design
- Train/calibrate only on development data.
- Use purged/embargoed chronological validation with embargo at least as large as the maximum forward-label horizon.
- Lock the model, feature set, benchmark definitions, execution assumptions and search budget before confirmation.
- Evaluate candidate and benchmarks on exactly the same dates and tradable observations.
- Apply identical spread, commission, slippage, impact and capacity assumptions.
- Report both absolute and benchmark-relative returns.

## Primary metrics
- mean net excess return over benchmark;
- paired difference in period returns;
- annualized net Sharpe and Sortino;
- maximum drawdown and tail loss;
- turnover and implementation shortfall;
- break-even transaction cost;
- confidence interval for incremental return/utility.

## Statistical safeguards
- Deflated Sharpe Ratio / multiple-testing adjustment;
- Probability of Backtest Overfitting / combinatorial purged validation where feasible;
- SPA / Reality Check for data-snooping across candidates;
- Model Confidence Set for surviving candidate families;
- matched-count placebo strategies;
- synthetic zero-alpha controls;
- subperiod and regime stability.

## Falsification rules
Reject the hypothesis if:
- the candidate does not beat the frozen benchmark on confirmation after costs;
- the advantage disappears under modest adverse-cost stress;
- benchmark-relative gains are concentrated in one short subperiod;
- the result requires a post-hoc benchmark or risk adjustment;
- placebo candidates achieve comparable benchmark-relative performance;
- the advantage disappears after multiple-testing correction.

## Interpretation
A positive absolute return is insufficient. Promotion requires evidence that the model adds information or execution value beyond a transparent rule under the same causal information set and realistic implementation assumptions.

## Literature notes
- Gencçay (2026), *What survives honest evaluation? Leakage-safe, search-aware assessment of LLM-driven trading strategy discovery*: point-in-time universes, realistic costs, search-aware evaluation, and benchmark comparison are central to credible certification.
- Saly-Kaufmann et al. (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*: evaluates OOS risk-adjusted performance together with significance, downside/tail risk, break-even costs, seed robustness, and computational efficiency.
- Zhang, Zhu & Linnainmaa (2025), *Man versus Machine Learning Revisited*: demonstrates that correcting look-ahead bias can eliminate apparently strong trading alpha.

## Current result
**Not tested yet.** The project README identifies the unresolved forward-label-overlap validation issue and the absence of the frozen candidate-level OOS matrix as blockers. No model is promoted on the basis of this hypothesis until those artifacts exist.
