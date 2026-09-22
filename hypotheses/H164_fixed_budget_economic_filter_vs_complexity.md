# H164 — Fixed-Budget Economic Filter vs Model Complexity

## Hypothesis
Under an identical, pre-registered research budget, an economically constrained signal/execution filter will improve net out-of-sample decision utility more reliably than adding model complexity.

## Null
After correcting for search, costs, leakage controls, and regime dependence, additional model complexity provides equal or greater incremental net OOS utility than the economic filter.

## Experimental ladder

A. Frozen simple benchmark
B. Regularized linear model
C. Tree model
D. Sequence model
E. Higher-capacity attention model
F. Best pre-registered model + cost-aware forecast-magnitude filter

The total number of model/feature/horizon/filter trials is capped and recorded before the final OOS is opened.

## Primary endpoint
Paired net OOS utility versus the frozen benchmark on identical decision timestamps.

## Secondary endpoints
- turnover
- implementation shortfall proxy
- cost breakeven
- drawdown and tail loss
- performance by regime
- seed dispersion
- capacity sensitivity

## Promotion gates
1. PIT information audit passes.
2. Label-overlap purge/embargo passes.
3. Final OOS remains untouched until all model/search decisions are frozen.
4. Candidate-minus-baseline incremental utility remains positive under 1x, 1.5x and 2x costs.
5. No single seed or regime explains the result.
6. Multiple-testing/search adjustment remains supportive.
7. Execution implementation is deterministic across independent implementations.

## Failure conditions
- material PIT violation
- post-OOS parameter adjustment
- performance reversal under modest cost stress
- isolated seed/regime dependence
- candidate loses to a simpler frozen baseline after search correction

## Status
Registered. Numerical results are not yet claimed.