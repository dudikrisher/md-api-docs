# Get Settlement Prices

## getSettlementPrices

This API allows  retrieve the settlement prices for all instruments or for a specific list of instruments. \
Stream is bounded stream, after sending the relvant responses, stream will be closed.&#x20;

{% hint style="info" %}
`qualifier:` v1/exchange.marketdata/getSettlementPrices
{% endhint %}

### **Request**

| Parameter | Type      | Description                                                                                                                                                                                     |
| --------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| symbols   | \[]String | <p>List of symbols to retrieve the settlement prices for.<br>Keep empty to get settlement prices for all instruments<br><br>Disabled instruments with settlement price are also returned.  </p> |

### **Response**

| Parameter  | Type           | Description                                                  |
| ---------- | -------------- | ------------------------------------------------------------ |
| symbol     | String         | Instrument symbol                                            |
| price      | Decimal        | Settlement price                                             |
| lastUpdate | Unix timestamp | <p>Settlement price update timestamp<br>In milliseconds </p> |

### **Error Codes**

| Code | Message                      |
| ---- | ---------------------------- |
| 1    | System is unavailable        |
| 2    | Missing fields: \[Fieldname] |

### **Samples**

{% tabs %}
{% tab title="Request" %}
```json
{
  "q": "v1/exchange.marketdata/getSettlementPrices",
  "token": "eyJleGNoYW5nZUlkIjozMCwicHJvamVjdElkIjoyMDB9",
  "sid": 10,
  "d": {
    "symbols": [
      "INS1",
      "INS2"
    ]
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "q": "v1/exchange.marketdata/getSettlementPrices",
  "sid": 10,
  "d": {
    "symbol": "INS1",
    "price": 1.235,
    "lastUpdate": 1662638980158
  }
}
```
{% endtab %}

{% tab title="Stream Closure" %}
```json
{
  "sig": 1,
  "q": "v1/exchange.marketdata/getSettlementPrices",
  "sid": 10
}
```
{% endtab %}
{% endtabs %}
