# Subscriptions API

Used to fetch a list of all active services or subscriptions from a CO belonging to the current SP.

## Methods

### GET

Request:
```HTTP
GET /api/2.4/subscriptions/
```

Response:
```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```
```JSON
[
  {
    "service": "BB-1000-100",
    "accessId": "STTA0001",
    "coSubscriptionId": "8b2ad40b4ffd45e5b48425f57821a7eb",
    "spReference": "WloKMvmArcCFiV679uhWpAAtNgyvHxma",
    "spSubscriptionId": "b49797aaed934642bc8ae136b87ed12b"
  },
  {
    "service": "IPTV",
    "accessId": "STTA0001",
    "coSubscriptionId": "af5143edb9624223810689c4100525f0",
    "spReference": "WloKMvmArcCFiV679uhWpAAtNgyvHxma",
    "spSubscriptionId": "55498978c4c446d0bbc2ae347a61e78d"
  }
]
```

## Fields

### service

 * Data format: text
 * Mandatory
 
### accessId

 * Data format: ID
 * References: accessId in [Accesses API](accesses.md)
 * Mandatory

### coSubscriptionId
 * Data format: ID
 * Mandatory
  
### spReference
 * Data format: ID
 * Mandatory

### spSubscriptionId
 * Data format: ID
 * Mandatory