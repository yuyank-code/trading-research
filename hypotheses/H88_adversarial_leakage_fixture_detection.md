# H88 — Adversarial Leakage Fixture Detection

## Hypothesis
The evaluation pipeline should detect deliberately injected future-information leaks and reject the resulting strategy before performance statistics are considered evidence.

## Motivation
Recent leakage-safe trading research shows that statistical corrections such as DSR/PBO are not sufficient by themselves: a deliberately leaky oracle can exhibit extreme performance while surviving statistical overfitting corrections. Leakage therefore has to be prevented structurally and tested with adversarial fixtures.

## Test design
1. Freeze the clean feature/label registry and evaluator.
2. Create paired clean and adversarial datasets with identical timestamps and schema.
3. Inject only controlled future information into the adversarial fixture (future return, future volatility, and future rank variants).
4. Run the complete pipeline without changing model-selection settings.
5. Require the evaluator to fail closed on the adversarial fixture and pass the clean fixture.
6. Repeat across walk-forward, purged/embargoed and CPCV paths.

## Pass criteria
- Every explicit future-information fixture is detected or produces a materially degraded/invalid result.
- No leaked fixture is allowed to reach promotion status even if DSR, PBO, Sharpe or benchmark-relative performance looks exceptional.
- Clean and adversarial manifests are distinguishable and reproducible.
- Detection does not rely on inspecting final performance.

## Failure interpretation
A failure is a pipeline-security failure, not evidence about market alpha. It blocks all model promotion until corrected.

## Required artifacts
- fixture definitions and hashes;
- leakage detector logs;
- feature availability timestamps;
- fold-level train/test manifests;
- clean vs adversarial comparison report.
