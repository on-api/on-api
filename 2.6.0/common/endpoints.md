# Endpoints endpoint

Path /2.6/

This endpoint is mandatory. It is used to inform the consumer of the API of the available API endpoints and their 
limitations. Can list legacy endpoints for backwards compatibility.

## Operations

### GET

Request
```HTTP
GET /onapi/2.6/ HTTP/1.1
```

```HTTP
HTTP/1.1 200 OK
Location: /onapi/2.6/
Content-Type: application/json
```

```JSON
[
    {
        "name": "accesses",
        "endpoint": "/onapi/2.6/accesses/",
        "version": "2.6",
        "documentation": "https://github.com/on-api/on-api/blob/master/2.6.0/spec/accesses.md"
    },
    { 
        "name": "order",
        "endpoint": "/onapi/2.6/order/",
        "version": "2.6",
        "documentation": "https://github.com/on-api/on-api/blob/master/2.6.0/spec/orders.md",
        "note": "Only supports direct activation, no scheduled orders",
        "unsupportedFields": [
          "requestedDateTime"
        ]
    }
]
```

## Fields

### name
The name of the endpoint.

 * Mandatory
 * Data format: text

### endpoint

URL or Path to the endpoint. If the endpoint is on another server the full URL is used.

 * Mandatory 
 * Data format: text

Examples
 * /onapi/2.6/accesses/
 * https://example.com/onapi/2.6/accesses

### version
Version number of the API
 * Mandatory
 * Data format: text

Examples
 * 2.6
 * 2.5
 * 2.4
 * 2.3.1

### documentation

URL to the documentation of the specific endpoint.

 * Data format: URL
 * Mandatory

### note 

Human readable notes about the endpoint.

 * Data format: text
 * Optional
 
### unsupportedFields

A list of fields that is not supported by the implementation.

 * Data format: array of text
 * Optional