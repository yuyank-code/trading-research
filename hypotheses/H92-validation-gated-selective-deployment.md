# H92 — Validation-Gated Selective Deployment

## Hypothesis
A trading model should trade only when a causal, validation-only estimate indicates that its expected net utility exceeds a frozen transparent fallback benchmark by a pre-registered margin. Otherwise it should abstain or use the fallback. This can improve net risk-adjusted performance and reduce turnover without using confirmation-period information.

## Motivation
Recent 2026 research reports that selective deployment can reduce turnover and improve net Sharpe when signals are weak or trading frictions are high, while other large cost-aware benchmarks find that apparently sophisticated ML improvements can be marginal versus simple baselines. The test therefore targets incremental economic value, not predictive accuracy.

## Pre-registration
- Candidate signal: the existing frozen candidate set; no new model family is introduced by this hypothesis.
- Fallback: frozen transparent benchmark defined before confirmation scoring.
- Gate inputs: validation-window net utility, uncertainty/confidence proxy, and realized execution-cost estimate available at decision time only.
- Gate threshold: selected only inside training/validation folds; never tuned on confirmation.
- Confirmation: untouched and scored once under the existing leakage, purging/embargo, cost, impact, and multiplicity protocol.
- Primary comparison: always-trade candidate vs gated candidate vs fallback, all using identical execution assumptions.
- Required outputs: net Sharpe/Sortino, drawdown, turnover, break-even cost, benchmark-relative return, trade count, abstention rate, and worst-subperiod performance.

## Falsification criteria
Reject H92 if the gated rule does not improve benchmark-relative net utility, if its improvement disappears under adverse cost/slippage stress, if the gate requires confirmation-period tuning, or if a matched null-search produces comparable gains.

## Leakage controls
The gate must be predictable: at date t it may use only information available by t. Validation data used to calibrate the gate must be separated from confirmation data. No threshold, abstention rule, or fallback choice may be altered after confirmation results are observed.
