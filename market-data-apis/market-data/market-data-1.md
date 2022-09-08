---
description: Allows to get market data from system
---

# Light Tickers

## lightTickers

This API allows easy refresh of the instruments market data.

{% hint style="info" %}
`qualifier:` v1/exchange.marketdata/lightTickers
{% endhint %}

### **Request**

| Parameter | Type      | Description                                                      |
| --------- | --------- | ---------------------------------------------------------------- |
| symbols   | \[]String | List of symbols to retrieve the light tickers for                |
| interval  | eNum      | Response interval in milliseconds, allowed values: 100,1000,2000 |

### **Response**

| Parameter   | Type           | Description                                                 |
| ----------- | -------------- | ----------------------------------------------------------- |
| symbol      | String         | Instrument symbol                                           |
| lastPrice   | Decimal        | last execution price                                        |
| bidPrice    | Decimal        | Highest bid price                                           |
| bidQuantity | Decimal        | Sum of quantity of all orders with `bidPrice`               |
| askPrice    | Decimal        | Lowest ask price                                            |
| askQuantity | Decimal        | Sum of quantity of all orders with the `askPrice`           |
| timeStamp   | Unix timestamp | Latest timestamp where one of the above values was changed  |

### **Error Codes**

| Code | Message                                          |
| ---- | ------------------------------------------------ |
| 1    | System is unavailable                            |
| 2    | Missing fields: \[Fieldname]                     |
| 3    | <p>Wrong interval |<br>Wrong symbol [symbol]</p> |

### **Samples**

{% tabs %}
{% tab title="Subscription" %}
```javascript
{
  "q": "v1/exchange.marketdata/lightTickers",
  "sid": 10,
  "d": {
    "symbols": ["AMZN","INS1"],
    "interval": 2000
  }
}
```
{% endtab %}

{% tab title="Response" %}
```javascript
{
  "q": "v1/exchange.marketdata/lightTickers",
  "sid": 10,
  "d": {
    "symbol": "AMZ",
    "lastPrice": 100.5,
    "bidPrice": 100.5,
    "bidQuantity": 10.25,
    "askPrice": 100.6,
    "askQuantity": 1.3,
    "timeStamp": 1646549579452
  }
}
```
{% endtab %}

{% tab title="Empty Response" %}
```javascript
{
  "q": "v1/exchange.marketdata/lightTickers",
  "sid": 10,
  "d": {
    "symbol": "INS10",
    "bidQuantity": 0,
    "askQuantity": 0,
    "timeStamp": 1646661691612
  }
}
```
{% endtab %}
{% endtabs %}
