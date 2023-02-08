# API Changes

## Coming Soon...  :hammer\_pick:

## 2023-02-07✔️

* new fields in the light ticker - settlementPrice, settlementPriceTimestamp, lastQuantity

## 2023-02-08  :hammer\_pick:

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
