# Error handling

All error handling should be using error codes from HTTP, if possible with the free text field "cause" stating what went wrong.

Example:
```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{ "cause": "Unknown service: 'INTERRNET'" }
```

## HTTP codes used (for full list, see RFC7231)

### 400 Bad request
Invalid data posted

### 401 Unauthorized
Invalid credentials

### 403 Forbidden
Not allowed with current credentials

### 404 Not found
Object not found (on valid API endpoint)

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

An incorrect order should immediatily lead to a "400 Bad Request".

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

If another service for the same servicetype is already active.
E.g. Broadband 100/100 is active when ordering Broadband 10/10:

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

If the service/servicetype is not possible to order since it's already taken by another service provider:

```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{ "cause": "ServiceType is already claimed by other Service Provider." }
```


