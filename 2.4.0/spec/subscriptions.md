# Subscriptions API

Used to fetch a list of all active services or subscriptions from a CO belonging to the current SP.

## Methods

### GET

#### All subscriptions 
Request:
```HTTP
GET /api/2.4/subscriptions/
```

#### Subscriptions created or updated since a specific time
Request:
```HTTP
GET /api/2.4/subscriptions/
If-Modified-Since: Tue, 05 Feb 2019 14:03:15 GMT
```

Response:
```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```
```JSON
[
  {
    "subscriptionId": "8b2ad40b4ffd45e5b48425f57821a7eb",
    "accessId": "8732c2f065e2490babce820e94b1011a",
    "service": "BB-1000-1000",
    "operationalState": "ACTIVATED",
    "spReference": "WloKMvmArcCFiV679uhWpAAtNgyvHxma",
    "spSubscriptionId": "b49797aaed934642bc8ae136b87ed12b",
    "option82": "52270123434F2D38373332633266303635653234393062616263653832306539346231303131610200",
    "dhcpIdentifier": {
      "ipv4CircuitId": "CO-8732c2f065e2490babce820e94b1011a"
    },
    "note": "Connection will be upgraded to 1000 Mbps at 2019-02-20",
    "characteristics": {
      "fixedIp": true,
      "ipAddress": [
        "1.2.3.4"
      ],
      "SLA": "SLA-3"
    }
  },
  {
    "subscriptionId": "af5143edb9624223810689c4100525f0",
    "accessId": "8732c2f065e2490babce820e94b1011a",
    "service": "IPTV",
    "operationalState": "ACTIVATED",
    "spReference": "WloKMvmArcCFiV679uhWpAAtNgyvHxma",
    "spSubscriptionId": "55498978c4c446d0bbc2ae347a61e78d",
    "option82": "52270123434F2D38373332633266303635653234393062616263653832306539346231303131610200",
    "dhcpIdentifier": {
      "ipv4CircuitId": "CO-8732c2f065e2490babce820e94b1011a"
    },
    "equipment": [
      {
        "vendorId": "ACME-IPTV",
        "macAddress": "AA:BB:CC:11:22:33"
      },
      {
        "vendorId": "ACME-IPTV",
        "macAddress": "AA:BB:CC:44:55:66"
      }
    ]
  }
]
```

## Fields

### subscriptionId

 * Data format: [ID](dataformats.md#subscriptionid)
 * Mandatory

### accessId

 * Data format: [accessId](dataformats.md#accessid)
 * Mandatory

### service

 * Data format: [text](dataformats.md#service)
 * Mandatory

### operationalState 

 * Data format: [operationalState](dataformats.md#operationalstate)
 * Mandatory
  
### spReference

 * Data format: [ID](dataformats.md#spreference)
 * Mandatory

### spSubscriptionId

 * Data format: [spSubscriptionId](dataformats.md#spsubscriptionid)
 * Mandatory

### option82

 * Data format: [option82](dataformats.md#option82)
 * Deprecated

### dhcpIdentifier

 * Data format: [dhcpIdentifier](dataformats.md#dhcpidentifier)
 
### characteristics

 * Data format: [characteristics](dataformats.md#characteristics)

### equipment

 * Data format: [equipment](dataformats.md#equipment)
