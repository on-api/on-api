#  Responses

All error handling should be using status codes from HTTP, if possible with the free text field "cause" stating what went wrong. If the server has an ID of the error (such as a fault number or, even better, a ticket ID it should be included in the cause field.

Example:
```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{ "cause": "Unknown service: 'INTERRNET'" }
```
Example 2:
```http
HTTP/1.1 500 Internal Server Error
Content-Type: application/json

{ "cause": "An Unknown error has occured. Error number 12345" }
```
## HTTP satus codes used (for full list, see RFC7231)

### 400 Bad request
Invalid data posted

### 401 Unauthorized
Invalid credentials

### 403 Forbidden
Not allowed with current credentials

### 404 Not found
Object not found (on valid API endpoint)

### 409 Conflict
Object is conflicting with other object (on valid API endpoint). 

### 429 Too Many Requests
The client is sending too many requests to the server in too short time. If Retry-After is used in the response the client should honor that time before sending any more requests. 

### 500 Internal Server Error
Unrecoverable error

### 501 Not implemented

Response for unknown or unimplemented API endpoints


{ "cause": "error description" }

## Error handling and behaviour when creating an order

If the order is correctly formed the response should be like this:

```http
HTTP/1.1 201 CREATED
Content-Type: application/json
Location: /api/2.3.1/orders/ec4bc754-6a30-11e2-a585-4fc569183061

{
    "path": "/api/2.3.1/orders/ec4bc754-6a30-11e2-a585-4fc569183061",
    "accessId": "STTA0001",
    "service": "BB-100-10",
    "operation": "ACTIVATE",
    "state": "RECEIVED",
    "message": ""
}
```

An incorrect order should immediately lead to a "400 Bad Request".

This error should be presented for:
* Incorrect JSON
* Missing obligatory fields
* Wrong content in fields
* Wrong AccessId
* Wrong service for access.

```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{ "cause": "Unknown service: 'INTERRNET'" }
```

If another service for the same service type is already active.
E.g. Broadband 100/100 is active when ordering Broadband 10/10:
```http
HTTP/1.1 409 Conflict
Content-Type: application/json

{ "cause": "Another Service of ServiceType 'Broadband' is already active." }
```
For compatibility with older API-versions this could also be correct:
```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{ "cause": "Another Service of ServiceType 'Broadband' is already active." }
```

If the service already has an active order:

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "path": "/api/2.3.1/orders/ec4bc754-6a30-11e2-a585-4fc569183061",
    "accessId": "STTA0001",
    "service": "BB-100-10",
    "operation": "ACTIVATE",
    "state": "RECEIVED",
    "message": ""
}
```

If the service is already active when doing `ACTIVATE`, or inactive when doing `DEACTIVATE`:

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "accessId": "STTA0001",
    "service": "BB-100-10",
    "operation": "ACTIVATE",
    "state": "DONE_SUCCESS",
    "message": ""
}
```

If the service/service type is not possible to order since it's already taken by another service provider:

```http
HTTP/1.1 409 Conflict
Content-Type: application/json

{ "cause": "ServiceType is already claimed by other Service Provider." }
```
For compatibility with older API-versions this could also be correct:
```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{ "cause": "ServiceType is already claimed by other Service Provider." }
```


