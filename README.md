# Stock Research Terminal

A self-contained, single-file stock research terminal — no backend, no build step, no framework. Open `index.html` in a browser and it works.

## What it does

- Look up any ticker and see its last close, day change, and a technical BUY/SELL/HOLD signal
- Pulls real daily price history from [Stooq](https://stooq.com)'s free public CSV endpoints (no API key required)
- Computes RSI(14), SMA(20), and SMA(50) client-side and combines them into a simple technical signal
- Maintains a watchlist persisted in the browser's `localStorage` — refresh the page and it's still there
- Renders a lightweight inline SVG price chart with no charting library

## Running it

Just open `index.html` in any modern browser. To serve it locally instead:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

To publish it, push this repo and enable GitHub Pages on the `main` branch — it will work as-is since there's nothing to build.

## Why Stooq

Stooq publishes free, keyless, CORS-friendly quote and historical data endpoints, which makes it the simplest option for a purely client-side tool like this one. Swap the `STOOQ_QUOTE` / `STOOQ_HISTORY` URL builders near the top of the `<script>` block for another provider (e.g. Alpha Vantage, Finnhub) if you want a different data source or intraday data.

## Notes

- Data is end-of-day, not real-time — this is a research tool, not a trading terminal.
- The technical signal is intentionally simple (SMA crossover + RSI extremes) and meant to be a readable, extensible starting point rather than a production trading strategy.
