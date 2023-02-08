# Light Tickers

## lightTickers

This API allows easy refresh of the instruments market data.\
Upon subscription data for all instruments will sent, afterward, data for specific instrument will be returned only in case one of the values was changed (it will not not be sent on real time but only when interval time reached)

{% hint style="info" %}
`qualifier:` v1/exchange.marketdata/lightTickers
{% endhint %}

### **Request**

| Parameter | Type      | Description                                                      |
| --------- | --------- | ---------------------------------------------------------------- |
| symbols   | \[]String | List of symbols to retrieve the light tickers for                |
| interval  | eNum      | Response interval in milliseconds, allowed values: 100,1000,2000 |

### **Response**

| Parameter                      | Type           | Description                                                                                             |
| ------------------------------ | -------------- | ------------------------------------------------------------------------------------------------------- |
| symbol                         | String         | Instrument symbol                                                                                       |
| lastPrice                      | Decimal        | last execution price                                                                                    |
| lastQuantity `new`             | Decimal        | Last executed trade quantity                                                                            |
| bidPrice                       | Decimal        | Highest bid price                                                                                       |
| bidQuantity                    | Decimal        | Sum of quantity of all orders with `bidPrice`                                                           |
| askPrice                       | Decimal        | Lowest ask price                                                                                        |
| askQuantity                    | Decimal        | Sum of quantity of all orders with the `askPrice`                                                       |
| timeStamp                      | Unix timestamp | Latest timestamp where one of the above values was changed                                              |
| openingPrice                   | Decimal        | First order book trade on the day, will be empty until first execution is happening                     |
| low                            | Decimal        | Lowest order book executed price of the day                                                             |
| high                           | Decimal        | Highest order book executed price of the day                                                            |
| volume                         | Decimal        | Total trade volume (in base asset)                                                                      |
| quoteVolume                    | Decimal        | <p>Total trade volume in quote asset<br><span class="math"> \xi (Trade Amount * Trade Price)</span></p> |
| closingPrice                   | Decimal        | Last day closing price (=last order book trade on the day)                                              |
| closingPriceTimestamp          | Unix timestamp | The time where closing price was determined                                                             |
| settlementPrice`new`           | Decimal        | Settlement price                                                                                        |
| settlementPriceTimestamp `new` | Unix timestamp | Settlement price last update timestamp                                                                  |

### **Samples**

{% tabs %}
{% tab title="Subscription" %}
```javascript
{
  "q": "v1/exchange.marketdata/lightTickers",
  "token": "eyJleGNoYW5nZUlkIjozMCwicHJvamVjdElkIjoyMDB9",
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
    "symbol": "INS10",
    "lastPrice": 0.3333,
    "lastQuantity": 0.23,
    "bidPrice": 0.3333,
    "bidQuantity": 1.1,
    "askPrice": 0.4455,
    "askQuantity": 3.77,
    "timeStamp": 1675869327183,
    "openingPrice": 1.3333,
    "low": 0.3333,
    "high": 1.3333,
    "volume": 12.09,
    "quoteVolume": 10.083385,
    "closingPrice": 1,
    "closingPriceTimestamp": 1675807200002,
    "settlementPrice": 1.12,
    "settlementPriceTimestamp": 1673793853931
  }
}
```
{% endtab %}

{% tab title="Empty Response" %}
```javascript
{
  "q": "v1/exchange.marketdata/lightTickers",
  "sid": 12,
  "d": {
    "symbol": "INS10",
    "bidQuantity": 0,
    "askQuantity": 0,
    "timeStamp": 1674115200000,
    "volume": 0,
    "quoteVolume": 0
  }
}
```
{% endtab %}
{% endtabs %}

### **Error Codes**

| Code | Message                                 |
| ---- | --------------------------------------- |
| 1    | System is unavailable                   |
| 2    | Missing fields: \[Fieldname]            |
| 3    | <p>Wrong interval |<br>Wrong symbol</p> |

Note: unlike other errors, in case of `Wrong symbol` , stream will continue working for the valid symbols.&#x20;

This error might returned on the subscription but also in case that stream is already working but instrument was updated so that symbol is no longer active instrument.

### **Error Samples**

{% tabs %}
{% tab title="Error" %}
```json
{
  "sig": 2,
  "q": "v1/exchange.marketdata/lightTickers",
  "errorType": "500",
  "sid": 10,
  "d": {
    "errorCode": 3,
    "errorMessage": "Wrong interval"
  }
}
```
{% endtab %}

{% tab title="Wrong Symbol" %}
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
{% endtab %}
{% endtabs %}
