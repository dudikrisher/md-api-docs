# API Changes

## Coming Soon...  :hammer\_pick:

TBD

## 2023-01-18  :hammer\_pick:

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
