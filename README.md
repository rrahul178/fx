# Rahul Dada · Ultimate ICT + UT Bot FX Scanner

A single-file, client-side Forex signal scanner combining a 6-layer ICT
(Inner Circle Trader) confluence engine with UT Bot Alerts and a 4H
higher-timeframe trend filter. Runs entirely in the browser — no backend,
no build step.

**⚠️ Educational purposes only. Not financial advice. No signal system
guarantees profits — always use proper risk management.**

## Features

- **6-Layer ICT Engine** — Market Structure (BOS), Premium/Discount Zone,
  FVG/Order Block detection, Liquidity Sweep, Candlestick pattern trigger,
  and UT Bot confluence.
- **4H HTF Trend Filter** — built locally from the fetched 1H candles
  (EMA 10/30 crossover), no extra API calls. Counter-trend setups are
  rejected outright rather than just down-weighted.
- **20 Price Action Patterns** — Doji, Hammer, Engulfing, Harami, Morning/
  Evening Star, Three White Soldiers/Black Crows, and more.
- **UT Bot Alerts** — Pine Script v6 ATR trailing-stop logic ported to JS.
- **Signal History & Win-Rate Tracker** — every `VALID` signal is logged
  locally (localStorage) with a 1:2 risk-reward target, and automatically
  marked WIN/LOSS as price moves. Gives you a real, measured accuracy
  instead of a guess.
- **Telegram Alerts** — optional push notification on every new valid setup.
- **Live Mode** — auto re-scan every 5 minutes.

## Setup

1. Get a free API key from [Twelve Data](https://twelvedata.com/) (forex
   time-series data).
2. Open the app (see [Deploy](#deploy) below) and go to the
   **⚙️ Pairs (Max 8)** tab → paste your API key → **Save Key**.
   The key is stored only in your browser's `localStorage` — it is never
   committed to this repo or sent anywhere except Twelve Data's API.
3. Pick up to 8 currency pairs (Twelve Data free tier request limits apply).
4. (Optional) Go to **🔔 Telegram** → add your bot token and chat ID to get
   push alerts on new `VALID` setups.
5. Hit **⟳ Smart Scan** or toggle **Live** for auto-scanning every 5 minutes.

## Deploy

This is a static HTML file — no build step needed.

### GitHub Pages
1. Push this repo to GitHub.
2. Repo **Settings → Pages → Source**: select the `main` branch, `/ (root)`
   folder.
3. Your app will be live at `https://<username>.github.io/<repo-name>/`.

### Local
Just open `index.html` in a browser, or serve it:
```bash
python3 -m http.server 8000
```

## How the confidence score works

Each signal is scored out of 7 possible confluence points:

| Layer | Points |
|---|---|
| Market Structure (BOS) | 1 |
| 4H HTF Trend Alignment | 1 |
| Premium/Discount Zone | 1 |
| FVG / Order Block (POI) | 1 |
| Liquidity Sweep | 1 |
| Candlestick Trigger Pattern | 1 |
| UT Bot Confluence | 1 |

A setup is only marked **VALID** at **5+/7** points (~71% confluence).
Counter-4H-trend setups are rejected regardless of score.

## Disclaimer

This tool is for educational purposes only and does not constitute
financial advice. Forex trading carries substantial risk of loss. No
scanner, indicator, or scoring system can guarantee any particular
win rate — always backtest, use proper position sizing, and never risk
money you can't afford to lose.

## License

MIT — see [LICENSE](LICENSE).
