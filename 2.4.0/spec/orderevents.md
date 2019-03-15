# Order Events API
Path /2.4/orderevents/

This API lists changes to orders. When an order state changes a event row is created that can be polled with this API. 
The event list is immutable and shall not change after a event have been created.

## Operations 

### GET

#### All events
```http
GET /onapi/2.4/orderevents/ HTTP/1.1
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

[
    {
        "event": "2a6d6432e59d11e39a523c970e806452",
        "order": {
            "path": "/api/2.3.1/orders/ec4bc7546a3011e2a5854fc569183061",
            "accessId": "STTA0001",
            "service": "BB-100-10",
            "operation": "DEACTIVATE",
            "state": "DONE_SUCCESS",
            "message": ""
        }
    }
 ]
```

#### Events since last fetch
To get events the last event ID in the previous fetch is used as a parameter to the next GET operation.

Request:
```http
GET /onapi/2.4/orderevents/?since=2a6d6432e59d11e39a523c970e806452 HTTP/1.1
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

[
    {
        "event": "6b4f026bccf247efb39f22ec4b01c1be",
        "order": {
            "path": "/api/2.4/orders/3393123ae59f11e393713c970e806452",
            "accessId": "STTA0002",
            "service": "BB-100-10",
            "operation": "ACTIVATE",
            "state": "DONE_FAILED",
            "message": "The service type is no longer available for this access"
        }
    }
 ]
```

## Fields

### event
ID of the event, used as a parameter to fetch following events 

 * Data format: ID
 * Mandatory
 
### order 
Object containing select fields from the order
 * Mandatory
 * See [order](orders.md)

**fields from order**
 * path
 * accessId
 * service
 * operation
 * state
 * message