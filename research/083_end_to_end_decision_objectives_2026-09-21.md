# Research 83 — End-to-End Decision Objectives vs Two-Stage Prediction

Date: 2026-09-21

## Question

Does optimizing the downstream trading objective directly improve genuinely out-of-sample net utility relative to a two-stage pipeline that first optimizes return prediction and then converts forecasts into positions?

## New evidence

### AlphaGlass (Bell, Kakhbod, Lettau, Nazemi, NBER 2026)

AlphaGlass proposes an interpretable ML portfolio architecture that maps characteristics into additive signals, uses a differentiable rank-and-mask layer, and directly optimizes investment objectives such as Sharpe ratio or mean-variance utility. The paper reports strong out-of-sample U.S. equity results and emphasizes traceable characteristic contributions.

Source: https://www.nber.org/papers/w35186

### AlphaPortfolio (Cong, Tang, Wang, NBER 2026)

AlphaPortfolio uses attention/transformer sequence representations and reinforcement learning to optimize portfolio-management objectives directly, including objectives that are not period-by-period additive. The authors report strong out-of-sample results and explicitly allow transaction costs and state interactions in the objective.

Source: https://www.nber.org/papers/w35195

### Large-scale deep-learning benchmark (Saly-Kaufmann et al., 2026)

A large futures benchmark evaluates models on risk-adjusted trading outcomes rather than prediction metrics alone, including statistical significance, tail risk, breakeven transaction costs, random-seed robustness and computational efficiency. This supports treating trading utility as the final evaluation target, while retaining strong baselines and cost stress.

Source: https://arxiv.org/abs/2603.01820

## Interpretation

These studies motivate a test, not a conclusion. Directly optimizing a portfolio objective can potentially avoid a mismatch between forecast accuracy and trading utility. But direct objective optimization also creates additional degrees of freedom and therefore an additional selection channel. A stronger in-sample objective is not evidence of better tradability.

## Testable hypothesis H134

A decision-aware model trained against a downstream portfolio objective will improve net out-of-sample utility versus an otherwise matched two-stage predictive model, without requiring materially higher turnover or a more favorable cost model.

## Controlled experiment

Compare:

1. Two-stage baseline: predict next-period return, then apply a frozen position rule.
2. Decision-aware model: train the same feature information against a portfolio utility objective.
3. Strong non-ML baseline.
4. Matched-capacity placebo / shuffled-label control.

Keep fixed across arms:

- information timestamps;
- universe and survivorship policy;
- target horizon;
- execution timestamp;
- portfolio constraints;
- commission, spread, slippage and impact model;
- cost-stress multipliers;
- validation folds;
- final OOS dates.

## Leakage and selection controls

- Fit preprocessing inside each training fold only.
- Purge observations whose labels overlap the validation/test horizon.
- Embargo after training windows where needed.
- Never tune the direct utility objective on the final OOS period.
- Log every objective, architecture, hyperparameter and failed candidate in the trial ledger.
- Apply the same search budget and selection accounting to the baseline and decision-aware arms where feasible.

## Economic tests

Report:

- net return and annualized Sharpe;
- downside/tail metrics;
- turnover;
- cost contribution by commission/spread/slippage/impact;
- break-even cost;
- 1x, 1.5x and 2x cost stress;
- execution-lag stress;
- regime/subperiod stability;
- candidate-minus-baseline incremental utility.

The decision-aware model fails promotion if its advantage disappears under realistic costs, if it depends on a single cost specification, or if it only appears after a larger search budget.

## Status

Hypothesis only. No numerical OOS claim is made until the immutable row-level OOS accounting artifact exists and corrected label-overlap validation is enforced.
