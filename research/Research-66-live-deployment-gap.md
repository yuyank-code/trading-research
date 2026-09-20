# Research 66 — Predictive Metrics vs Tradable Net Economics

## Date
2026-09-20

## Question
Does better prediction quality reliably produce better net trading performance after realistic execution costs and OOS validation?

## High-quality evidence reviewed

### 1. Saly-Kaufmann et al. (2026), Deep Learning for Financial Time Series
Large benchmark across daily futures from 2010–2025. The evaluation explicitly includes statistical significance, downside/tail risk, break-even transaction costs, random-seed robustness and computational efficiency. This is useful as a benchmark for what a serious model comparison should measure. The result should not be generalized into an unconditional claim that deep learning always beats linear models.

### 2. Lalwani, Meshram & Jindal (2026), European Financial Management
Across 5,376 ML portfolios, research-design choices materially changed profitability; reported nonstandard errors can be several times conventional standard errors. Only about one-third of portfolios remained significant after transaction costs. This supports treating research design as part of the uncertainty budget rather than a fixed implementation detail.

### 3. Bysik & Ślepaczuk (2026), Machine Learning-Based Bitcoin Trading Under Transaction Costs
A 27-fold walk-forward study of hourly BTC-USDT forecasts reports that naive sign-based strategies fail after 10 bps costs, while cost-aware forecast-magnitude filtering can reduce turnover and recover profitability in selected configurations. XGBoost is descriptively stronger in their experiments, but bootstrap evidence does not establish formal model dominance. This is directly relevant to the project's cost-gated execution work.

### 4. Shi (2025/2026), Journal of Economic Surveys
A survey of the transition from econometrics to ML in empirical asset pricing emphasizes the predictive-power/generalization tradeoff and the need to preserve econometric discipline when applying flexible models to noisy financial data.

### 5. Koijen & Levy (NBER Working Paper 35431, July 2026)
They argue that historical evaluation of AI systems can suffer look-ahead bias because models are trained on all available data, and propose a real-time out-of-sample benchmark around earnings announcements. This supports a stricter information-set timestamp and event-time cutoff in the project's data model.

## Synthesis
The literature does not support optimizing a trading research program around forecast accuracy alone. The correct object is the realized economic decision after the information cutoff, portfolio construction and execution costs. The strongest recurring requirements are:

- point-in-time information;
- genuinely out-of-sample evaluation;
- transaction-cost and break-even-cost analysis;
- research-design sensitivity;
- multiple-testing/search accounting;
- stochastic-seed robustness;
- comparison to transparent baselines.

## New protocol consequence
H116 converts this synthesis into an explicit falsification test. Candidate models must provide an immutable per-decision artifact connecting forecast -> position -> turnover -> cost components -> net realized return. Predictive metrics remain useful diagnostics, but they cannot be the promotion criterion.

## Negative evidence to preserve
If a model improves MSE, accuracy or IC but does not improve net OOS utility after costs, this is a valid and important failure: the model added prediction without tradable economic value.

## Numerical status
No new candidate performance number is claimed in this research pass. The immutable OOS matrix and corrected forward-label-overlap validation remain prerequisites for trustworthy numerical model comparison.

## Sources
- https://arxiv.org/abs/2603.01820
- https://onlinelibrary.wiley.com/doi/10.1111/eufm.70033
- https://econpapers.repec.org/paper/arxpapers/2606.00060.htm
- https://onlinelibrary.wiley.com/doi/10.1111/joes.70002
- https://www.nber.org/papers/w35431
