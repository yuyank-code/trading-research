# Research 31 — Null-Calibrated Abstention in Cost-Aware Trading ML

## Status
Literature synthesis supporting H80. No empirical promotion claim.

## Question
Can a trading model improve economically by refusing to trade when its forecast is too weak to overcome execution costs, without turning the abstention threshold into another overfit parameter?

## Literature evidence

### Selective deployment
A January 2026 preprint, *When Not to Trade: Leakage-Aware Selective Machine Learning for Factor Rotation*, formalizes a rolling-origin protocol in which a model is deployed only when its validation improvement over a transparent fallback exceeds a calibrated threshold. The reported sector-rotation experiment is encouraging, but it is not evidence for FX and remains a preprint; the relevant contribution for this project is the separation of fitting, validation calibration, and untouched testing.

### Transaction-cost interaction
A May 2026 walk-forward study of hourly BTC-USDT finds that naive sign trading can fail after a 10-bps transaction cost and that a forecast-magnitude execution filter can restore profitability in selected configurations. The study also reports that model ranking is not statistically decisive under bootstrap testing. This supports testing the execution decision separately from the forecast model rather than assuming a better forecast automatically produces a better strategy.

### Overfitting controls
Bailey et al. document how repeated backtest search creates false discoveries. Deflated Sharpe Ratio and Probability of Backtest Overfitting are therefore required whenever a threshold or gating rule is selected from a candidate family. Purged/embargoed validation remains necessary whenever forward labels overlap.

## Transferable implication
The strongest testable claim for our project is not that abstention creates alpha. It is narrower: conditional on an already specified predictive signal, can a small, pre-registered abstention rule improve net utility without increasing false discoveries under a matched search budget?

## Proposed test
Freeze the candidate model and all upstream choices. Inside each causal validation origin compare an always-trade baseline with a fixed cost-based gate and a small pre-registered validation grid. Never tune the gate on the confirmation block.

The null experiment uses placebo forecasts with identical search budget and validation geometry. This estimates whether the gating mechanism itself can manufacture apparent improvement.

Primary metrics: net Sharpe, Sortino, maximum drawdown, turnover, abstention rate, trade count, break-even cost and confirmation degradation. Secondary diagnostics: fold sign consistency, tail concentration, DSR/PBO, SPA/Reality Check and Model Confidence Set.

## Critical limitation
The repository still does not contain the frozen candidate-level OOS prediction/return matrix, and README.md records an unresolved forward-label-overlap issue. Therefore this research cannot yet produce an honest numerical result.

## Sources
- Guo (2026), *When Not to Trade: Leakage-Aware Selective Machine Learning for Factor Rotation*, SSRN 7021298.
- Bysik & Ślepaczuk (2026), *Machine Learning-Based Bitcoin Trading Under Transaction Costs: Evidence From Walk-Forward Forecasting*, arXiv:2606.00060.
- Bailey & López de Prado (2021), *How “backtest overfitting” in finance leads to false discoveries*, Significance.
- Bailey, Borwein, López de Prado & Zhu (2015), *The Probability of Backtest Overfitting*, Journal of Computational Finance.

## Conclusion
H80 is worth testing because it attacks a concrete economic bottleneck—weak forecasts that do not clear trading costs—while explicitly treating threshold selection as a source of multiple testing. No evidence of FX profitability is claimed until the frozen OOS artifacts and corrected causal validation are available.
