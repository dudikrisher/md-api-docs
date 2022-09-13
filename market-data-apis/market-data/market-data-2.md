# Live Trades

## liveTrades

This API allows to get close to real time trades details happen on the market, you can retrieve limited amount last trades the were already happen and right after you will get real time event for new trades.\
Trade will come sorted by time, old trades will come first. \
When snapshot is completed, the last trade will be sent again, but quantity field will be set to 0.&#x20;

{% hint style="info" %}
`qualifier:` v1/exchange.marketdata/liveTrades
{% endhint %}

### **Request**

| Parameter | Type   | Description                                                                          |
| --------- | ------ | ------------------------------------------------------------------------------------ |
| symbol    | String | Symbol to retrieve the light tickers for                                             |
| limit     | eNum   | <p>Number of past trades (sorted by time descending). </p><p>0 ≤ limit ≤ 10,000 </p> |

### **Response**

<table><thead><tr><th data-type="number">Index</th><th>Parameter</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>1</td><td>price</td><td>Decimal</td><td>Trade price</td></tr><tr><td>2</td><td>quantity</td><td>Decimal</td><td>Trade quantity, for snapshot end message this will be set to 0.  </td></tr><tr><td>3</td><td>makerSide</td><td>Decimal</td><td>If resting order is Buy→ 1 else 0</td></tr><tr><td>4</td><td>timeStamp</td><td>Unix timestamp</td><td>Trade timestamp (milliseconds)</td></tr></tbody></table>

### **Error Codes**

| Code | Message                                         |
| ---- | ----------------------------------------------- |
| 1    | System is unavailable                           |
| 2    | Missing fields: \[Fieldname]                    |
| 3    | <p>Wrong limit |<br>Wrong symbol [symbol] |</p> |

### **Samples**

{% tabs %}
{% tab title="Subscription" %}
```json
{
  "q": "v1/exchange.marketdata/liveTrades",
  "sid": 153,
  "d": {
    "symbol": "AMZ",
    "limit": 100
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "q": "v1/exchange.marketdata/liveTrades",
  "sid": 153,
  "d": [
    3.2,           //price
    1.21,          //quantity
    1,             //makerSide
    1648969398501  //timestamp
  ]
}
```
{% endtab %}

{% tab title="End Of Snapshot" %}
```javascript
{
  "q": "v1/exchange.marketdata/liveTrades",
  "sid": 153,
  "d": [
    3.2,
    0, //This means snapshot is completed
    1,
    1648969398501
  ]
}
```
{% endtab %}

{% tab title="Empty Instrument" %}
```json
{
  "q": "v1/exchange.marketdata/liveTrades",
  "sid": 153,
  "d": [
    0,
    0, //This means snapshot is completed
    0,
    0
  ]
}
```
{% endtab %}
{% endtabs %}

