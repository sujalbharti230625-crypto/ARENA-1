# ETH/USDT Smart Money Terminal — Final Release

## Files
| File | Description |
|------|-------------|
| `index.html` | Main terminal — Live price, SMC chart, signals, backtesting |
| `tradeplan.html` | Trade Plans — Scalp / Intraday / Swing with live analysis |
| `final-setup.html` | High-confidence setup card with risk calculator |

## Features
- **Live data**: OKX API primary → Coinbase fallback → CoinGecko fallback
- **SMC analysis**: BOS, CHoCH, Supply/Demand zones, Liquidity pools, Elliott Wave
- **TradingView embed**: BINANCE:ETHUSDT iframe (all TFs: 1m/5m/15m/1H/4H/1D)
- **Backtesting**: Delta Exchange fees (maker=taker=0.01%), partial exits, equity curve
- **Auto-calibration**: TP/SL/score-gate adapts from backtest results → live signals
- **Zero dependencies**: Pure HTML + CSS + JS, no npm, no build step

## Usage
Open any file directly in a browser — no server required.

## Data Sources
- Price: `https://www.okx.com/api/v5/market/ticker?instId=ETH-USDT`
- Candles: `https://www.okx.com/api/v5/market/candles?instId=ETH-USDT`
- USDT Dom: `https://api.coingecko.com/api/v3/global`
- Delta fees verified: `api.delta.exchange/v2/products/ETHUSDT` (0.01% maker/taker)

## Version
- Built: June 2026
- Status: Production-ready, zero known bugs
