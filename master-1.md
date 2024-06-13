# Technical Guidelines

API protocol is WebSocket (unless mentioned otherwise) \
Any request body should be a valid `JSON`, non valid `JSON` objects will be ignored.

Within the valid `JSON` please be aware that:

* System ignores any additional parameter that was sent on request body but was not specified in this document.
* In case of multiple parameters sent with different values, system will always use the last value provided.

### **Request Parameters**

<table><thead><tr><th width="121.4">Parameter</th><th width="150">Type</th><th>Description</th></tr></thead><tbody><tr><td>q</td><td>String</td><td>qualifier, contains the method for the specific API call.</td></tr><tr><td>token</td><td>String</td><td>Token is configurable value per environment, it allows accurate and efficient instrument discovery. <br>Token generation described on the <a href="./">Introduction </a>section.</td></tr><tr><td>sid</td><td>Int</td><td>stream identifier, for each WebSocket connection this is a unique identifier for the API call. Please note that as long as the sid was not ended (other by exchange or by consumer) this can’t be used again on the same WebSocket connection</td></tr><tr><td>d</td><td>Json</td><td>data object, contain the request body</td></tr></tbody></table>

```javascript
{ 
 "q":"exchange.market/placeOrder", 
 "token": "eyJleGNoYW5nZUlkIjozMCwicHJvamVjdElkIjoyMDB9",
 "sid":1, 
 "d": 
   { 
     Object
   } 
}
```

### **Success Response**

The response will always include the `q` and `sid` parameters from request and a `d` parameter with the response body.

```javascript
{ 
   "q":"exchange.market/placeOrder", 
   "sid":1, 
   "d": 
     { 
       Object
     } 
}
```

In case of short living stream (i.e. trading action), additional response will be sent upon stream closure with success, this message will include the `q` and `sid` parameters from request and `sig:1`.

```javascript
{
  "sig": 1,
  "q": "exchange.market/createSession",
  "sid": 1
}
```

### **Failure Response**

The response will always include the below parameters:

<table><thead><tr><th width="150">Parameter</th><th width="355">Description</th></tr></thead><tbody><tr><td>sig</td><td>signal will be equal to "2"</td></tr><tr><td>q</td><td>from request</td></tr><tr><td>errorType</td><td>internal error type that should be ignored</td></tr><tr><td>sid</td><td>from request</td></tr><tr><td>d</td><td>data that contain errorCode and errorMessage. <br>Those are the error code and message to consider.</td></tr></tbody></table>

```javascript
{
  "sig": 2,
  "q": "exchange.market/createSession",
  "errorType": "401",
  "sid": 1,
  "d": {
    "errorCode": 6002,
    "errorMessage": "Missing fields: 'apiKey'"
  }
}
```

### **Stream Closure**

In order to close active stream need to send a message with `sig:3` in addition to `q` and `sid` from request.

```javascript
{
  "sig": 3,
  "q": "exchange.market/orderBookDepth",
  "sid": 100
}
```

sig parameter summary table:

<table><thead><tr><th width="150">sig</th><th width="338.8571428571429">Description</th></tr></thead><tbody><tr><td>1</td><td>Stream closed with success</td></tr><tr><td>2</td><td>Stream closed with failure</td></tr><tr><td>3</td><td>Stream was closed due to consumer request</td></tr></tbody></table>

### Heartbeats (Pings) <a href="#websocket-heartbeats" id="websocket-heartbeats"></a>

The WebSocket connection supports ping messages for the client to identify connection drops. Ping requests can be made on-demand, and the server responds to each request.

It is recommended that this API should only be used for heartbeats from the browser. Use WebSocket [native ping/pong](https://datatracker.ietf.org/doc/html/rfc6455#section-5.5.2) for outher use cases.

{% hint style="info" %}
qualifier: `v1/heartbeat/ping`
{% endhint %}

### **Request Parameters**

<table><thead><tr><th width="121.4">Parameter</th><th width="150">Type</th><th>Description</th></tr></thead><tbody><tr><td>d</td><td>Int</td><td>This value will be returned in the response.</td></tr></tbody></table>

###

### **Samples**

{% tabs %}
{% tab title="Request" %}
<pre class="language-javascript"><code class="lang-javascript"><strong>{
</strong>  "q": "v1/heartbeat/ping",
  "sid": 1,
  "d": 42
}
</code></pre>
{% endtab %}

{% tab title="Success Response" %}
```javascript
{
  "q": "v1/heartbeat/ping",
  "sid": 1,
  "d": 42
}
```
{% endtab %}

{% tab title="Failure Response" %}
```json
{
  "sig": 2,
  "q": "v1/heartbeat/ping",
  "errorType": "500",
  "sid": 1,
  "d": {
    "errorCode": 500,
    "errorMessage": "Failed to decode service message data"
  }
}
```
{% endtab %}
{% endtabs %}



