# (NEW v1.20) Calendar List

This API provides snapshot and real-time updates for calendar details.&#x20;

Upon successful subscription, a snapshot of all calendars is sent. The last message of the snapshot contains `lastMessage=Y`. Any changes to the calendars after the snapshot are sent as subsequent updates.

{% hint style="info" %}
`qualifier:` v1/exchange.marketdata/calendarList
{% endhint %}

### **Request**

No request parameters



### **Response**

Similar to [this](https://www.postman.com/exberry-team/workspace/admin-api/folder/6229811-94a026ea-4e5c-48ae-84f9-9980a8e58278).



### **Error Codes**

<table><thead><tr><th width="150">Code</th><th width="554.4285714285713">Message</th></tr></thead><tbody><tr><td>1</td><td>System is unavailable</td></tr></tbody></table>



### **Samples**

{% tabs %}
{% tab title="Subscription" %}
```javascript
{
  "q": "v1/exchange.marketdata/calendarList",
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
  "q": "v1/exchange.marketdata/calendarList",
  "sid": 13,
  "d": {
    "id": "2692",
    "name": "cal3",
    "timeZone": "+05:30",
    "marketOpen": "09:30",
    "marketClose": "16:00",
    "tradingDays": [
      "MONDAY",
      "TUESDAY",
      "WEDNESDAY",
      "THURSDAY",
      "FRIDAY",
      "SATURDAY",
      "SUNDAY"
    ],
    "holidays": [
      {
        "date": "2023-10-20",
        "closeTime": "13:30",
        "name": "Holiday 1"
      },
      {
        "date": "2023-10-25",
        "name": "Holiday 2"
      }
    ],
    "auctions": [
      {
        "days": [],
        "startTimes": [],
        "duration": "300000",
        "matchingAlgorithm": "EQUILIBRIUM_PRICE",
        "allowedTimeInForces": [
          "GTC",
          "GTD",
          "GAA",
          "DAY"
        ],
        "eventsModes": [
          "LIT",
          "INDICATIVE_PRICE"
        ],
        "auctionType": "MANY_TO_MANY",
        "indicativePriceFrequency": "1000",
        "trigger": "Resume",
        "overrideReferencePrice": false
      },
      {
        "days": [],
        "startTimes": [],
        "duration": "900000",
        "matchingAlgorithm": "EQUILIBRIUM_PRICE",
        "allowedTimeInForces": [
          "GTC",
          "GTD",
          "GAA",
          "DAY"
        ],
        "eventsModes": [
          "LIT",
          "INDICATIVE_PRICE"
        ],
        "auctionType": "ONE_TO_MANY",
        "buyMpList": [
          "14"
        ],
        "indicativePriceFrequency": "1000",
        "trigger": "AutoResume",
        "overrideReferencePrice": false
      }
    ]
  }
}
```
{% endtab %}

{% tab title="Last message" %}
```javascript
{
  "q": "v1/exchange.marketdata/calendarList",
  "sid": 13,
  "d": {
    "id": "2692",
    "name": "cal3",
    "timeZone": "+05:30",
    "tradingDays": [
      "MONDAY",
      "TUESDAY",
      "WEDNESDAY",
      "THURSDAY",
      "FRIDAY",
      "SATURDAY",
      "SUNDAY"
    ],
    "holidays": [],
    "auctions": [],
    "lastMessage": "Y"
  }
}
```
{% endtab %}
{% endtabs %}









