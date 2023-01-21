# Binance Futures Leaderboard API
[Binance Futures Leaderboard API](https://rapidapi.com/DevNullZero/api/binance-futures-leaderboard1) is an API hosted in [RapidAPI](https://rapidapi.com/DevNullZero/api/binance-futures-leaderboard1) for querying the leaderboard of the Binance Futures Exchange.

The API is written in Python with FastAPI and and AIOHTTP for asynchronous requests. Uvicorn is used as an ASGI server.


## Features
- Advanced search with filters - You can search for a specific symbol, such as **BTCUSDT, EHTUSDT**; period time, **weekly, monthly**; sort by **PNL, ROI or followers**; specific trade type, **USDⓈ-M and COIN-M** 

- Get open positions from different traders - You can get open positions from different traders, such as **trader1, trader2, trader3**. Get all position details, such as **symbol, open time, PNL, ROI, amount, etc**.

- Search traders by name - You can search for a specific trader by name, such as **Elon Musk, Vitalik Buterin**.

- Get trader information - You can get trader information, such as **Twitter URL, followers, open positions, etc.** 


## Use cases
- Automate trading with leaderboard data - You can copy the open positions from the leaderboard.
- Signal bot - You can get the open positions from the leaderboard and send the signal to the bot.
- Trend analysis - You can get the open positions from the leaderboard and analyze the trend.

## Usage
This examples are written in JavaScript, but you can use any language you want.
### Get all positions from a trader

<details>
<summary>Code</summary>

```javascript
const unirest = require("unirest");


// Get all positions from a trader
const req = unirest(
    "GET",
    "https://binance-futures-leaderboard1.p.rapidapi.com/v1/getOtherPosition"
);

// Set query parameters
req.query({
  "encryptedUid": "FAD84AAFD6E43900BF15E06B21857715",
  "tradeType": "PERPETUAL"  // USDⓈ-M position
});

// Set headers
req.headers({
  "X-RapidAPI-Key": "391ef9f160msh695944ba3b12e0fp552a76",
  "X-RapidAPI-Host": "binance-futures-leaderboard1.p.rapidapi.com",
  "useQueryString": true
});

req.end(function (res) {
  if (res.error) throw new Error(res.error);

  console.log(res.body);
});
```
</details>

<details>
<summary>Output</summary>

```json
{
  "message": null,
  "data": {
    "otherPositionRetList": [
      {
        "symbol": "1000SHIBBUSD",
        "entryPrice": 0.0109575274547,
        "markPrice": 0.00869468,
        "pnl": -413.05202508,
        "roe": -5.20511393,
        "updateTime": [
          2022,
          12,
          16,
          22,
          27,
          31,
          167000000
        ],
        "amount": 182537,
        "updateTimeStamp": 1671229651167,
        "yellow": false,
        "tradeBefore": true,
        "leverage": 20
      },
      {
        "symbol": "DOGEBUSD",
        "entryPrice": 0.1138665496141,
        "markPrice": 0.07586939,
        "pnl": -689.268301,
        "roe": -10.01646382,
        "updateTime": [
          2022,
          12,
          16,
          22,
          27,
          22,
          15000000
        ],
        "amount": 18140,
        "updateTimeStamp": 1671229642015,
        "yellow": false,
        "tradeBefore": true,
        "leverage": 20
      },
      {
        "symbol": "CHZUSDT",
        "entryPrice": 0.1406267485939,
        "markPrice": 0.11980222,
        "pnl": -370.2599656,
        "roe": -3.47648316,
        "updateTime": [
          2022,
          12,
          22,
          15,
          16,
          38,
          388000000
        ],
        "amount": 17780,
        "updateTimeStamp": 1671722198388,
        "yellow": false,
        "tradeBefore": true,
        "leverage": 20
      }
    ],
    "updateTime": [
      2022,
      12,
      16,
      22,
      27,
      22,
      15000000
    ],
    "updateTimeStamp": 1671229642015
  },
  "success": true
}
```
</details>

### Get multiple positions from different traders in one call

<details>
<summary>Code</summary>

```javascript
const unirest = require("unirest");

// Get multiple positions from different traders in one call
const req = unirest(
    "GET",
    "https://binance-futures-leaderboard1.p.rapidapi.com/v2/getTraderPositions"
);

// Set query parameters. You can add up to 50 traders UUIDs.
req.query({
  "encryptedUid": [
        "A81B9CB3E58B471B269CB88A30EF0190",
        "FB23E1A8B7E2944FAAEC6219BBDF8243",
        "D64DDD2177FA081E3F361F70C703A562",
        "F45BBD3F4C148BFCE413B0A343A1BF97"
    ],
    "tradeType": "PERPETUAL"  // USDⓈ-M position
});

// Set headers
req.headers({
  "X-RapidAPI-Key": "391ef9f160msh695944ba3b12e0fp552a76",
  "X-RapidAPI-Host": "binance-futures-leaderboard1.p.rapidapi.com",
  "useQueryString": true
});

req.end(function (res) {
  if (res.error) throw new Error(res.error);

  console.log(res.body);
});
```
</details>

<details>
<summary>Output</summary>

```json
{
  "message": null,
  "data": [
    {
      "encryptedUid": "FAD84AAFD6E43900BF15E06B21857715",
      "positions": {
        "perpetual": [
          {
            "symbol": "1000SHIBBUSD",
            "entryPrice": 0.0109575274547,
            "markPrice": 0.0086906,
            "pnl": -413.79677604,
            "roe": -5.21694705,
            "amount": 182537,
            "updateTimeStamp": 1671229651167,
            "tradeBefore": true,
            "long": true,
            "short": false,
            "leverage": 20
          },
          {
            "symbol": "DOGEBUSD",
            "entryPrice": 0.1138665496141,
            "markPrice": 0.07572,
            "pnl": -691.9782356,
            "roe": -10.0756841,
            "amount": 18140,
            "updateTimeStamp": 1671229642015,
            "tradeBefore": true,
            "long": true,
            "short": false,
            "leverage": 20
          },
          {
            "symbol": "CHZUSDT",
            "entryPrice": 0.1406267485939,
            "markPrice": 0.12009586,
            "pnl": -365.0390464,
            "roe": -3.41908206,
            "amount": 17780,
            "updateTimeStamp": 1671722198388,
            "tradeBefore": true,
            "long": true,
            "short": false,
            "leverage": 20
          }
        ],
        "delivery": null
      }
    },
    {
      "encryptedUid": "B2E4D88D1E5633B2584F87EB5E2A6D6A",
      "positions": {
        "perpetual": [
          {
            "symbol": "ETHUSDT",
            "entryPrice": 1318.067245509,
            "markPrice": 1324.52538664,
            "pnl": -5.39254785,
            "roe": -0.03900652,
            "amount": -0.835,
            "updateTimeStamp": 1673311052233,
            "tradeBefore": false,
            "long": false,
            "short": true,
            "leverage": 8
          },
          {
            "symbol": "BTCUSDT",
            "entryPrice": 17239.00810811,
            "markPrice": 17207,
            "pnl": 2.3686,
            "roe": 0.01488144,
            "amount": -0.074,
            "updateTimeStamp": 1673311072663,
            "tradeBefore": false,
            "long": false,
            "short": true,
            "leverage": 8
          }
        ],
        "delivery": null
      }
    },
    {
      "encryptedUid": "2154D02AD930F6C6E65C507DD73CB3E7",
      "positions": {
        "perpetual": [
          {
            "symbol": "FILUSDT",
            "entryPrice": 3.075621118755,
            "markPrice": 3.719,
            "pnl": -9018.11322535,
            "roe": -1.72997819,
            "amount": -14016.8,
            "updateTimeStamp": 1672853709039,
            "tradeBefore": false,
            "long": false,
            "short": true,
            "leverage": 10
          }
        ],
        "delivery": null
      }
    }
  ],
  "success": true
}
```
</details>

### Get Binance Futures Leaderboard rankings

<details>
<summary>Code</summary>

```javascript
const unirest = require("unirest");


// Get Binance Futures Leaderboard rankings
const req = unirest(
    "GET",
    "https://binance-futures-leaderboard1.p.rapidapi.com/v2/searchLeaderboard"
);

// Set query parameters
req.query({
	"isShared": "false",
	"limit": "5"
});

// Set headers
req.headers({
	"X-RapidAPI-Key": "391ef9f160msh695944ba3b12e0fp552a76",
	"X-RapidAPI-Host": "binance-futures-leaderboard1.p.rapidapi.com",
	"useQueryString": true
});

req.end(function (res) {
	if (res.error) throw new Error(res.error);

	console.log(res.body);
});
```
</details>

<details>
<summary>Output</summary>

```json
{
  "message": null,
  "data": [
    {
      "encryptedUid": "04739B7591F44D5CD43386085B59780C",
      "nickName": "Anonymous User-588a617",
      "positionShared": false,
      "deliveryPositionShared": false,
      "followerCount": 46,
      "pnlValue": 300000,
      "roiValue": 3000,
      "rank": 1,
      "leaderboardUrl": "https://www.binance.com/en/futures-activity/leaderboard?type=myProfile&encryptedUid=04739B7591F44D5CD43386085B59780C",
      "positions": {
        "perpetual": null,
        "delivery": null
      }
    },
    {
      "encryptedUid": "32C0A0B511B20B4E3F2930E1FCD54A72",
      "nickName": "Anonymous User-1a13711",
      "positionShared": false,
      "deliveryPositionShared": false,
      "followerCount": 7,
      "pnlValue": 38122.64217118,
      "roiValue": 381.226422,
      "rank": 2,
      "leaderboardUrl": "https://www.binance.com/en/futures-activity/leaderboard?type=myProfile&encryptedUid=32C0A0B511B20B4E3F2930E1FCD54A72",
      "positions": {
        "perpetual": null,
        "delivery": null
      }
    },
    {
      "encryptedUid": "1D808AEA1ACBC5BF616464276C4B8990",
      "nickName": "Anonymous User-582be9",
      "positionShared": false,
      "deliveryPositionShared": false,
      "followerCount": 7,
      "pnlValue": 5021.970393,
      "roiValue": 50.219704,
      "rank": 3,
      "leaderboardUrl": "https://www.binance.com/en/futures-activity/leaderboard?type=myProfile&encryptedUid=1D808AEA1ACBC5BF616464276C4B8990",
      "positions": {
        "perpetual": null,
        "delivery": null
      }
    },
    {
      "encryptedUid": "A365F4855F3EC1E260C00DE6DC90174D",
      "nickName": "太子妃",
      "positionShared": false,
      "deliveryPositionShared": false,
      "followerCount": 20,
      "pnlValue": 7090.650612,
      "roiValue": 37.348359,
      "rank": 4,
      "leaderboardUrl": "https://www.binance.com/en/futures-activity/leaderboard?type=myProfile&encryptedUid=A365F4855F3EC1E260C00DE6DC90174D",
      "positions": {
        "perpetual": null,
        "delivery": null
      }
    },
    {
      "encryptedUid": "46ACA48D96565DCDE1A901868894F746",
      "nickName": "BoWay",
      "positionShared": false,
      "deliveryPositionShared": false,
      "followerCount": 3,
      "pnlValue": 4821.20351,
      "roiValue": 33.172897,
      "rank": 5,
      "leaderboardUrl": "https://www.binance.com/en/futures-activity/leaderboard?type=myProfile&encryptedUid=46ACA48D96565DCDE1A901868894F746",
      "positions": {
        "perpetual": null,
        "delivery": null
      }
    }
  ],
  "success": true
}
```
</details>


## Using the API
You can use the API via the following methods:
- [RapidAPI](https://rapidapi.com/DevNullZero/api/binance-futures-leaderboard1)
- [Direct API URL (500 request per week for each endpoint)](http://85.239.231.127:2318)
- [Purchasing it](https://t.me/devnullzer0)

## Contact
You can contact me via Telegram: [@DevNullZer0](https://t.me/devnullzer0) or [email](mailto:devnullzer0@pm.me)

