# Research 88 — Execution Timing: Auction vs Continuous Market

Date: 2026-09-21

## Research question

Can a fixed signal's net trading economics improve materially by changing only the execution venue/timing, rather than changing the alpha model?

## Literature signal

Goyal, Jegadeesh, and Wu (JFQA, 2026), *Price Impact in Closing Auctions, Opening Auctions, and Continuous Markets*, finds that closing auctions have lower price impact than continuous trading for most stocks, while opening auctions are relatively illiquid. For anomaly portfolios, reported annualized trading costs fall from roughly 17–41 bps to 9–21 bps in closing auctions when microcaps are excluded.

Shynkevich (Journal of Futures Markets, 2026), *Trading Periodicity and Algorithmic Divide in Cryptocurrency Markets*, finds recurring high-frequency activity can increase volatility and transaction costs, while the periods associated with proprietary algorithms contribute materially to price discovery.

Riera Abbade and Reali Costa (2026 preprint), *Realistic Market Impact Modeling for Reinforcement Learning Trading Environments*, finds that replacing fixed costs with nonlinear market-impact models can materially change both absolute performance and model rankings. This is preprint evidence and is treated as hypothesis-generating.

## Interpretation

Execution is an independent research dimension. If the same frozen predictions generate materially different net OOS outcomes solely because execution is moved between a continuous-market assumption and an auction/timing-aware assumption, the project should not attribute that improvement to better alpha.

Conversely, if the apparent advantage disappears after point-in-time liquidity constraints and realistic participation/impact costs, the execution hypothesis is rejected.

## Testable hypothesis H139

For a frozen signal and identical portfolio targets, a pre-specified execution-timing rule using a lower-cost auction/timing window will produce higher net out-of-sample utility than the project's default continuous-market execution assumption, after realistic spread, slippage, impact, and participation constraints.

## Required controls

1. Frozen predictions and positions: no model retraining between execution arms.
2. Default continuous-market execution.
3. Pre-declared auction/timing execution.
4. Randomized timing placebo with matched turnover.
5. Liquidity-constrained baseline.

## Leakage controls

- Execution rule is fixed before the outer OOS period.
- Any auction eligibility/liquidity variable must be available at decision time.
- No realized spread, closing price, or post-decision volume may determine the execution choice.
- Preserve exact decision, order, fill, and information timestamps.
- Correct label-overlap purging/embargo remains mandatory.

## Cost model

Every arm must include commission/fees, spread, slippage, nonlinear impact, participation/capacity limits, and any applicable borrow/funding costs. Stress the complete model at 1x, 1.5x, and 2x base costs and with execution-lag perturbations.

## Promotion criterion

The timing-aware arm is promoted only if its incremental net OOS utility over the frozen continuous-execution baseline remains positive under the pre-specified stress grid and does not depend on one regime, one liquidity bucket, or one timing parameter selected after observing OOS results.

## Current evidence status

No numerical OOS conclusion is claimed in this research note. The repository still requires corrected forward-label-overlap validation and an immutable prediction -> position -> execution -> net-P&L ledger before historical candidate results are considered trustworthy.

## Sources

- Goyal, Jegadeesh, Wu (2026), JFQA: https://www.cambridge.org/core/journals/journal-of-financial-and-quantitative-analysis/article/price-impact-in-closing-auctions-opening-auctions-and-continuous-markets-a-benchmark-for-cost-of-trading-on-anomalies/0F72910A79C5B42CF6E85F55164CE846
- Shynkevich (2026), Journal of Futures Markets: https://onlinelibrary.wiley.com/doi/10.1002/fut.70089
- Riera Abbade & Reali Costa (2026), arXiv: https://arxiv.org/abs/2603.29086
