# Trading Research

A continuously audited research record for systematic trading and quantitative finance.

## Purpose

This repository stores the **research itself**, not just code. Each meaningful research pass should leave a readable, reproducible record here.

## Research standards

- Start from high-quality academic and practitioner literature.
- Convert claims into explicit, testable hypotheses.
- Separate theory, empirical evidence, implementation evidence, and speculation.
- Use point-in-time information wherever possible.
- Prevent look-ahead, survivorship, selection, and label-overlap leakage.
- Use purged/embargoed out-of-sample validation where appropriate.
- Include realistic commissions, spread, slippage, market impact, borrow costs, turnover, and capacity where relevant.
- Account for multiple testing and research selection effects.
- Preserve meaningful failures as carefully as successes.
- Never promote a strategy based only on in-sample performance.

## Structure

- `research/` — theoretical literature reviews and research synthesis
- `hypotheses/` — explicit testable hypotheses
- `experiments/` — experiment designs and protocols
- `findings/` — validated findings and results
- `failures/` — rejected hypotheses, bugs, and invalidated results
- `sources/` — bibliography and source notes

## Current research status

The project is currently expanding the theoretical foundation while hardening the experimental pipeline. A previously identified issue involved forward-label overlap at walk-forward boundaries; corrected validation must be used before older model results are treated as trustworthy.

## Research principle

> Complexity must earn its place through genuinely out-of-sample, cost-aware, reproducible evidence.
