# Stock Research Terminal

A self-contained, single-file stock research terminal — no backend, no build step, no framework. Open `index.html` in a browser, paste in a free [Twelve Data](https://twelvedata.com/pricing) API key, and it works.

## What it does

- Look up any ticker and see its last close, day change, and a technical BUY/SELL/HOLD signal
- Pulls real daily price history from Twelve Data's `time_series` endpoint, straight from the browser
- Computes RSI(14), SMA(20), and SMA(50) client-side and combines them into a simple technical signal
- Maintains a watchlist persisted in the browser's `localStorage` — refresh the page and it's still there
- Renders a lightweight inline SVG price chart with no charting library

## Running it

1. Get a free API key at https://twelvedata.com/pricing (800 requests/day, 8/minute).
2. Open `index.html` in any modern browser — double-clicking the file works.
3. Paste the key into the **API key** box and click **Save key**.

The key is stored only in your browser's `localStorage`; it is never written to the code or the repo. To serve the page instead of opening the file:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

It also works as-is on GitHub Pages, since there's nothing to build.

## Why Twelve Data

Twelve Data allows browser requests (CORS) and includes daily history on its free tier, which a purely client-side page needs. Stooq, the original source, now serves a bot-check page instead of data; Yahoo Finance blocks browser requests; Finnhub's free tier no longer includes historical candles. To use another provider, change `SERIES_URL` near the top of the `<script>` block and adapt `fetchQuote` / `fetchHistory` to its response format.

- Each ticker lookup or watchlist row uses one request, so a watchlist of more than 8 tickers can hit the per-minute limit on the free plan.

## Notes

- Data is end-of-day, not real-time — this is a research tool, not a trading terminal.
- The technical signal is intentionally simple (SMA crossover + RSI extremes) and meant to be a readable, extensible starting point rather than a production trading strategy.
