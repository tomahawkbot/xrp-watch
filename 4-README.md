# XRP Watch

A small, dependency-free XRP-USD market dashboard. It fetches Coinbase Exchange public daily candles, charts closes and a seven-day average, and shows the latest daily close, close-to-close change, 30-day high/low, and daily volume. Choose 7, 30, 90 or 180 days; refresh manually or export the available candles to CSV.

## Run

Open `index.html` in a modern browser. If your browser blocks network requests from local files, serve this folder locally instead:

```sh
python3 -m http.server 8000
```

Then visit `http://localhost:8000/`. No dependencies, API keys, wallet connection or trading permission are needed. The dashboard uses a single fetch on load and another only when you press Refresh; it does not poll.

## Data and limits

- Source: [Coinbase Exchange REST API: product candles](https://docs.cdp.coinbase.com/api-reference/exchange-api/rest-api/products/get-product-candles), `XRP-USD`, daily granularity (`86400`). The response is OHLCV arrays `[timestamp, low, high, open, close, volume]`, sorted by the dashboard into chronological order.
- The newest UTC daily candle can be unfinished. The previous-candle percentage compares its current close with the previous returned candle, not a guaranteed final day-on-day return.
- The endpoint caps a request at 300 candles and may omit intervals without trades. This dashboard displays up to 180 of the available daily candles, but data gaps are not interpolated. Values are specific to Coinbase Exchange, not a market-wide average. If the service or browser connection fails, an error appears; it never silently substitutes sample data.
- CSV is generated in the browser from the latest fetched response. It does not contain account or holding information.

This project is for viewing market data, not financial advice or a buy/sell signal. It does not place orders or track a portfolio.
