# Orders

* Endpoint /onapi/2.6/orders/

This endpoint allows the service provider to activate, deactivate, suspend, resume, update and change services. Once an order
is no longer in the state "RECEIVED" no changes can be made to that order.

## States

In the simplest implementation an order goes directly to DONE_SUCCESS or DONE_FAILED depending on if it is accepted or
not. If an order goes to a queue it ends up in RECEIVED. If an order is RECEIVED changes can be made to it until it
changes state. An order that is RECEIVED can also have the status checked and during processing the status can be
IN_PROGRESS before reaching DONE_SUCCESS or DONE_FAILED.

## Operations

### GET

Used to fetch placed orders.

#### Get all unfinished orders

Request

```HTTP
GET /onapi/2.6/orders/ HTTP/1.1
```

Response

```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```

```JSON
[
  {
    "path": "/onapi/2.6/orders/f3f26446f6e8407aae876ea8e52d7417",
    "orderId": "f3f26446f6e8407aae876ea8e52d7417",
    "accessId": "8732c2f065e2490babce820e94b1011a",
    "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
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
      "ipAddress": [
        "1.2.3.4"
      ],
      "SLA": "SLA-3"
    }
  }
]
```

#### Get all orders pertaining a specific acccessId

Request

```HTTP
GET /onapi/2.6/orders/?accessId={accessId} HTTP/1.1
```

Response

```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```

```JSON
[
  {
    "path": "/onapi/2.6/orders/f3f26446f6e8407aae876ea8e52d7417",
    "orderId": "f3f26446f6e8407aae876ea8e52d7417",
    "accessId": "8732c2f065e2490babce820e94b1011a",
    "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
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
      "ipAddress": [
        "1.2.3.4"
      ],
      "SLA": "SLA-3"
    }
  }
]
```

#### Get all orders with a certain state

Request

```HTTP
GET /onapi/2.6/orders/?state="RECEIVED" HTTP/1.1
```

Response

```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```

```JSON
[
  {
    "path": "/onapi/2.6/orders/f3f26446f6e8407aae876ea8e52d7417",
    "orderId": "f3f26446f6e8407aae876ea8e52d7417",
    "accessId": "8732c2f065e2490babce820e94b1011a",
    "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
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
      "ipAddress": [
        "1.2.3.4"
      ],
      "SLA": "SLA-3"
    }
  }
]
```

#### Get a single order

Request

```HTTP
GET /onapi/2.6/orders/{orderId} HTTP/1.1
```

Response

```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```

```JSON
{
  "path": "/onapi/2.6/orders/f3f26446f6e8407aae876ea8e52d7417",
  "orderId": "f3f26446f6e8407aae876ea8e52d7417",
  "accessId": "8732c2f065e2490babce820e94b1011a",
  "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
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
    "ipAddress": [
      "1.2.3.4"
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
POST /onapi/2.6/orders/ HTTP/1.1
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
    "ipAddress": [
      "1.2.3.4"
    ],
    "SLA": "SLA-3"
  }
}
```

Response

```HTTP
HTTP/1.1 201 CREATED
Location: /onapi/2.6/orders/{orderId}
Content-Type: application/json
```

```JSON
{
  "path": "/onapi/2.6/orders/f3f26446f6e8407aae876ea8e52d7417",
  "orderId": "f3f26446f6e8407aae876ea8e52d7417",
  "accessId": "8732c2f065e2490babce820e94b1011a",
  "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
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
    "ipAddress": [
      "1.2.3.4"
    ],
    "SLA": "SLA-3"
  }
}
```

#### Deactivate a service

Request

```HTTP
POST /onapi/2.6/orders/ HTTP/1.1
Content-Type: application/json
```

```JSON
{
  "operation": "DEACTIVATE",
  "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
  "requestedDateTime": "2019-02-05T00:00:00Z"
}
```

Response

```HTTP
HTTP/1.1 201 CREATED
Location: /onapi/2.6/orders/{orderId}
Content-Type: application/json
```

```JSON
{
  "path": "/onapi/2.6/orders/0e5152dbbe424fb0b82e7ab177ed4ab1",
  "orderId": "0e5152dbbe424fb0b82e7ab177ed4ab1",
  "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
  "operation": "DEACTIVATE",
  "state": "RECEIVED",
  "expectedCompletionDate": "2019-02-05T00:00:01Z"
}
```

#### Change service

Request

```HTTP
POST /onapi/2.6/orders/ HTTP/1.1
Content-Type: application/json
```

```JSON
{
  "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
  "operation": "CHANGE",
  "service": "BB-1000-1000"
}
```

Response

```HTTP
HTTP/1.1 201 CREATED
Location: /onapi/2.6/orders/{orderId}
Content-Type: application/json
```

```JSON
{
  "path": "/onapi/2.6/orders/8883168fb4354a189a164dc9a53522ba",
  "orderId": "8883168fb4354a189a164dc9a53522ba",
  "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
  "service": "BB-1000-1000",
  "operation": "CHANGE",
  "state": "DONE_SUCCESS"
}
```

#### Suspend a service

This operation is for a service that is suspended, for instance for abuse. It's to be used temporarily and billing is
supposed to keep going. A special field "externalNote" is added here, for information the CO may publish to the customer
if possible.

Request

```HTTP
POST /onapi/2.6/orders/ HTTP/1.1
Content-Type: application/json
```

```JSON
{
  "operation": "SUSPEND",
  "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
  "externalNote": "This is the reason I suspend you"
}
```

Response

```HTTP
HTTP/1.1 201 CREATED
Location: /onapi/2.6/orders/{orderId}
Content-Type: application/json
```

```JSON
{
  "path": "/onapi/2.6/orders/e52499d7ea1f4584a71d0a67addfb3aa",
  "orderId": "e52499d7ea1f4584a71d0a67addfb3aa",
  "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
  "operation": "SUSPEND",
  "state": "DONE_SUCCESS",
  "externalNote": "This is the reason I suspend you"
}
```

### Resume a service

This operation is only used to resume a service that is suspended.

Request

```HTTP
POST /onapi/2.6/orders/ HTTP/1.1
Content-Type: application/json
```

```JSON
{
  "operation": "RESUME",
  "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5"
}
```

Response

```HTTP
HTTP/1.1 201 CREATED
Location: /onapi/2.6/orders/{orderId}
Content-Type: application/json
```

```JSON
{
  "path": "/onapi/2.6/orders/bd8ce555ee1d4983bc22fa4ec6937cf6",
  "orderId": "bd8ce555ee1d4983bc22fa4ec6937cf6",
  "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
  "operation": "RESUME",
  "state": "DONE_SUCCESS"
}
```

#### Modify a subscription

Used to modify spReference and/or spSubscriptionId.

Request

```HTTP
POST /onapi/2.6/orders/ HTTP/1.1
Content-Type: application/json
```

```JSON
{
  "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
  "operation": "MODIFY",
  "spReference": "a6cc5da980034948ba654ae6ceda03f4",
  "spSubscriptionId": "d02925f0083b4f64993b365accfbb1ac"
}
```

Response

```HTTP
HTTP/1.1 201 CREATED
Location: /onapi/2.6/orders/{orderId}
Content-Type: application/json
```

```JSON
{
  "path": "/onapi/2.6/orders/64ff212a16dd42c09360a2bc683bfd8a",
  "orderId": "64ff212a16dd42c09360a2bc683bfd8a",
  "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
  "operation": "MODIFY",
  "state": "DONE_SUCCESS",
  "spReference": "a6cc5da980034948ba654ae6ceda03f4",
  "spSubscriptionId": "d02925f0083b4f64993b365accfbb1ac"
}
```

### PUT

With put it is possible to update an order for which the state is "RECEIVED", using the complete object.

Request

```HTTP
PUT /onapi/2.6/orders/{orderId} HTTP/1.1
Content-Type: application/json
```

```JSON
{
  "path": "/onapi/2.6/orders/f3f26446f6e8407aae876ea8e52d7417",
  "orderId": "f3f26446f6e8407aae876ea8e52d7417",
  "accessId": "8732c2f065e2490babce820e94b1011a",
  "subscriptionId": "35738e19ab534dff9f9becb3a064a7d5",
  "service": "BB-100-100",
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
    "ipAddress": [
      "1.2.3.4"
    ],
    "SLA": "SLA-3"
  }
}
```

Response

```HTTP
HTTP/1.1 204 No Content
```

### PATCH

With patch it is possible to update an order for which the state is "RECEIVED", using only the changed part.

Request

```HTTP
PATCH /onapi/2.6/orders/{orderId} HTTP/1.1
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

Used to cancel an order for which the state is "RECEIVED".

Request

```HTTP
DELETE /onapi/2.6/orders/{orderId} HTTP/1.1
```

Response

```HTTP
HTTP/1.1 204 No Content
```

## Fields

### orderId

* Data format: ID
* Required in response
* Key for order

### path

* API path for the specific order
* Required in response
* In response only

### accessId

* Data format: ID
* Required in response

This field is a reference to accessId in the [accesses](accesses.md) API

### service

The technical service offered by the CO. Listed in the [accesses](accesses.md) API

* Data format: [service](../common/dataformats.md#service)
* Required in response

### operation

The type of operation this order is intended to perform.

* Data format: [enumeration](../common/dataformats.md#enumeration)
* Required in request and response

**Values**

* ACTIVATE
    * Activate a service
    * Creates a new subscription or active service
    * Required fields in request
        * [accessId](orders.md#accessid)
        * [service](orders.md#service)
* DEACTIVATE
    * Deactivate the service
    * Remove the subscription
    * Required fields in request
        * [subscriptionId](orders.md#subscriptionid)
* SUSPEND
    * Temporary suspend the service
    * Change subscription state to "SUSPENDED"
    * Required fields in request
        * [subscriptionId](orders.md#subscriptionid)
* RESUME
    * Resume a temporary suspended service
    * Only for subscriptions state from "SUSPENDED" to "ACTIVE"
    * Required fields in request
        * [subscriptionId](orders.md#subscriptionid)
* MODIFY
    * Update a service with new parameters
    * Required fields in request
        * [subscriptionId](orders.md#subscriptionid)
* CHANGE
    * Change the current service to a new service
    * Required fields in request
        * [subscriptionId](orders.md#subscriptionid)
        * [service](orders.md#service)

### requestedDateTime

Earliest date and time for the order to be executed. If date is omitted the order is executed immediately. If a date in
the past is provided (current date is 2019-04-01 and provided date is 2019-03-28) order will be executed immediately.

* Data format: [dateTime](../common/dataformats.md#datetime)
* Required in response, if set

### expectedCompletionDate

The date and time when the order is expected to be delivered. This is an estimated time.

* Data format: [dateTime](../common/dataformats.md#datetime)
* In response, if known

### spReference

* Data format: [spReference](../common/dataformats.md#spreference)
* Required in response, if set

### spSubscriptionId

* Data format: [spSubscriptionId](../common/dataformats.md#spsubscriptionid)
* Required in response, if set

### subscriptionId

* Data format: [subscriptionId](../common/dataformats.md#subscriptionid)
* Required for the operations SUSPEND, RESUME, MODIFY and CHANGE
* Required in response

### externalNote

Note that is formatted in such a way that it can be displayed to the end customer.
* Data format: [text](../common/dataformats.md#text)
* Required in response, if set

Examples:

* Your service have been blocked due to outstanding payment

### characteristics

* Data format: [characteristics](../common/dataformats.md#characteristics)

### forcedTakeover

If the SP wishes to replace the service from another SP this value is set to true. This is only possible if the accesses
API responds with [forcedTakeoverPossible](accesses.md#servicesforcedtakeoverpossible): true for the service to be
activated. If forcedTakeoverPossible is false this field must be omitted or be set to false.

* Data format: boolean
* Optional for operation "ACTIVATE"
* Must be omitted or false if [forcedTakeoverPossible](accesses.md#servicesforcedtakeoverpossible) is false

### equipment

* Data format: [equipment](../common/dataformats.md#equipment)

### state

The state of the order. This is returned from the communication operator.

* Data format: [orderState](../common/dataformats.md#orderstate)

### message

Can be used in the response to describe why the status is DONE_FAILED

* Data format: [text](../common/dataformats.md#text)
* Required (but may be empty)
 