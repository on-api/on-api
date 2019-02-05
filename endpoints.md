# Endpoints API

Path /2.4/

This API endpoint is mandatory. It is used to inform the consumer of the API of the available API endpoints and their 
limitations.

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
        "documentation": "https://github.com/on-api/onapi-inprogress-2.4/blob/master/accesses.md",
        "endpoint": "/opapi/2.4/accesses/",
        "note": "",
        "unsupportedFields": []
    },
    { 
        "name": "order",
        "endpoint": "/opapi/2.4/order/",
        "documentation": "https://github.com/on-api/onapi-inprogress-2.4/blob/master/order.md",
        "note": "Only supports direct activation, no scheduled orders",
        "unsupportedFields": [
          "requestedDateTime"
        ]
    }    
]
```

## Fields

### name
The name of the API.

 * Mandatory
 * Data format: text

### endpoint

Path to the API endpoint.

 * Mandatory 
 * Data format: text

Examples
 * /onapi/2.4/accesses/

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