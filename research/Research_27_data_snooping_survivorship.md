# Research 27 — Data-Snooping, Universe Construction, and Survivorship Bias

## Why this matters

The project's validation gates already address model selection, costs, embargoes, null workflows, and candidate multiplicity. A separate source of false discovery is constructing the historical tradable universe with hindsight. If delisted, failed, or temporarily unavailable instruments are missing, a backtest can implicitly condition on survival.

The 2026 literature reviewed in this pass strengthens the case for treating the *research universe* as part of the model specification. Nikolopoulos shows that adaptive search can generate spurious predictive evidence under nulls; Kim's validation framework emphasizes that statistical prediction metrics can remain disconnected from economic validity; the large 2026 financial-time-series benchmark evaluates robustness across OOS periods, costs, and seeds.

## Research implication

The data pipeline should version the universe definition separately from feature/model code. Every instrument eligibility decision must carry an effective timestamp and source. Training and validation jobs must reconstruct the eligible universe as it was known at that date.

## New pipeline requirement

Before numerical promotion, produce a `universe_manifest` containing:

- instrument identifier;
- eligibility start/end timestamps;
- listing/delisting or availability source;
- liquidity/venue eligibility fields;
- timestamp at which each field became knowable;
- immutable data-version identifier.

The backtester must reject records whose eligibility timestamp is later than the decision timestamp.

## Experimental comparison

Run the exact same frozen candidate family over static versus point-in-time universes. Apply identical purging/embargoing, cost and impact assumptions, OOS confirmation, and multiplicity controls. Treat any post-hoc universe modification as a new research trial.

## Conclusion

Universe construction is now a first-class leakage surface. A strategy that survives this test gains evidence of robustness; a strategy that fails cannot be promoted merely because its model-level validation is clean.

**No numerical conclusion yet: the required point-in-time universe manifest and frozen candidate-level OOS matrix are not present in the repository.**
