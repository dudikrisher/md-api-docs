# Light Tickers

## lightTickers

This API allows easy refresh of the instruments market data.\
Upon subscription data for all instruments will sent, afterward, data for specific instrument will be returned only in case one of the values was changed (it will not not be sent on real time but only when interval time reached)

This API is not considering trade cancellations.

{% hint style="info" %}
`qualifier:` v1/exchange.marketdata/lightTickers
{% endhint %}

### **Request**

<table><thead><tr><th width="146.17225950782998">Parameter</th><th width="94">Type</th><th width="446.2">Description</th></tr></thead><tbody><tr><td>symbols</td><td>[]String</td><td>List of symbols to retrieve the light tickers for </td></tr><tr><td>interval</td><td>eNum</td><td>Response interval in milliseconds, allowed values: 100,1000,2000</td></tr><tr><td><mark style="color:blue;">(NEW v1.23.0)</mark><br>scope</td><td>eNum</td><td><p>Optional</p><p>Specifies the type of data used to calculate: <code>lastPrice</code>, <code>lastQuantity</code>, <code>high</code>, <code>low</code>, <code>volume</code>, <code>quoteVolume</code> fields.</p><p></p><p>Supported Values:</p><ul><li>CLOB - data is derived from order book executions only</li><li>All - data is derived from all trades (CLOB, trade entry and RFQ) </li></ul><p>If not sent - CLOB is the default </p></td></tr></tbody></table>

### **Response**

<table><thead><tr><th width="175.6710763680096">Parameter</th><th width="132">Type</th><th width="423.2">Description</th></tr></thead><tbody><tr><td>symbol</td><td>String</td><td>Instrument symbol </td></tr><tr><td>lastPrice</td><td>Decimal</td><td>last execution price <mark style="color:blue;">(CHANGED v1.23.0)</mark> as per the <code>scope</code>. <del>(including the data from the trade entry <mark style="color:blue;">(NEW v1.22.0)</mark> and RFQ trades)</del></td></tr><tr><td>lastQuantity </td><td>Decimal</td><td>Last executed trade quantity <mark style="color:blue;">(CHANGED v1.23.0)</mark> as per the <code>scope</code>. <del>(including the data from the trade entry <mark style="color:blue;">(NEW v1.22.0)</mark> and RFQ trades)</del></td></tr><tr><td>bidPrice</td><td>Decimal</td><td>Highest bid price</td></tr><tr><td>bidQuantity</td><td>Decimal</td><td>Sum of quantity of all orders with <code>bidPrice</code></td></tr><tr><td>askPrice</td><td>Decimal</td><td>Lowest ask price</td></tr><tr><td>askQuantity</td><td>Decimal</td><td>Sum of quantity of all orders with the <code>askPrice</code></td></tr><tr><td>timeStamp</td><td>Unix timestamp</td><td>Latest timestamp where one of the above values was changed </td></tr><tr><td>openingPrice</td><td>Decimal</td><td>First order book trade on the day, will be empty until first execution is happening</td></tr><tr><td>low</td><td>Decimal</td><td>Lowest order book executed price of the day <mark style="color:blue;">(CHANGED v1.23.0)</mark> as per the <code>scope</code>. <del>(including the data from the trade entry <mark style="color:blue;">(NEW v1.22.0)</mark> and RFQ trades)</del></td></tr><tr><td>high </td><td>Decimal</td><td>Highest order book executed price of the day <mark style="color:blue;">(CHANGED v1.23.0)</mark> as per the <code>scope</code>. <del>(including the data from the trade entry <mark style="color:blue;">(NEW v1.22.0)</mark> and RFQ trades)</del></td></tr><tr><td>volume</td><td>Decimal</td><td>Total trade volume (in base asset) <mark style="color:blue;">(CHANGED v1.23.0)</mark> as per the <code>scope</code>. <del>(including the data from the trade entry <mark style="color:blue;">(NEW v1.22.0)</mark> and RFQ trades)</del></td></tr><tr><td>quoteVolume </td><td>Decimal</td><td><p>Total trade volume in quote asset <mark style="color:blue;">(CHANGED v1.23.0)</mark> as per the <code>scope</code>.<br><span class="math"> \xi (Trade Amount * Absolute Value Of Trade Price) </span> </p><p><del>sum[TradeAmount*TradePrice]</del> </p><p><del>(including the data from the trade entry <mark style="color:blue;">(NEW v1.22.0)</mark> and RFQ trades)</del></p></td></tr><tr><td>closingPrice </td><td>Decimal</td><td>Last day closing price (=last order book trade on the day)</td></tr><tr><td>closingPriceTimestamp  </td><td>Unix timestamp</td><td>The time where closing price was determined</td></tr><tr><td>settlementPrice</td><td>Decimal</td><td>Settlement price</td></tr><tr><td>settlementPriceTimestamp </td><td>Unix timestamp</td><td>Settlement price last update timestamp</td></tr><tr><td>status</td><td>Enum</td><td>The trading status of the instrument.<br>Trading/ Closed/ Halted/ AuctionCall/ AuctionCrossing</td></tr><tr><td> referencePrice </td><td>Decimal</td><td>Reference Price to be considered on the daily price bands and market rate circuit breakers. </td></tr><tr><td>referencePriceTimestamp</td><td>Unix timestamp</td><td>Reference Price last update timestamp</td></tr><tr><td>volumeTypes</td><td>[] Object</td><td>Array of all relevant volumes</td></tr></tbody></table>

volumeTypes object:

<table><thead><tr><th width="124.33333333333331">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>type</td><td>Enum</td><td><p>The type of the volume:</p><ul><li>MATCHED: Order book trades </li><li>EFRP: EFRP trade entry</li><li>BLOCK: Block trade entry </li><li>OTHER: Other trade entry</li><li><mark style="color:blue;">(NEW v1.22.0)</mark> RFQ: RFQ trades</li></ul></td></tr><tr><td>volume</td><td>Decimal</td><td>Total trade volume (in base asset) for the specific volume type</td></tr></tbody></table>

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
    "status": "Trading",
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
    "settlementPriceTimestamp": 1673793853931,
    "volumeTypes": [
    {
      "type": "EFRP",
      "volume": 1234
    },
    {
      "type": "Block",
      "volume": 5555
    },
   {
      "type": "Other",
      "volume": 6666
    },
    {
      "type": "Matched",
      "volume": 7878
    },
    {
      "type": "RFQ",
      "volume": 44
    },
    "referencePrice": 1.68,
    "referencePriceTimestamp": 1686002400000
  ]
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
    "status": "Trading",
    "timeStamp": 1674115200000,
    "volume": 0,
    "quoteVolume": 0
  }
}
```
{% endtab %}
{% endtabs %}

### **Error Codes**

<table><thead><tr><th width="169.57142857142856">Code</th><th>Message</th></tr></thead><tbody><tr><td>1</td><td>System is unavailable</td></tr><tr><td>2</td><td>Missing fields: [Fieldname]</td></tr><tr><td>3</td><td>Wrong interval |<br>Wrong symbol</td></tr></tbody></table>

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
