# Research 95 — Economic Restrictions and Latent-Factor Stability

Date: 2026-09-22

## New evidence

Chen, Wang and Huang (International Review of Economics & Finance, 2026), “Variational Autoencoder Asset Pricing models with economic restrictions,” reports that variational regularization plus economically motivated restrictions can improve out-of-sample predictive R², information coefficients, Sharpe ratios and long-short returns relative to linear and unconstrained autoencoder benchmarks. The paper argues that high-dimensional asset pricing has a low signal-to-noise ratio and that flexible latent-factor models can overfit.

Source: https://doi.org/10.1016/j.iref.2026.105402

The result is promising but cannot be transplanted directly into this project: the paper uses U.S. equity data and a particular factor-learning architecture, while our promotion standard requires point-in-time information, corrected purging/embargo, realistic execution costs and explicit multiple-testing accounting.

## Research implication

Economic restrictions should be tested as a regularizer, not accepted as an automatic alpha source. The central question is whether economically anchored latent representations improve net OOS utility after the extra modeling choices are charged to the research budget.

## Design requirements

- Freeze the feature universe before comparing restricted and unrestricted variants.
- Fit all normalization, factor extraction and restriction parameters only on the training/validation data available at each decision date.
- Keep the final holdout single-use.
- Compare against a strong linear/shrinkage factor baseline and a capacity-matched flexible baseline.
- Report predictive metrics separately from portfolio/economic metrics.
- Include commissions, spread, slippage, nonlinear impact, turnover and capacity where applicable.
- Stress costs at 1x, 1.5x and 2x and perturb execution lag.
- Preserve all seeds and failed trials; do not report the best run as representative.
- Require placebo/null controls to pass before interpreting improvements as genuine signal.

## Decision rule

Do not promote the architecture unless the economically restricted variant beats the pre-specified flexible and shrinkage baselines on untouched net OOS utility and the advantage survives cost stress, design perturbations and null/placebo controls.
