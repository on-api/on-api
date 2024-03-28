# Services Endpoint

Used to fetch a list of all available services from a CO belonging to the current SP.

## Methods

### GET

#### Available services for a single Access

To get available services for a single access use accessId as key. The response contains details about the services available for activation.
 
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

When a single access is requested the response contains a single JSON-object containing the accessId and an array of services.

```JSON
{
  "accessId": "8732c2f065e2490babce820e94b1011a",
  "services": [
    {
      "service": "BB-1000-1000",
      "connectionDateTime": "2014-03-01T14:09:23Z",
      "availableDateTime": "2014-03-01T14:09:23Z",
      "disconnectionDateTime": "",
      "forcedTakeoverPossible": false,
      "comments": [
        "This service is limited to 100 Mbps for up to two weeks after ordering"
      ],
      "characteristics": {
        "fixedIp": {
          "required": false,
          "values": [
            true,
            false
          ]
        },
        "ipAddress": {
          "required": false
        },
        "SLA": {
          "required": false,
          "values": [
            "SLA-1",
            "SLA-2",
            "SLA-3"
          ]
        }
      }
    },
    {
      "service": "BB-100-100",
      "connectionDateTime": "2013-10-12T14:09:23Z",
      "availableDateTime": "2013-10-12T14:09:23Z",
      "disconnectionDateTime": "",
      "forcedTakeoverPossible": false
    },
    {
      "service": "BB-10-10",
      "connectionDateTime": "2013-10-12T14:09:23Z",
      "availableDateTime": "2013-10-12T14:09:23Z",
      "disconnectionDateTime": "2018-12-31T14:09:23Z",
      "forcedTakeoverPossible": false
    },
    {
      "service": "IPTV",
      "connectionDateTime": "2013-10-12T14:09:23Z",
      "availableDateTime": "3030-12-12T14:09:23Z",
      "disconnectionDateTime": "",
      "forcedTakeoverPossible": false
    },
    {
      "service": "VOIP",
      "connectionDateTime": "3030-12-12T14:09:23Z",
      "availableDateTime": "3030-12-12T14:09:23Z",
      "disconnectionDateTime": "",
      "forcedTakeoverPossible": true
    }
  ]
}
```


#### All services 
Request:
```HTTP
GET /onapi/2.6/services/
```

#### Services created or updated since a specific time
Request:
```HTTP
GET /onapi/2.6/services/
If-Modified-Since: Tue, 05 Feb 2019 14:03:15 GMT
```

Response:
```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```

#### Example for all services for all accesses

When services for all accesses are requested the response contains a JSON-array with JSON-objects each containing the accessId and an array of services. . 

```JSON
[
  {
    "accessId": "8732c2f065e2490babce820e94b1011a",
    "services": [
    {
      "service": "BB-1000-1000",
      "connectionDateTime": "2014-03-01T14:09:23Z",
      "availableDateTime": "2014-03-01T14:09:23Z",
      "disconnectionDateTime": "",
      "forcedTakeoverPossible": false,
      "comments": [
        "This service is limited to 100 Mbps for up to two weeks after ordering"
      ],
      "characteristics": {
        "fixedIp": {
          "required": false,
          "values": [
            true,
            false
          ]
        },
        "ipAddress": {
          "required": false
        },
        "SLA": {
          "required": false,
          "values": [
            "SLA-1",
            "SLA-2",
            "SLA-3"
          ]
        }
      }
    },
    {
      "service": "BB-100-100",
      "connectionDateTime": "2013-10-12T14:09:23Z",
      "availableDateTime": "2013-10-12T14:09:23Z",
      "disconnectionDateTime": "",
      "forcedTakeoverPossible": false
    },
    {
      "service": "BB-10-10",
      "connectionDateTime": "2013-10-12T14:09:23Z",
      "availableDateTime": "2013-10-12T14:09:23Z",
      "disconnectionDateTime": "2018-12-31T14:09:23Z",
      "forcedTakeoverPossible": false
    },
    {
      "service": "IPTV",
      "connectionDateTime": "2013-10-12T14:09:23Z",
      "availableDateTime": "3030-12-12T14:09:23Z",
      "disconnectionDateTime": "",
      "forcedTakeoverPossible": false
    },
    {
      "service": "VOIP",
      "connectionDateTime": "3030-12-12T14:09:23Z",
      "availableDateTime": "3030-12-12T14:09:23Z",
      "disconnectionDateTime": "",
      "forcedTakeoverPossible": true
    }
  ]
  }
]
```



## Fields

### accessId

Identifies a single access. Used as key when fetching a single access and ordering services.

 * Data format: [accessId](../common/dataformats.md#accessid)
 * Mandatory
 
### services 
Lists of deliverable services.

 * Data format: JSON array of JSON objects
 * Mandatory

### services/service

Name of the service, used as reference in the [order API](orders.md)

 * Data format: [text](../common/dataformats.md#text)
 * Mandatory

### services/connectionDateTime

Indicates when the service is technically deliverable for the first time. If you don't have a date when it was connected, you can specify the date as "1990-01-01T00:00:01Z". If you don't know when it will be connected, you can specify the date as "3030-12-12T00:00:01Z" for example.

 * Data format: [ISO 8601 date time](../common/dataformats.md#datetime)
 * Mandatory

### services/availableDateTime 

Indicates when the service can be ordered. If you don't know when it will be available, you can specify the date as empty string "". If a service will be available to a future date due to ongoing cancellation by another service provider, then the future available date can be provided for calling service provider.

 * Data format: [ISO 8601 date time](../common/dataformats.md#datetime) (Valid values are also empty string "")
 * Mandatory


### services/disconnectionDateTime

Specifies when a service is no longer available. This can indicate that a certain service will no longer be available after the given date or that the access itself will be unavailable and in that case all the services will have a disconnection date. 
 
 * Data format: [ISO 8601 date time](../common/dataformats.md#datetime) (Valid values are also empty string "")
 * Mandatory but can be empty

### services/forcedTakeoverPossible

Specifies if a service provider can replace another service providers activated service. 

 * Data format: [boolean](../common/dataformats.md#boolean)
 * Mandatory

### services/comments

A list of messages from the CO intended for the end customer. 

 * Data format: JSON array of [text](../common/dataformats.md#text)
 * Optional 
 
Examples: 
 * An agreement with Acme Networks is required to use this service
 * This service is limited to 100 Mbps for up to two weeks after ordering
 * Additional equipment needed for this service can be picked up at Acme Networks office

### services/characteristics

Characteristics available when ordering this service.

 * JSON object
 * Available with single access

### services/characteristics/[type]/required

 Specifies if the characteristic of [type] is required for activation

 * Data format [boolean](../common/dataformats.md#boolean)

### services/characteristics/[type]/validValues

Array with valid values if applicable 

 * JSON array

