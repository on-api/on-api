# Endpoints API

Path /2.4/

This API endpoint is mandatory. It is used to inform the consumer of the API of the available API endpoints and their 
limitations.

##Operations

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
        "endpoint": "accesses",
        "note": "",
        "unsuppportedFields": []
    },
    { 
        "endpoint": "order",
        "note": "Only supports direct activation, no scheduled orders",
        "unsupportedFields": [
          "requestedDateTime"
        ]
    }    
]
```


## Fields

### endpoint

The path and name of the endpoint

 * Mandatory 
 * Data format: text 
 
### note 

Human readable notes about the API-endpoint.

 * Data format: text
 * Optional
 
### unsupportedFields

A list of fields that is not supported by the implementation of the API.

 * Data format: array of text
 * Optional