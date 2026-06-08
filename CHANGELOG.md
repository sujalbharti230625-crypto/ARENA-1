# Changelog

## v4.0 — 2026-06-08 (Current)
### Critical Fixes
- `btReason()` called `_sr()` (local scope only) → `ReferenceError` on every trade log render — replaced with deterministic round-robin counter
- `tradingView` set to `display:'grid'` in `init()` but CSS requires `flex` → layout broken on load
- `sigFreshness` styled HTML was built then immediately destroyed by a stale `textContent` overwrite

### High Impact
- Analysis tab: `renderAnalysis()` crashed on empty `S.ms` → added loading guard + `computeAll()` pre-call
- Candle interval checked `tradingView.display !== 'none'` (always true) → now uses `S.loaded && !hidden`
- `calcRisk()` in Trade Plans showed `$0.00` for all levels before first API call → ATR fallback %
- `genHist()` with 15m×3y = 105k bars → browser freeze → capped at 5000 bars
- Final-setup TP levels hardcoded ($1,617 etc) → now computed relative to live entry price

### Medium Fixes
- `validTP()` null-guarded (elements inside dynamic `renderBT()` innerHTML)
- `init()` fetch chain now has `.catch()` → no infinite spinner on network failure
- Duplicate `.page.active{display:block}` CSS rule removed
- `runStrictAnalysis()` wrapped in `try/catch` in Trade Plans
- `net/cap` NaN guard when cap=0 in final-setup
- `S.btStyle` default changed from `'swing'` to `'intraday'` (matches UI default active card)
- `renderBT()` idempotent — re-run safe, no stale DOM rebuild
- `readCfg()` fully null-safe via `_gv()` helper with defaults
- Auto-calibration: `btReason`, `scoreThresh`, `STYLE_P` propagate back to live signal engine

## v3.0 — 2026-06-08
- Layout: pages use `position:absolute` fill inside `position:relative` workspace
- Backtest: `renderBT()` called before element access — no null crashes
- Trade Plans: load overlay auto-dismisses after 7s + skip button

## v2.0 — 2026-06-08
- Auto-calibration engine: backtest results → adaptive TP/SL/score params
- Deterministic LCG replaces `Math.random()` in `genHist()`/`synthCandles()`
- `aMax()`/`aMin()` NaN-safe, `esc()` null-safe
- Tab visibility: pause/resume fetch intervals

## v1.0 — 2026-06-08
- Initial release: 3-file static HTML terminal
- OKX → Coinbase → CoinGecko fallback chain
- CSS Grid dual-chart layout (SMC canvas / TradingView iframe)
- 8-factor strict signal engine in Trade Plans
- Delta Exchange fee structure verified (0.01% maker/taker)
