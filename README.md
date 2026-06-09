# ETH/USDT Smart Money Terminal

A fully self-contained, zero-dependency professional trading terminal for ETH/USDT — built with pure HTML/CSS/JS. No build step, no Node.js, no npm. Drop into any static host (GitHub Pages, Netlify, Vercel) and it works instantly.

---

## 📁 Files

| File | Description |
|------|-------------|
| `index.html` | Main terminal — live price, canvas chart, signal engine, backtesting |
| `tradeplan.html` | Trade plan engine — Scalp / Intraday / Swing tabs with live analysis |
| `final-setup.html` | High-conviction setup card — price ladder, risk calculator |

---

## 🚀 Deploy to GitHub Pages

1. Fork or upload these 3 files to a GitHub repository
2. Go to **Settings → Pages → Source → main branch / root**
3. Done — your terminal is live at `https://yourusername.github.io/your-repo/`

---

## ✨ Features

### Live Data (OKX → Coinbase → Synth fallback)
- Real-time ETH/USDT price via OKX API (CORS-friendly)
- Candles: 15m / 1H / 4H / 1D / 1W
- USDT Dominance via CoinGecko (inverse ETH correlation)

### 6-Tier Top-Down Cascade Analysis
Full SMC hierarchy enforced at every level:
```
Yearly → Weekly → Daily → 4H → 1H → 15m
```
- **1H Conflict Hard Block**: Engine never fires a trade when 1H opposes the cascade direction. Shows "⏳ WAITING FOR 1H CONFIRMATION" with exact trigger conditions (CHoCH/BOS required).
- **15m micro-gate**: Final execution filter once 1H is confirmed

### Signal Engine (Pure Price Action — Zero Lagging Indicators)
- Break of Structure (BOS) + Change of Character (CHoCH)
- Supply & Demand zones (fresh vs tested)
- Liquidity pools (BSL / SSL sweep detection)
- Elliott Wave labelling
- USDT Dominance inverse correlation
- Candle pattern recognition (Hammer, Shooting Star, Doji, Strong Body)

### Backtesting Engine (Delta Exchange fees)
- Verified Delta Exchange fee structure: maker = taker = **0.01%**
- Funding rate: ~0.005% / 8h
- Partial exits at TP1 (40%) → TP2 (35%) → TP3 (25%)
- Auto-calibration: derives optimal TP/SL multipliers from backtest results
- 6-tier cascade hard blocks applied identically to live engine
- Cascade alignment breakdown: aligned WR vs counter WR vs h4/1H clash WR
- CSV export of full trade log

### TradingView Chart Embed
- Live BINANCE:ETHUSDT candlestick chart (iframe, no indicators)
- Switchable intervals: 15m / 1H / 4H / 1D / 1W

### Canvas Price Chart
- DPR-aware (crisp on Retina/HiDPI)
- Supply/Demand zone overlays
- Signal level overlays (Entry / SL / TP1 / TP2 / TP3)
- Liquidity level overlays
- Elliott Wave annotations

---

## 🧠 SMC Logic — 1H Conflict Rule

> **BEAR cascade + 1H BULL = pullback phase. NO SHORT until 1H forms a BEAR BOS/CHoCH.**

This is the core rule. The engine enforces it with layered hard blocks:

| Condition | Action |
|-----------|--------|
| 4H BEAR + 1H BULL | Block ALL trades (both directions) |
| 4H BULL + 1H BEAR | Block ALL trades (both directions) |
| BEAR cascade + counter-trade | Blocked at macroStr ≥ 25% |
| 1H agrees + 15m opposes | Score capped below threshold, show "wait for 15m BOS" |
| All 6 TFs aligned | Full size, max score (+20 bonus) |

---

## 📊 Scoring System

| Factor | Weight |
|--------|--------|
| Top-Down Cascade (macro bias) | 25–35 pts |
| 1H gate (confirms cascade) | +12 pts |
| 15m gate (final execution) | +6 pts |
| 4H BOS (cascade-aligned) | +22 pts |
| 1H BOS (cascade-aligned) | +14 pts |
| Supply/Demand zone | +13–20 pts |
| Liquidity (BSL/SSL) | ±8 pts |
| USDT Dominance | ±3–10 pts |
| Candle pattern | +2–12 pts |
| Volume | ±5–10 pts |
| Perfect 6-TF stack bonus | +20 pts |

**Signal threshold: 60 pts** (configurable via auto-calibration)

---

## ⚙️ Fee Structure (Delta Exchange ETHUSDT Perpetual)

- Maker: **0.01%** (0.0001)
- Taker: **0.01%** (0.0001)
- Funding: **~0.005% / 8h** typical
- Source: `api.delta.exchange/v2/products/ETHUSDT` — verified June 2026

---

## 🔧 Technical Notes

- **No optional chaining** (`?.`) — Safari <14 compatible
- **No `Math.max(...array)` spread** — uses `aMax()`/`aMin()` loop helpers (no RangeError)
- `'use strict'` in all scripts
- DOMContentLoaded + double `requestAnimationFrame` init pattern
- GPU compositing CSS (`will-change: transform`, `backface-visibility: hidden`) on sticky elements
- All `fetch()` chains have `.catch()` handlers
- `clearInterval` on all `setInterval` handles
- Canvas: DPR scaling, `ctx.translate(0.5, 0.5)` sub-pixel sharpness, `alpha: false` for perf

---

## 📡 API Endpoints Used

| Data | Primary | Fallback |
|------|---------|----------|
| Price tick | `okx.com/api/v5/market/ticker?instId=ETH-USDT` | Coinbase |
| Candles | `okx.com/api/v5/market/candles?instId=ETH-USDT&bar={tf}` | Coinbase → Synth |
| USDT Dominance | `api.coingecko.com/api/v3/global` | Estimated from price delta |

---

## 📌 Version History

| Version | Changes |
|---------|---------|
| v16 | **1H conflict hard block** — engine never fires trades when 1H opposes cascade; Factor 1 penalty −5→−30; h4_1h_conflict only penalises counter-cascade direction; Factor 6 candles gated on 1H state; BT hard blocks tightened |
| v15 | Bug fixes: `allBear`/`allBull` undefined in context; `topDown` fallback missing fields; allBear5 used `trend15` instead of `m15B` |
| v14 | Full 6-tier cascade: 15m tier integrated in both live engine and BT; post-scoring cascade cap |
| v13 | Auto-calibration engine; cascade-gated scoring (S/D ×0.30, candles ×0.25 counter-cascade) |
| v12 | BT multi-TF dataset; 5-tier cascade in backtest; position sizing rules |
| v11 | TradingView iframe embed; DPR canvas chart |

---

*Built for educational and research purposes. Not financial advice.*
