# (NEW v1.20) Instrument List

This API provides snapshot and real-time updates for instruments details.&#x20;

Upon successful subscription, a snapshot of all active instruments is sent. The last message of the snapshot contains `lastMessage=Y`. Any changes to the instruments after the snapshot are sent as subsequent updates.

{% hint style="info" %}
`qualifier:` v1/exchange.marketdata/instrumentList
{% endhint %}

### **Request**

No request parameters



### **Response**

Similar to [this](https://documenter.getpostman.com/view/6229811/TzCV3jcq#f11697b8-fc27-4c58-90d1-b15e73f47de3).

###

### **Error Codes**

<table><thead><tr><th width="150">Code</th><th width="554.4285714285713">Message</th></tr></thead><tbody><tr><td>1</td><td>System is unavailable</td></tr></tbody></table>



### **Samples**

{% tabs %}
{% tab title="Subscription" %}
```javascript
{
  "q": "v1/exchange.marketdata/instrumentList",
  "token": "eyJleGNoYW5nZUlkIjozMCwicHJvamVjdElkIjoyMDB9",
  "sid": 10,
  "d": {
  }
}
```
{% endtab %}

{% tab title="Response" %}
```javascript
{
  "q": "v1/exchange.marketdata/instrumentList",
  "sid": 13,
  "d": {
    "id": "268",
    "symbol": "BA",
    "calendarId": "7",
    "activityStatus": "ACTIVE",
    "minQuantity": "0.000001",
    "maxQuantity": "1000000",
    "pricePrecision": "4",
    "quantityPrecision": "6",
    "description": "Boeing Co.",
    "quoteCurrency": "USD",
    "category": "E",
    "tradingModels": [
      "CLOB"
    ]
  }
}
```
{% endtab %}

{% tab title="Last message" %}
```javascript
{
  "q": "v1/exchange.marketdata/instrumentList",
  "sid": 13,
  "d": {
    "id": "4136",
    "symbol": "INST2",
    "calendarId": "7",
    "activityStatus": "ACTIVE",
    "minQuantity": "1",
    "maxQuantity": "1000000",
    "pricePrecision": "0",
    "quantityPrecision": "0",
    "description": "INST 2",
    "quoteCurrency": "USD",
    "category": "E",
    "tradingModels": [
      "CLOB"
    ],
    "lastMessage": "Y"
  }
}
```
{% endtab %}
{% endtabs %}

