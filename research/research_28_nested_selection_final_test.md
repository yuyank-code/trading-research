# Research 28 — Nested Selection, Search Exposure, and Final-Test Quarantine

## Core finding
A final holdout is only informative if it has remained outside every adaptive decision. If model family, features, thresholds, costs, embargoes, or deployment rules are changed after observing the holdout, the holdout becomes another training signal and its nominal p-value is no longer credible.

## High-quality evidence
- Zhang, Zhu & Linnainmaa, *Man versus Machine Learning Revisited*, Review of Financial Studies (2025): correcting a look-ahead problem erased the reported alpha and left linear models competitive.
- Wang, *Too Good to Be True: Look-Ahead Bias in Empirical Options Research*, Review of Financial Studies (published June 30, 2026): seemingly exceptional Sharpe ratios can result from filtering with information unavailable at formation time.
- Arian, Norouzi Mobarekeh & Seco, *Backtest overfitting in the machine learning era* (Knowledge-Based Systems, 2024): controlled experiments find CPCV better at mitigating overfitting than simpler OOS schemes under nonstationarity and dependence.
- Gençay, *What survives honest evaluation?* (2026 preprint): records strategy-search exposure explicitly and shows that leakage-safe, search-aware evaluation can reject apparently attractive LLM-generated strategies.

## Project implication
The trading-research pipeline should have three immutable phases:

1. **Development:** research, feature engineering, model selection and cost-model selection.
2. **Validation:** repeated purged/embargoed OOS evaluation used only for decisions explicitly allowed by the protocol.
3. **Confirmation:** one locked specification evaluated on an untouched block. No threshold tuning, feature deletion, universe changes, cost changes or model replacement may follow from confirmation performance.

The registry should record every adaptive decision and attach a monotonically increasing search/evaluation identifier to each candidate. Confirmation results must be stored separately from development results and must not feed subsequent model selection.

## Testable consequences
- Development-to-confirmation degradation should be quantified rather than hidden.
- A large degradation is evidence of selection pressure, not something to be repaired by retuning on the confirmation block.
- Under synthetic zero-alpha data, the complete process should not systematically produce apparently successful confirmed strategies.
- If multiple candidates are indistinguishable in confirmation, choose the simpler candidate rather than reopening the confirmation set.

## Status
Literature synthesis and protocol update. Numerical claims about the project's own model remain blocked until the frozen candidate-level OOS predictions/returns and point-in-time data are available.
