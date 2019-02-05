# Order 
 * Endpoint orders/

This API allows the service provider to activate, deactivate, suspend, resume, update and change services. Once an order
is no longer in the "RECEIVED" no changes can be made to that order.

## Operations 

### GET

Used to fetch placed orders.

#### Get all unfinished orders

Request
```HTTP
GET /onapi/2.4/orders/ HTTP/1.1
```

Response
```HTTP
HTTP/1.1 200 OK
Location: /onapi/2.4/orders/f3f26446f6e8407aae876ea8e52d7417
Content-Type: application/json
```

```JSON
[
  {
    "path": "/onapi/2.4/orders/f3f26446f6e8407aae876ea8e52d7417",
    "accessId": "8732c2f065e2490babce820e94b1011a",
    "coSubscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
    "service": "BB-1000-100",
    "operation": "ACTIVATE",
    "state": "RECEIVED",
    "forcedTakeover": false,
    "equipment": [
      {
        "vendorId": "ACME-ROUTER",
        "macAddress": "AA:BB:CC:11:22:33"
      }
    ],
    "spReference": "a6cc5da980034948ba654ae6ceda03f4",
    "spSubscriptionId": "d02925f0083b4f64993b365accfbb1ac",
    "requestedDateTime": "2019-02-05T00:00:00Z",
    "expectedCompletionDate": "2019-02-05T00:00:01Z",
    "characteristics": {
      "fixedIp": true,
      "ipaddress": [
        "1.2.3.4/32"
      ],
      "SLA": "SLA-3"
    }
  }
]
```

#### Get all unfinished orders pertaining a specific acccessId

Request
```HTTP
GET /onapi/2.4/orders/?accessId=8732c2f065e2490babce820e94b1011a HTTP/1.1
```

Response
```HTTP
HTTP/1.1 200 OK
Location: /onapi/2.4/orders/f3f26446f6e8407aae876ea8e52d7417
Content-Type: application/json
```

```JSON
[
  {
    "path": "/onapi/2.4/orders/f3f26446f6e8407aae876ea8e52d7417",
    "accessId": "8732c2f065e2490babce820e94b1011a",
    "coSubscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
    "service": "BB-1000-100",
    "operation": "ACTIVATE",
    "state": "RECEIVED",
    "forcedTakeover": false,
    "equipment": [
      {
        "vendorId": "ACME-ROUTER",
        "macAddress": "AA:BB:CC:11:22:33"
      }
    ],
    "spReference": "a6cc5da980034948ba654ae6ceda03f4",
    "spSubscriptionId": "d02925f0083b4f64993b365accfbb1ac",
    "requestedDateTime": "2019-02-05T00:00:00Z",
    "expectedCompletionDate": "2019-02-05T00:00:01Z",
    "characteristics": {
      "fixedIp": true,
      "ipaddress": [
        "1.2.3.4/32"
      ],
      "SLA": "SLA-3"
    }
  }
]
```

#### Get a single order

Request
```HTTP
GET /onapi/2.4/orders/8732c2f065e2490babce820e94b1011a HTTP/1.1
```

Response
```HTTP
HTTP/1.1 200 OK
Location: /onapi/2.4/orders/f3f26446f6e8407aae876ea8e52d7417
Content-Type: application/json
```

```JSON
{
  "path": "/onapi/2.4/orders/f3f26446f6e8407aae876ea8e52d7417",
  "accessId": "8732c2f065e2490babce820e94b1011a",
  "coSubscriptionId" : "35738e19ab534dff9f9becb3a064a7d5",
  "service": "BB-1000-100",
  "operation": "ACTIVATE",
  "state": "RECEIVED",
  "forcedTakeover": false,
  "equipment": [
    {
      "vendorId": "ACME-ROUTER",
      "macAddress": "AA:BB:CC:11:22:33"
    }
  ],
  "spReference": "a6cc5da980034948ba654ae6ceda03f4",
  "spSubscriptionId": "d02925f0083b4f64993b365accfbb1ac",
  "requestedDateTime": "2019-02-05T00:00:00Z",
  "expectedCompletionDate": "2019-02-05T00:00:01Z",
  "characteristics": {
    "fixedIp": true,
    "ipaddress": [
      "1.2.3.4/32"
    ],
    "SLA": "SLA-3"
  }
}
```

### POST 

Used to place a new order

#### Activate a service 

Request
```HTTP
POST /onapi/2.4/orders/ HTTP/1.1
Content-Type: application/json
```

```JSON
{
  "accessId": "8732c2f065e2490babce820e94b1011a",
  "service": "BB-1000-100",
  "operation": "ACTIVATE",
  "forcedTakeover": false,
  "equipment": [
    {
      "vendorId": "ACME-ROUTER",
      "macAddress": "AA:BB:CC:11:22:33"
    }
  ],
  "spReference": "a6cc5da980034948ba654ae6ceda03f4",
  "spSubscriptionId": "d02925f0083b4f64993b365accfbb1ac",
  "requestedDateTime": "2019-02-05T00:00:00Z",
  "characteristics": {
    "fixedIp": true,
    "ipaddress": [
      "1.2.3.4/32"
    ],
    "SLA": "SLA-3"
  }
}
```

Response

```HTTP
HTTP/1.1 201 CREATED
Location: /onapi/2.4/orders/f3f26446f6e8407aae876ea8e52d7417
Content-Type: application/json
```

```JSON
{
  "path": "/onapi/2.4/orders/f3f26446f6e8407aae876ea8e52d7417",
  "accessId": "8732c2f065e2490babce820e94b1011a",
  "coSubscriptionId" : "35738e19ab534dff9f9becb3a064a7d5",
  "service": "BB-1000-100",
  "operation": "ACTIVATE",
  "state": "RECEIVED",
  "forcedTakeover": false,
  "equipment": [
    {
      "vendorId": "ACME-ROUTER",
      "macAddress": "AA:BB:CC:11:22:33"
    }
  ],
  "spReference": "a6cc5da980034948ba654ae6ceda03f4",
  "spSubscriptionId": "d02925f0083b4f64993b365accfbb1ac",
  "requestedDateTime": "2019-02-05T00:00:00Z",
  "expectedCompletionDate": "2019-02-05T00:00:01Z",
  "characteristics": {
    "fixedIp": true,
    "ipaddress": [
      "1.2.3.4/32"
    ],
    "SLA": "SLA-3"
  }
}
```

#### Suspend a service 


Request
```HTTP
POST /onapi/2.4/orders/ HTTP/1.1
Content-Type: application/json
```

```JSON
{
  "accessId": "STTA0001",
  "service": "BB-1000-100",
  "operation": "SUSPEND",
  "coSubscriptionId" : "35738e19ab534dff9f9becb3a064a7d5",
  "forcedTakeover": false,
  "equipment": [
    {
      "vendorId": "ACME-ROUTER",
      "macAddress": "AA:BB:CC:11:22:33"
    }
  ],
  "spReference": "a6cc5da980034948ba654ae6ceda03f4",
  "spSubscriptionId": "d02925f0083b4f64993b365accfbb1ac",
  "characteristics": {
    "fixedIp": true,
    "ipaddress": [
      "1.2.3.4/32"
    ],
    "SLA": "SLA-3"
  }
}
```

Response

```HTTP
HTTP/1.1 201 CREATED
Location: /onapi/2.4/orders/f3f26446f6e8407aae876ea8e52d7417
Content-Type: application/json
```

```JSON
{
  "path": "/onapi/2.4/orders/f3f26446f6e8407aae876ea8e52d7417",
  "accessId": "8732c2f065e2490babce820e94b1011a",
  "coSubscriptionId" : "35738e19ab534dff9f9becb3a064a7d5",
  "service": "BB-1000-100",
  "operation": "SUSPEND",
  "state": "DONE_SUCCESS",
  "forcedTakeover": false,
  "equipment": [
    {
      "vendorId": "ACME-ROUTER",
      "macAddress": "AA:BB:CC:11:22:33"
    }
  ],
  "spReference": "a6cc5da980034948ba654ae6ceda03f4",
  "spSubscriptionId": "d02925f0083b4f64993b365accfbb1ac",
  "characteristics": {
    "fixedIp": true,
    "ipaddress": [
      "1.2.3.4/32"
    ],
    "SLA": "SLA-3"
  }
}
```



### PUT
Used to update an order for which the requestedDateTime have not yet passed. 

Request
```HTTP
PUT /onapi/2.4/orders/f3f26446f6e8407aae876ea8e52d7417 HTTP/1.1
Content-Type: application/json
```

```JSON
{
  "accessId": "8732c2f065e2490babce820e94b1011a",
  "coSubscriptionId" : "35738e19ab534dff9f9becb3a064a7d5",
  "service": "BB-1000-100",
  "operation": "ACTIVATE",
  "forcedTakeover": false,
  "equipment": [
    {
      "vendorId": "ACME-ROUTER",
      "macAddress": "AA:BB:CC:11:22:33"
    }
  ],
  "spReference": "a6cc5da980034948ba654ae6ceda03f4",
  "spSubscriptionId": "d02925f0083b4f64993b365accfbb1ac",
  "requestedDateTime": "2019-02-05T00:00:00Z",
  "expectedCompletionDate": "2019-02-05T00:00:01Z",
  "characteristics": {
    "fixedIp": true,
    "ipaddress": [
      "1.2.3.4/32"
    ],
    "SLA": "SLA-3"
  }
}
```

### PATCH
With patch it is possible to update an order for which the requestedDateTime have not yet passed with only partial order
data. 

Request
```HTTP
PUT /onapi/2.4/orders/f3f26446f6e8407aae876ea8e52d7417 HTTP/1.1
Content-Type: application/json
```

```JSON
{
  "requestedDateTime": "2019-02-06T00:00:00Z"
}
```

Response 
```HTTP
HTTP/1.1 204 No Content
```

### DELETE
Used to cancel and order for which the requestedDateTime have not yet passed.

Request
```HTTP
DELETE /onapi/2.4/orders/f3f26446f6e8407aae876ea8e52d7417 HTTP/1.1
```

Response
```HTTP
HTTP/1.1 204 No Content
```

## Fields 

### accessId
 * Data format: ID
 * Mandatory

 This field is a reference to accessId in the [accesses](accesses.md) API

### service
 * Data format: text
 * Mandatory
 
The technical service offered by the CO. Listed in the [accesses](accesses.md) API

### operation 

The type of operation this order is intended to perform.

* Data format: enumeration

**Values**
  * ACTIVATE
    * Activate a service
    * Creates a new subscription or active service
  * DEACTIVATE
    * Deactivate the service
    * Remove the subscription
  * SUSPEND
    * Requires COSubscriptionId
    * Temporary suspend the service
  * RESUME
    * Requires COSubscriptionId
    * Resume a temporary suspended service
  * MODIFY
    * Requires COSubscriptionId
    * Update a service with new parameters
  * CHANGE
    * Requires COSubscriptionId
    * Change the current service type to a new service type

### requestedDateTime

Earliest date and time for the order to be executed. If omitted the order is executed immediately. 

 * Data format: dateTime

### expectedCompletionDate

The date and time when the order is expected to be delivered. This is an estimated time.

 * Data format: dateTime
 * Response only
 
### spReference

 * Data format: ID
 * Mandatory
 
### spSubscriptionId

 * Data format: ID
 * Optional
 
### coSubscriptionId

 * Data format: ID
 * Required for the operations SUSPEND, RESUME, MODIFY and CHANGE
 * Mandatory in response

### note
Note that is formatted in such a way that it can be displayed to the end customer. Is used to inform the end customer
of things like abuse blocks, requirements about agreements with the CO or delayed deliveries or service.

 * Data format: text

### characteristics
Additional settings for the service.

 * Data format: object

### characteristics/fixedIp
Indicates if a fixedIp is to be used. If the ipAddresses characteristic is provided the specified IP-addresses will be 
used. If ipAddresses is omitted the CO reserves an IP-address from a predefined pool.

Data format: boolean

### characteristics/ipAddresses

Fälttyp: array of IP-addresses to be used.

```JSON
{
    "characteristics": {
        "fixedIp": true,
        "ipAddresses": [
            "1.2.3.4/32",
            "AB::01/64",
            "1.3.0.1/24"
        ]
    }
}
```

### characteristics/SLA
SLA type to be used for the service. 

Data format: text

```JSON
{
    "characteristics": {
        "SLA": "premium"
    }
}

```

### forcedtakeover
If the SP wishes to replace the service from another SP this value is set to true. This is only possible if the 
acccesses API responds with forcedTakeoverPossible: true for the service to be activated. If forcedTakeoverPossible is 
false this field must be omitted or be set to false.

 * Data format: boolean
 * Optional for operation "ACTIVATE"
 
### equipment

List of equipment which is used to deliver the specified service. This can be used to tie the service to specific 
equipment, such as VOIP or IPTV-equipment. 

 * Data format: array of key value pairs

**Keys**
 * vendorId
   * Dataformat: text
   * Specifies the DHCP Option 60 Vendor class identifier 
   * See [RFC 2132](https://www.ietf.org/rfc/rfc2132.txt)

 * macAddress
   * Dataformat: MAC
   * Specifies the equipments MAC-address
