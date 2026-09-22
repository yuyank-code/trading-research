# Research 113 — Search Budget and Economic Signal Filtering

## Date
2026-09-22

## Question
Does an economically constrained trading rule add more robust value than increasing predictive-model complexity when the total research/search budget is fixed?

## Literature synthesis

1. **Gençay (2026), leakage-safe, search-aware strategy discovery**: structural prevention of look-ahead is necessary; statistical corrections cannot rescue a deliberately leaky oracle. The system also records every evaluated strategy so the search itself enters the evidence calculation.
2. **Kim (2026), VALID**: across 340 crypto strategy variants, prediction metrics and trading economics can diverge sharply; transaction costs can consume most gross alpha. The study reports that CPCV + PBO materially reduces false positives versus prediction-only validation.
3. **Bysik & Ślepaczuk (2026)**: hourly BTC models can show positive gross results while naive sign trading fails after 10 bp costs; a forecast-magnitude execution threshold can reduce turnover and recover selected net profitability. Descriptive XGBoost superiority was not statistically established.
4. **Bailey & López de Prado (2014)**: selection over many trials inflates the observed Sharpe; the number and dependence structure of trials must enter the significance calculation.
5. **Santoni, Jouanne & Scullin (2026), MinervaScore**: a composite robustness score separated signal from luck in synthetic data, but showed no significant forward relationship in its preregistered unseen real-market test. Validation scores must therefore remain evidence layers, not alpha generators.
6. **Kelly, Malamud, Schwab & Xu (2026)**: point-in-time construction matters because temporally unrestricted information can contaminate historical financial inference.

## Testable implication

If economic signal filtering is genuinely useful, a fixed-budget pipeline should show lower turnover and stronger net incremental OOS utility without requiring a larger model/search space.

## Required controls

- point-in-time feature availability
- purge/embargo for overlapping labels
- immutable final OOS
- exact trial accounting, including rejected candidates
- realistic commission/spread/slippage/impact
- 1x/1.5x/2x cost stress
- execution-delay stress
- paired candidate-minus-baseline inference
- seed aggregation for stochastic models
- regime and capacity diagnostics
- no post-OOS tuning

## Interpretation rule

Do not promote a strategy because a cost filter improves one backtest. The filter must be preregistered, applied without OOS tuning, and demonstrate incremental net utility over a frozen baseline across cost and regime stress.

## Current status

Hypothesis registered. This is a research protocol, not evidence of alpha. Existing repository status remains blocked until a complete PIT-safe candidate-level OOS artifact is produced.