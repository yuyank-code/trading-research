# Research 79 — Decision-Aware Objectives, Cost Frictions, and the Prediction-to-Trading Gap

## Date
2026-09-21

## Executive finding
The newest literature reinforces a design principle for this project: predictive accuracy should not be treated as the economic objective. A model can improve forecast metrics without improving net portfolio utility, especially when trading costs and turnover are material. However, decision-aware objectives are themselves adaptive choices and must therefore be nested and frozen before final OOS evaluation.

## Evidence

### 1. Cost-aware BTC walk-forward evidence
Bysik and Ślepaczuk (2026) evaluate XGBoost, LSTM and iTransformer on about 70,000 hourly BTC-USDT observations using 27 walk-forward folds. They report that naive sign strategies fail after 10 bps transaction costs, while a cost-aware forecast-magnitude filter reduces turnover and restores profitability in selected configurations. They also report that descriptive XGBoost superiority is not supported as formal statistical dominance.
Source: https://arxiv.org/abs/2606.00060

### 2. Smart Predict-then-Optimize
Wang and Hasuike (2026) explicitly study the mismatch between forecast accuracy and portfolio decision quality under realistic trading frictions and constraints. Their SPO formulation trains models against downstream optimization objectives rather than only pointwise prediction loss.
Source: https://arxiv.org/abs/2601.04062

### 3. Negative large-cap US equity benchmark
Bengoechea Pardo (2026) reports a leak-free, cost-aware benchmark on 30 large-cap US equities. In the reported experiment, the promoted MLP only marginally exceeded a no-ML Black-Litterman baseline while incurring more than three times cumulative transaction costs; an equal-weight portfolio was also close. This is useful negative evidence that sophisticated prediction can add little after the portfolio layer and costs.
Source: https://doi.org/10.2139/ssrn.6952859

### 4. Real-time AI benchmark
Koijen and Levy (NBER 2026) emphasize that historical training can create look-ahead problems and propose a real-time out-of-sample benchmark in which models only use information available at the contemporaneous event time. This supports strict information-cutoff accounting for any decision-aware model.
Source: https://www.nber.org/papers/w35431

### 5. Nonstationary FX and cost-aware multiwindow decisions
Grigoriev, Musaev and Grigorieva (2026) evaluate cost-aware multiwindow FX decision support with nonoverlapping walk-forward testing and net-of-cost utility, highlighting the joint importance of window choice, nonstationarity, turnover and execution thresholds.
Source: https://doi.org/10.1155/cplx/1155228

## Testable implication
H130 compares pointwise prediction optimization against a pre-declared decision-aware objective while holding the downstream portfolio and execution machinery fixed. The key quantity is incremental net OOS utility, not predictive accuracy.

## Falsification
The hypothesis fails if decision-aware optimization does not beat the pointwise model and strong non-ML baseline after realistic costs, or if its advantage disappears under 1.5x/2x costs, execution-lag perturbation, regime splits, placebo controls, or selection-aware inference.

## Project status
No numerical OOS result is claimed in this research note. The repository still requires corrected forward-label-overlap handling and the immutable prediction -> position -> turnover -> realized return -> full-cost artifact before historical model results can be treated as trustworthy.
