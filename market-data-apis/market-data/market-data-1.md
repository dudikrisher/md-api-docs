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

| Parameter                    | Type           | Description                                                                                             |
| ---------------------------- | -------------- | ------------------------------------------------------------------------------------------------------- |
| symbol                       | String         | Instrument symbol                                                                                       |
| lastPrice                    | Decimal        | last execution price                                                                                    |
| bidPrice                     | Decimal        | Highest bid price                                                                                       |
| bidQuantity                  | Decimal        | Sum of quantity of all orders with `bidPrice`                                                           |
| askPrice                     | Decimal        | Lowest ask price                                                                                        |
| askQuantity                  | Decimal        | Sum of quantity of all orders with the `askPrice`                                                       |
| timeStamp                    | Unix timestamp | Latest timestamp where one of the above values was changed                                              |
| openingPrice                 | Decimal        | First order book trade on the day, will be empty until first execution is happening                     |
| low                          | Decimal        | Lowest order book executed price of the day                                                             |
| high `new`                   | Decimal        | Highest order book executed price of the day                                                            |
| volume`new`                  | Decimal        | Total trade volume (in base asset)                                                                      |
| quoteVolume `new`            | Decimal        | <p>Total trade volume in quote asset<br><span class="math"> \xi (Trade Amount * Trade Price)</span></p> |
| lastClosingPrice `new`       | Decimal        | Last day closing price (=last order book trade on the day)                                              |
| closingPriceTimestamp  `new` | Unix timestamp | The time with where closing price was determined                                                        |

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
    "lastPrice": 1.3,
    "bidPrice": 1.3,
    "bidQuantity": 1.67,
    "askPrice": 1.35,
    "askQuantity": 2,
    "timeStamp": 1667317150356,
    "low": 1,
    "high": 1.4,
    "volume": 20.54,
    "quoteVolume": 24.419
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
