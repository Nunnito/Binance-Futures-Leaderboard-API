# Binance Smart Money API

A commercial REST API for Binance Smart Money (formerly the Binance Futures Leaderboard): discover top traders, read their open positions, and pull performance history.

Written in Python with FastAPI and AIOHTTP for asynchronous requests. Uvicorn is used as an ASGI server.

**Full documentation and interactive reference: [Kopyon API docs](https://kopyon.com/binance-smart-money-api/docs/)**

## Features

- **Trader discovery** — rank traders by PNL or ROI over 24h, 3D, 7D, 30D, 90D, 1Y or all time, with optional filtering by account group (AI, featured human, featured AI).
- **Search by name** — the same ranking and filter options applied to a keyword search.
- **Trader profiles** — performance metrics and account detail for a single trader.
- **Open positions** — current positions per trader across USDⓈ-M (`UM`) and COIN-M (`CM`) markets.
- **Position and order history** — historical positions and orders, filterable by symbol and time range, with cursor pagination.
- **Chart data** — ROI, PNL or balance series over any supported time range.
- **Versioned endpoints** — versions are served in parallel under their own prefix, so a change on my side does not break existing consumers.

## Use cases

- Copy-trading systems that mirror positions from top traders.
- Signal bots that forward position changes into Telegram.
- Trend analysis across trader cohorts.

## Authentication

You can try the API without a key under a small per-IP allowance. For Free and paid plan quotas, send your API key in the `X-API-KEY` header.

```
X-API-KEY: your-api-key
```

Responses use `200` on success, `401` for an invalid key, `429` when rate limited, and `500` on a server error.

## Endpoints

Base URL: `https://api.kopyon.com/v4`

| Endpoint | Returns |
|---|---|
| `GET /tradersList` | Ranked list of traders |
| `GET /traderSearch` | Traders matching a keyword |
| `GET /traderProfile` | Profile and metrics for one trader |
| `GET /traderChartData` | ROI, PNL or balance series |
| `GET /traderOpenPositions` | Current open positions |
| `GET /traderPositionHistory` | Historical positions |
| `GET /traderOrderHistory` | Historical orders |

Shared parameter values:

- `timeRange` — `24h`, `3D`, `7D`, `30D`, `90D`, `1Y`, `ALL`
- `rankingType` — `PNL`, `ROI`
- `order` — `DESC`, `ASC`
- `marketType` — `UM` (USDⓈ-M), `CM` (COIN-M)
- `accountGroup` — `AI`, `FEATURED_TRADERS_AI`, `FEATURED_TRADERS_HUMAN`
- `chartDataType` — `ROI`, `PNL`, `BALANCE`

## Usage

These examples use `curl`, but any HTTP client works.

### Top traders by 7-day ROI

```bash
curl -H "X-API-KEY: $API_KEY" \
  "https://api.kopyon.com/v4/tradersList?timeRange=7D&rankingType=ROI&order=DESC&onlyShowSharingPosition=true&page=1&rows=20"
```

### Search for a trader by name

```bash
curl -H "X-API-KEY: $API_KEY" \
  "https://api.kopyon.com/v4/traderSearch?searchKeyword=whale&timeRange=30D&rankingType=PNL&order=DESC&onlyShowSharingPosition=true&page=1&rows=20"
```

### A trader's open USDⓈ-M positions

```bash
curl -H "X-API-KEY: $API_KEY" \
  "https://api.kopyon.com/v4/traderOpenPositions?topTraderId=TRADER_ID&marketType=UM&page=1&rows=20"
```

### Position history for one symbol

```bash
curl -H "X-API-KEY: $API_KEY" \
  "https://api.kopyon.com/v4/traderPositionHistory?topTraderId=TRADER_ID&marketType=UM&symbol=BTCUSDT&rows=20"
```

Response schemas for every endpoint are documented in the [Kopyon API reference](https://kopyon.com/binance-smart-money-api/docs/).

## Access

Try every endpoint, compare plans, and request an API key on the [Kopyon API page](https://kopyon.com/binance-smart-money-api/). The Free plan includes 10,000 requests per month and does not require a card.

The [legacy RapidAPI listing](https://rapidapi.com/DevNullZero/api/binance-futures-leaderboard1) remains available for marketplace users. The direct Kopyon v4 API above is the current API and documentation.

## Contact

Telegram [@nunnito](https://t.me/nunnito) · [support@kopyon.com](mailto:support@kopyon.com)
