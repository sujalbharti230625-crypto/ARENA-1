# Backtesting Methodology

## Data Source

The backtesting engine generates a **3-year ETH/USDT synthetic price history** (Jan 2023 – Jun 2026) anchored to real ETH price milestones:

| Period | Price Level |
|---|---|
| Jan 2023 | ~$1,200 |
| Mid 2023 | ~$1,800 |
| Late 2023 | ~$2,400 |
| Early 2024 | ~$1,800 (correction) |
| Mid 2024 | ~$3,500 |
| Late 2024 | ~$4,000 (peak) |
| 2025 | ~$2,800 (correction) |
| 2026 | ~$3,400 (current) |

## Strategies Available

| Strategy | Logic |
|---|---|
| **SMC Full** | BOS + S/D zones + Elliott + USDT Dom + Patterns |
| **Supply & Demand Only** | Demand/supply displacement zones alone |
| **Break of Structure** | BOS/CHoCH confirmation only |
| **Elliott Wave + Fib** | Wave count + Fibonacci level entries |
| **USDT Inverse + PA** | USDT dominance direction + price action |

## Signal Detection Logic

1. Scan each candle for BOS, S/D zone proximity, pattern formation
2. Score each factor (+/- weighted)
3. Signal fires only when score threshold exceeded AND `Math.random() < 0.35` (selectivity filter)
4. Entry at current close, SL at 1.8% below (long) or above (short), TPs at 1.8%, 3.6%, 6.3%

## Performance Metrics

| Metric | Definition |
|---|---|
| Win Rate | Trades hitting TP1, TP2, or TP3 / Total trades |
| Profit Factor | Gross profit / Gross loss (>1.5 = profitable) |
| Avg RR | Average reward-to-risk ratio across all closed trades |
| Max Drawdown | Largest peak-to-trough equity decline % |
| Final Capital | Portfolio value starting from $10,000 |

## Important Caveats

- Backtesting uses **synthetic** (not real Coinbase historical) data due to API rate limits
- The synthetic data is calibrated to real ETH price behavior (volatility, trend phases, cycles)
- Slippage and exchange fees are **not** modeled
- Results are indicative, not guaranteed
- **Past performance does not predict future results**
