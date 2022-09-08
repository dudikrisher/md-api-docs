---
description: Allows to get market data from system
---

# Partial Order Book

## partialOrderBook

This API allows easy refresh of the book state without the need to calculate the entire book, it allows consumers to subscribe to some price levels in the book.

{% hint style="info" %}
`qualifier:` v1/exchange.marketdata/partialOrderBook
{% endhint %}

### **Request**

| Parameter | Type   | Description                                                      |
| --------- | ------ | ---------------------------------------------------------------- |
| symbol    | String | Symbol to retrieve the light tickers for                         |
| levels    | eNum   | Price level to be returned , values can be : 1,5,10,20,100       |
| interval  | eNum   | Response interval in milliseconds, allowed values: 100,1000,2000 |
| decimals  | Int    | Define the grouping decimal places (empty means no grouping)     |

### **Response**

| Parameter                 | Type           | Description                                      |
| ------------------------- | -------------- | ------------------------------------------------ |
| symbol                    | String         | Instrument symbol                                |
| timeStamp                 | Unix timestamp | Timestamp where message was sent                 |
| bids                      | \[]priceLevel  | Array of bids, sorted by price level descending  |
| asks                      | \[]priceLevel  | Array of asks, sorted by price level ascending   |
| priceLevel.price          | Decimal        | Price level according to the decimal in request  |
| priceLevel.quantity       | Decimal        | Aggregated quantity for that price level         |
| priceLevel.numberOfOrders | Int            | Aggregated number of orders for that price level |

### **Error Codes**

| Code | Message                                                                                |
| ---- | -------------------------------------------------------------------------------------- |
| 1    | System is unavailable                                                                  |
| 2    | Missing fields: \[Fieldname]                                                           |
| 3    | <p>Wrong levels |<br>Wrong interval |<br>Wrong symbol [symbol] |<br>Wrong decimals</p> |
| 100  | Your connection is slow, please reduce data consumed                                   |

****

### **Samples**

{% tabs %}
{% tab title="Subscription" %}
```javascript
{
  "q": "v1/exchange.marketdata/partialOrderBook",
  "sid": 10,
  "d": {
    "symbol": "INS1",
    "levels": 5,
    "interval": 1000,
    "decimals": 2
  }
}
```
{% endtab %}

{% tab title="Response" %}
```javascript
{
  "q": "v1/exchange.marketdata/partialOrderBook",
  "sid": 10,
  "d": {
    "symbol": "AMZ",
    "timeStamp": 1646549579452,
    "bids": [
      [
        100.5,  //Price level
        10.25,  //Total quantity 
        1       //number of orders 
      ],
      [
        100.33,
        6.5,
        5
      ],
      [
        100,
        93.0049,
        1
      ],
      [
        97,
        99.0038,
        2
      ],
      [
        96,
        123.0193,
        3
      ]
    ],
    "asks": [
      [
        100.6,
        1.3,
        1
      ],
      [
        101,
        1.3,
        1
      ]
    ]
  }
}
```
{% endtab %}

{% tab title="Empty Response" %}
```javascript
{
  "q": "v1/exchange.marketdata/partialOrderBook",
  "sid": 13,
  "d": {
    "symbol": "INS3",
    "timeStamp": 1646667453613,
    "bids": [],
    "asks": []
  }
}
```
{% endtab %}
{% endtabs %}

