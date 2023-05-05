# Subscriptions Endpoint

Used to fetch a list of all active subscriptions from a CO belonging to the current SP.

## Methods

### GET

#### Available services for a single Access

To get available services for a single access use accessId as key. The response contains details about activated services and the services
 available for activation.
 
Request
```http
GET /onapi/2.6/services/{accessId} HTTP/1.1
```

Response 
```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```
#### Example data from a single access response 

When a single access is requested the response contains a single JSON-object containing the accessId and an array of subscriptions.

```JSON
{
  "accessId": "8732c2f065e2490babce820e94b1011a",
  "subscriptions": [
    {
      "subscriptionId": "8b2ad40b4ffd45e5b48425f57821a7eb",
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
}
```


#### All subscriptions 
Request:
```HTTP
GET /onapi/2.6/subscriptions/
```

#### Subscriptions created or updated since a specific time
Request:
```HTTP
GET /onapi/2.6/subscriptions/
If-Modified-Since: Tue, 05 Feb 2019 14:03:15 GMT
```

Response:
```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```

#### Example for all subscriptions for all accesses

When subscriptions for all accesses are requested the response contains a JSON-array with JSON-objects each containing the accessId and an array of subscriptions. 


```JSON
[
  {
    "accessId": "8732c2f065e2490babce820e94b1011a",
    "subscriptions": [
      {
        "subscriptionId": "8b2ad40b4ffd45e5b48425f57821a7eb",
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
  }
]
```

## Fields

### accessId

 * Data format: [accessId](../common/dataformats.md#accessid)
 * Mandatory

### subscriptions 
Lists of subscriptions.

 * Data format: JSON array of JSON objects
 * Mandatory

### subscriptions/subscriptionId

 * Data format: [ID](../common/dataformats.md#subscriptionid)
 * Mandatory

### subscriptions/service

 * Data format: [text](../common/dataformats.md#service)
 * Mandatory

### subscriptions/operationalState 

 * Data format: [operationalState](../common/dataformats.md#operationalstate)
 * Mandatory
  
### subscriptions/spReference

 * Data format: [ID](../common/dataformats.md#spreference)
 * Mandatory

### subscriptions/spSubscriptionId

 * Data format: [spSubscriptionId](../common/dataformats.md#spsubscriptionid)
 * Mandatory

### subscriptions/option82

 * Data format: [option82](../common/dataformats.md#option82)
 * Deprecated

### subscriptions/dhcpIdentifier

 * Data format: [dhcpIdentifier](../common/dataformats.md#dhcpidentifier)
 
### subscriptions/characteristics

 * Data format: [characteristics](../common/dataformats.md#characteristics)

### subscriptions/equipment

 * Data format: [equipment](../common/dataformats.md#equipment)
