# Research 36 — Metric Invariance and Decision Utility in Financial ML

## Research question
Can a trading model be considered robust when its apparent superiority depends on which evaluation metric the researcher chooses after seeing results?

## Literature synthesis

### 1. Beyond-accuracy validation
Kim (2026), *Beyond Accuracy: A Validation Framework for Machine Learning in Cryptocurrency Trading*, reports that AUC-only validation can produce high false-positive rates and that strategies surviving permutation-style checks can still fail combinatorial purged cross-validation, PBO, and Deflated Sharpe Ratio tests. The paper argues for ordered statistical and economic gates rather than a single predictive metric.

### 2. Large-scale financial time-series benchmarking
Saly-Kaufmann et al. (2026), *Deep Learning for Financial Time Series: A Large-Scale Benchmark of Risk-Adjusted Performance*, evaluates models on daily futures across commodities, equity indices, bonds, and FX from 2010–2025. The benchmark explicitly considers statistical significance, downside/tail risk, break-even transaction costs, random-seed robustness, and computational efficiency alongside Sharpe performance. This supports treating model quality as a vector of economic outcomes rather than a single leaderboard score.

### 3. Research-design sensitivity
Lalwani et al. (2025/2026), *Empirical Asset Pricing via Machine Learning: The Role of Research Design Choices*, studies 5,376 portfolios and finds that choices such as training-window length, filters, and portfolio construction can materially change reported returns. The nonstandard errors of ML strategies can be several times the conventional standard errors. This is direct evidence that the evaluation specification itself is a source of uncertainty.

### 4. Realistic frictions change rankings
Riera Abbade and Reali Costa (2026), *Realistic Market Impact Modeling for Reinforcement Learning Trading Environments*, reports that changing from fixed transaction costs to nonlinear market-impact modeling materially changes both absolute performance and the ranking of algorithms. This reinforces the need to evaluate candidates over a cost-model family instead of selecting a model under one convenient cost assumption.

### 5. Spurious predictability under adaptive search
Nikolopoulos (2026), *Spurious Predictability in Financial Machine Learning*, proposes falsification against zero-predictability and microstructure placebo reference classes. The paper shows adaptive specification search can generate significant walk-forward evidence under null processes. A metric selected after the search is therefore another potential selection channel.

## Testable implication
If candidate rankings are unstable across pre-registered economic metrics, the project should interpret the result as specification-sensitive rather than as strong evidence for one model. If rankings remain stable and candidates survive MCS/SPA/DSR/PBO plus cost and placebo controls, the evidence becomes materially stronger.

## Planned experiment
H85 freezes the candidate set and OOS return matrix first. Then compute a metric panel containing net Sharpe, Sortino, maximum drawdown, expected shortfall, turnover/cost burden, break-even cost, and benchmark-relative net value. Compare rank correlations, top-k overlap, and Model Confidence Set membership. Repeat the same analysis on matched-count placebo and synthetic zero-alpha candidates.

## Current limitation
No numerical conclusion is claimed yet. The repository's existing blocker remains: forward-label-overlap validation must be corrected and the immutable candidate-level OOS prediction/return matrix must exist before historical candidate performance can be trusted.

## Sources
- Jaewook Kim (2026), SSRN 6508779.
- Adir Saly-Kaufmann, Kieran Wood, Jan Peter-Calliess, Stefan Zohren (2026), arXiv:2603.01820.
- Varun Jindal / Lalwani et al. (2025/2026), European Financial Management, DOI 10.1111/eufm.70033.
- Lucas Riera Abbade, Anna Helena Reali Costa (2026), arXiv:2603.29086.
- Sotirios D. Nikolopoulos (2026), arXiv:2604.15531.
