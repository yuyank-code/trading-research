# Research 29 — Signal Decay, Holding Period, and Economic Robustness

## Literature synthesis

Recent financial ML validation work emphasizes that financial time series are non-stationary and that conventional walk-forward evaluation can still be vulnerable to false discoveries; combinatorial purged approaches provide a stronger stress test for model-selection risk. A 2024 Knowledge-Based Systems study found CPCV materially reduced backtest-overfitting risk in controlled experiments relative to simpler validation schemes. citeturn0search0

Research on intraday FX learning is also cautionary: computational learning methods can generate apparently significant in-sample and out-of-sample profits before transaction costs, while realistic costs eliminate statistical profitability in the tested setting. citeturn0search10

A 2026 BTC walk-forward study similarly reports that naive sign-based trading can fail under 10 bps costs and that cost-aware trade filtering can materially reduce turnover; importantly, the reported model differences were not supported as statistically dominant. This is crypto evidence, not an FX result, so it is used only to motivate a testable execution hypothesis. citeturn0search6turn0academia36

## Research question

Does the frozen trading signal possess a stable return half-life, or does profitability depend on a narrowly chosen holding period?

## Why this matters

Holding period determines label overlap, turnover, transaction costs, market-impact exposure, and effective sample size. Searching across horizons without correcting for the full search family creates another multiple-testing channel. A single winning horizon is therefore weak evidence.

## Experimental protocol

1. Freeze features, model family, training protocol, execution convention, and universe.
2. Pre-register a small horizon grid spanning short, medium, and longer holding periods.
3. Use explicit label end times and purge all training observations whose label windows overlap the validation interval.
4. Apply the same fixed embargo policy across the horizon family; do not tune embargo after seeing results.
5. Evaluate with chronological OOS folds and an untouched confirmation block.
6. Apply spread, commission, slippage, and impact assumptions consistently; repeat under adverse cost multipliers.
7. Preserve every horizon's OOS return series for DSR/PBO, SPA/Reality Check, and Model Confidence Set analysis.
8. Run matched-count randomized-signal and synthetic-zero-alpha controls.

## Primary outcomes

- net Sharpe / Sortino;
- maximum drawdown and tail loss;
- turnover and median holding time;
- break-even transaction cost;
- degradation under cost stress;
- fold-level sign consistency;
- statistical significance after accounting for the full horizon search.

## Falsification criteria

Reject the economic claim if the apparent edge:
- exists only at one isolated horizon;
- disappears under plausible cost/slippage stress;
- reverses sign across major chronological folds;
- is comparable to matched-count random controls;
- or loses significance after multiple-testing correction.

## Current conclusion

No empirical conclusion yet. The repository still requires the frozen candidate-level OOS prediction/return matrix before numerical claims can be made. The project README explicitly states that older model results remain untrusted until corrected validation addresses forward-label overlap. fileciteturn2file0
