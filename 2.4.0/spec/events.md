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
    "type": "CREATE",
    "objectType": "order",
    "objectId": "b5314ed39557472098843fe0ab358069",
    "path": "/onapi/2.4/order/b5314ed39557472098843fe0ab358069",
    "time": "2019-02-04T13:03:16.1252"
  },
  {
    "type": "DELETE",
    "objectType": "access",
    "objectId": "849f97124c4840629535c7f204e8cf09",
    "time": "2019-02-04T13:03:16.5230"
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

### type

 * Data format: enumeration

Values: 
 * CREATE
 * UPDATE
 * DELETE


### objectType

 * Data format: enumeration

Values: 
 * accesses
 * orders
 * subscriptions
 * tickets

### objectId

The ID of the object that triggered the event

 * Data format: ID

### path

URL path to the object the event is for

 * Data format: text 
 * Mandatory for eventTypes CREATE and UPDATE
 * Omitted for eventType DELETE
 
### time

 * Data format: dateTime
