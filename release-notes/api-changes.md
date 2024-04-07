# API Changes

## v1.27.0 (2024-04-01)️✔️

* New API for OHLCV data `v1/exchange.marketdata/aggregates`
* New API Heartbeats (Pings) `v1/heartbeat/ping` for browser API clients
* `tradingModels` field will always be returned by `exchange.marketdata/instrumentList`

## v1.26.0 (2024-02-28)️✔️

* Bugfix related to the Market Data Service. `referencePrice` was not returned after restarting the service before the fix.

## v1.25.0 (2024-02-07)️✔️

* Bugfix related to the end of the snapshot message of `v1/exchange.marketdata/liveTrades`. `multiLegReportingType` field was not returned prior to the fix.
* Bugfix related to the required fields of `v1/exchange.marketdata/lightTickers`. The error message returned was incorrect before the fix.

## v1.24.0 (2024-01-17)✔️

* Changed `quoteVolume` formula of `LightTicker` to `Total(trade amount * absolute value of trade price * contract size)`. The previous formula didn’t have the `contract size`.
* Added `deliveryStartDate` and `deliveryEndDate` to the `v1/exchange.marketdata/instrumentList`
* Added `makerSide` to the RFQ Trades of `v1/exchange.marketdata/liveTrades`
* Bugfix related to `quantity` of `liveTrades` messages of legs instruments of strategies. `quantity` of trades has incorrectly had the `quantity` of current trade + `quantity` of previous trade when trade prices of current and previous trades were the same.

## v1.23.0 (2023-12-26)️✔️

* Added `scope` to the `lightTickers` API.
* Added `multiLegReportingType` to the `liveTrades` API.

## v1.22.0 (2023-12-05)️✔️

* Added RFQ trades to the liveTrades and lightTickers APIs
* Bugfix related to ​​`openingPrice` calculation of `lightTickers`. The system has incorrectly taken trade entries for the calculation before the fix.
* Bugfix related to the `volumeTypes` object of `lightTickers` API. `volume` field was incorrectly returned as `value` before the fix.

## v1.20.0 (2023-10-25)✔️

* New API to disseminate Instrument details `v1/exchange.marketdata/instrumentList`
* New API to disseminate Calendar details `v1/exchange.marketdata/calendarList`
* New API to disseminate tickSize details `v1/exchange.marketdata/tickSizeList`
* Changed `token` to be a required field in all Market Data APIs
* Deprecated `environments.exchangeNum` field in all Market Data APIs
* Bug fix on  [#livetrades](../market-data-apis/market-data/market-data-2.md#livetrades "mention") API on strategy allocated leg trades to properly display `makerSide`

## 2023-07-12✔️

* Fixed the bug related to timeStamp format in `v1/exchange.marketdata/liveTrades`

## 2023-06-21✔️

* volumeTypes object in the light ticker will be sent only if there is data that is not 0&#x20;

## 2023-06-06✔️

* Adding new fields to the light ticker
* Taking the trade entry data considered in some fields in the light ticker (volume, quoteVolume, high, low, lastPrice, lastQuantity)
* Adding the trade entry and trade cancellation to the live trades.
  * new value in quantity in case of cancellation
  * makerSide will be in this case: -1

## 2023-05-02✔️

* Adding the reference price and timestamp of the instrument to the light ticker response

## 2023-03-22✔️

* Adding the trading status of the instrument to the light ticker response

## 2023-02-08  ✔️

There are new fields in the light ticker API:

* settlementPrice: Settlement price
* settlementPriceTimestamp: Settlement price last update timestamp
* lastQuantity: Last executed trade quantity



Until now in case one of the symbols is wrong, the entire stream was disconnected.

From now on, in case of wrong symbol stream will continue working for the valid symbols and for the invalid symbols the message returned will be:

```json
{
  "q": "v1/exchange.marketdata/lightTickers",
  "sid": 10,
  "d": {
    "symbol": "Ins1",
    "bidQuantity": 0,
    "askQuantity": 0,
    "timeStamp":1675769165802,
    "errorCode": 3,
    "errorMessage": "Wrong symbol" 
  }
}
```

This error might occur in case that stream is already working (in case symbol is no longer active instrument).

## 2023-01-18  ✔️

[market-data.md](../market-data-apis/market-data/market-data.md "mention") will publish events only in case there is change in data. Once there is change- it will be sent only when interval time elapsed.

## 2023-01-03  ✔️

All API has a new optional header parameter - we strongly recommend to use it instead of the previous `environments.exchangeNum`  (which is still supported), the new parameter provides more accurate and efficient instrument discovery.&#x20;

The parameter is called `token` and can be retrieved from Admin application under home page:

<img src="../.gitbook/assets/image (3) (2).png" alt="" data-size="original">  &#x20;



Sample API using new parameter:

```json
{
  "q": "v1/exchange.marketdata/lightTickers",
  "token": "eyJleGNoYW5nZUlkIjozMCwicHJvamVjdElkIjoyMDB9",
  "sid": 10,
  "d": {
    "symbols": [
      "ABC",
      "XYZ",
      "INS1"
    ],
    "interval": 1000
  }
}
```

## 2022-**11**-21✔️

`getSettlementPrices` API  will response with the latest results updated in system. &#x20;

## 2022-09-13✔️

`lightTickers` API will have new properties, that are referring to the current trading day :

* lastClosingPrice - last execution prive before market close&#x20;
* closingPriceTimestamp - closing price timestamp
* openingPrice - first execution price after market open&#x20;
* low - lowest execution price since market open&#x20;
* high -  highest execution price since market open
* volume - total volume since market open (total orders amount)&#x20;
* quoteVolume -  total volume since market open in quote currency terms (amount \* price)&#x20;



## 2022-09-13✔️

New API added [market-data-3.md](../market-data-apis/market-data/market-data-3.md "mention")

##
