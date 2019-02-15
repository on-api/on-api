# Endpoints API

Path /2.4/

This API endpoint is mandatory. It is used to inform the consumer of the API of the available API endpoints and their 
limitations. Can list legacy API endpoints for backwards compatibility.

## Operations

### GET

Request
```HTTP
GET /onapi/2.4/ HTTP/1.1
```

```HTTP
HTTP/1.1 200 OK
Location: /onapi/2.4/
Content-Type: application/json
```

```JSON
[
    {
        "name": "accesses",
        "endpoint": "/onapi/2.4/accesses/",
        "version": "2.4",
        "documentation": "https://github.com/on-api/onapi-inprogress-2.4/blob/master/accesses.md"
    },
    { 
        "name": "order",
        "endpoint": "/onapi/2.4/order/",
        "version": "2.4",
        "documentation": "https://github.com/on-api/onapi-inprogress-2.4/blob/master/orders.md",
        "note": "Only supports direct activation, no scheduled orders",
        "unsupportedFields": [
          "requestedDateTime"
        ]
    },
    {
        "name": "order",
        "documentation": "https://github.com/on-api/on-api-release-2.3.1/blob/master/service_activation.md",
        "endpoint": "https://example.com/onapi/2.4/opapi/2.3/order/",
        "version": "2.3.1"
    }
]
```

## Fields

### name
The name of the API.

 * Mandatory
 * Data format: text

### endpoint

URL or Path to the API endpoint. If the endpoint is on another server the full URL is used.

 * Mandatory 
 * Data format: text

Examples
 * /onapi/2.4/accesses/
 * https://example.com/onapi/2.4/accesses

### version
Version number of the API
 * Mandatory
 * Data format: text

Examples
 * 2.4
 * 2.3.1

### documentation

URL to the documentation of the specific API endpoint.

 * Data format: URL
 * Mandatory

### note 

Human readable notes about the API-endpoint.

 * Data format: text
 * Optional
 
### unsupportedFields

A list of fields that is not supported by the implementation of the API.

 * Data format: array of text
 * Optional