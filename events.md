# Events

Path: /onapi/2.4/events

Lists object changes. 

## Operations 

### GET


#### All available events
Get all events stored in the system up to the previous second. Events should be stored for a minimum of 24 hours.
Events for the current second is omitted to ensure that events are not sent twice. This is to get around a limitation 
in the "If-Modified-Since" header that does not allow fractional seconds. 

```HTTP
/onapi/2.4/events/ HTTP/1.1
```

Response 
```HTTP
HTTP/1.1 200 OK
Content-Type: application/json

Last-Modified: Tue, 05 Feb 2019 13:03:15 GMT
```
```JSON
[
  {
    "eventType": "CREATE",
    "objectType": "order",
    "objectId": "b5314ed39557472098843fe0ab358069",
    "path": "/onapie/2.4/order/b5314ed39557472098843fe0ab358069",
    "eventTime": "2019-02-04T13:03:16.1252",
    "object": {
      "path": "/onapi/2.4/orders/f3f26446f6e8407aae876ea8e52d7417",
      "accessId": "8732c2f065e2490babce820e94b1011a",
      "coSubscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
      "service": "BB-1000-100",
      "operation": "ACTIVATE",
      "state": "RECEIVED",
      "forcedTakeover": false,
      "equipment": [
        {
          "vendorId": "ACME-ROUTER",
          "macAddress": "AA:BB:CC:11:22:33"
        }
      ],
      "spReference": "a6cc5da980034948ba654ae6ceda03f4",
      "spSubscriptionId": "d02925f0083b4f64993b365accfbb1ac",
      "requestedDateTime": "2019-02-05T00:00:00Z",
      "expectedCompletionDate": "2019-02-05T00:00:01Z",
      "characteristics": {
        "fixedIp": true,
        "ipaddress": [
          "1.2.3.4/32"
        ],
        "SLA": "SLA-3"
      }
    }
  },
  {
    "eventType": "DELETE",
    "objectType": "access",
    "objectId": "849f97124c4840629535c7f204e8cf09",
    "eventTime": "2019-02-04T13:03:16.5230"
  }
]
```

### New events

Use the "Last-Modified" header value as parameter for "If-Modified-Since" header to fetch new events. This operation 
needs to be fairly lightweight on the API-server side to allow rapid requests.

Request
```HTTP
/onapi/2.4/events/ HTTP/1.1
If-Modified-Since: Tue, 05 Feb 2019 13:03:15 GMT
```

Response
```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
Last-Modified: Tue, 05 Feb 2019 13:03:16 GMT
```

Response if no updates is available 
```HTTP
HTTP/1.1 304 Not Modified
Content-Type: application/json
```

## Fields

### eventType
 * Data format: enumeration

Values: 
 * CREATE
 * UPDATE
 * DELETE


### objectType
 * Data format: enumeration

Values: 
 * accesses
 * order
 * services

### objectId
The ID of the object that triggered the event
 * Data format: ID

### path
URL path to the object the event is for
 * Data format: text 
 * Mandatory for eventTypes CREATE and UPDATE
 * Omitted for eventType DELETE
 
### eventTime
 * Data format: dateTime

### object
Object data after the event with eventType CREATE and UPDATE. Object data before the event when eventType is DELETE. 
The object may include only updated fields. 

 * Optional
 * Data type: JSON object

