# IP lookup
path /2.4/ip_lookup/

## Operations

### GET

Look up an order based on IP address and time, returns a single orderId.

### Parameters 

   * ipAddress      ipAddress
   * allocatedTime  ipAddress

Request:
```HTTP
GET /api/2.4/ip_lookup/?ipaddress=10.10.10.10&allocatedTime=2019-02-05T00:00:00Z HTTP/1.1
```

Response:

```HTTP
HTTP/1.1 200 OK
Content-Type: application/json

{
    "OrderId": "96bd5353f0854cb4a18457d9b5f66d4b"
}
```

### Fields

 #### orderID
 * Data format: ID
 * References: [orders/orderid](orders.md)
