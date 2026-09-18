# H67 — Null-Workflow Falsification Audit

## Hypothesis
A valid trading research pipeline should not produce statistically convincing out-of-sample alpha when the predictive relationship is destroyed while preserving the empirical structure of the data.

## Motivation
Recent financial-ML research proposes falsification audits using synthetic zero-predictability reference classes and microstructure placebos. The key lesson is complementary to DSR/PBO/SPA: statistical correction can discount selection among trials, but it cannot prove that the information flow is causal or that the workflow behaves correctly under a known-null process.

## Test design

1. Freeze the entire candidate-generation and evaluation pipeline before inspecting null results.
2. Construct null controls that preserve, as far as possible, return autocorrelation, volatility clustering, cross-sectional dependence and missingness while destroying predictive alignment.
3. Run the identical feature engineering, model fitting, thresholding, position sizing and execution-cost simulator used for genuine candidates.
4. Keep the full search ledger, including every null candidate and failed run.
5. Apply the same purged/embargoed OOS protocol and the same realistic spread, commission, slippage and impact assumptions.
6. Apply DSR/PBO and family-level Reality Check/SPA to the null candidate family.
7. Repeat with a microstructure placebo where the feature timestamps are shifted so that any apparent relationship is causally impossible.

## Falsification criteria

The pipeline fails H67 if null or placebo workflows repeatedly generate apparently deployable OOS results, especially if they survive the project's normal promotion gates. Any such result blocks model promotion until the source of the artifact is identified.

## Positive result interpretation

Passing the null audit does **not** establish profitable predictability. It only demonstrates that the research machinery does not obviously manufacture alpha under the selected null controls.

## Required reporting

- null construction and random seeds;
- number of genuine and null trials;
- best and distributional OOS Sharpe;
- DSR/PBO/SPA results;
- break-even transaction cost;
- turnover and drawdown;
- placebo leakage detection rate;
- complete search ledger hash.

## Decision rule

No candidate can reach final confirmation unless the complete workflow passes H67 and all earlier causal, cost, capacity and multiple-testing gates.
