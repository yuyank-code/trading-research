# Research 108 — Validation Gates: Evidence vs Selection

## Date
2026-09-22

## Question
Do composite backtest-robustness scores add evidence beyond their component statistical gates, or should the project retain the components separately and treat any composite only as reporting metadata?

## New literature

Santoni, Jouanne & Scullin (2026), *Equity Strategy Backtesting: Luck or Edge? The MinervaScore as a Statistical Robustness Grade*, combines Deflated Sharpe Ratio (DSR), Probability of Backtest Overfitting (PBO), Superior Predictive Ability (SPA), Minimum Track Record Length (MinTRL), and a regime-stability diagnostic. In synthetic markets with known ground truth, the score separates true signal from lucky backtests well, but in a pre-registered unseen real-market test its forward relationship was not significant (Spearman rho 0.013; one-sided permutation p=0.40). Therefore the composite should be treated as an auditable validation/reporting layer, not as evidence that a strategy will predict future returns.

Bailey & Lopez de Prado (2014), *The Deflated Sharpe Ratio*, establishes that the observed best Sharpe must be discounted for multiple testing and non-normality. The number of trials is part of the statistical evidence and cannot be ignored after selecting a winner.

Lalwani, Meshram & Jindal (2026), *Empirical Asset Pricing via Machine Learning: The Role of Research Design Choices*, finds large return dispersion across research-design choices in 5,376 ML portfolios. This supports recording the full research specification/search path rather than only the final model.

## Implications for this project

1. Keep DSR, PBO, SPA/related tests, and track-record requirements as separate auditable outputs.
2. Record every candidate and material research choice in the trial ledger, including discarded models and cost assumptions.
3. Do not use a composite robustness score as a model-selection feature unless a separate prospective test establishes incremental value.
4. Require any promoted candidate to pass the economic gate and statistical gates independently.
5. Use synthetic nulls and injected known signals to test whether our validation stack rejects false discoveries without rejecting known signal.

## Status
Literature synthesis only. No model performance is inferred from these papers, and no candidate is promoted.
