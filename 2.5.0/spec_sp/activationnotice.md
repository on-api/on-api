# Activation Notice

This API is intended to be used to notify the SP that the CO has activated a new SP product offering and corresponding CO transmission product. It is not possible to reject a subscription through this API. To disconnect a subscription that is unwanted, a DEACTIVATE order needs to be sent through the CO order API.

The purpose of this API is to support integration paths used historically where the CO or external portal activates the CO transmission products and then notifies the SP, commonly via email. This API provides a more structured way to handle this in an automatic approach. This API allows exchanging subscription and customer references automatically.

## Usage

The CO or external portal captures the order details on a given access, including selected product offering and customer information, and places an activation order to the CO. As part of handling the order, the CO or external portal sends an activation notice to the SP. The SP receives and validates the order, but is unable to reject the order directly in the response. If the order is unwanted, the SP must instead handle this through the CO order API. If order is OK, the SP may respond back with subscription and customer references.

```json
{
  "coId": "Acme",
  "coOrderId": "c70f880e-c1d1-4d6a-910d-f484a6bcf27c",
  "coAccessId": "3d663ca5-9020-415c-9412-53282b168738",
  "orderDateTime": "2021-05-03T20:31:15Z",
  "requestedDateTime": "2021-05-06T00:01:00Z",
  "products": [
    {
      "productId": "1f94f25b-3ae0-434f-a49e-bc4d3093e399",
      "offeringId": "821cfc90-762a-4272-aacf-ba7ffed8614c",
      "coProduct": "100/100",
      "coSubscriptionId": "2e450f9b-b1ca-4300-b8a2-451f007af85f"      
    }
  ],
  "customerDetails": {
    "identifiedCustomer": true,
    "personalIdentityNumber": "string",
    "customerFirstname": "string",
    "customerLastName": "string",
    "customerPhone": "string",
    "customerMobilePhone": "string",
    "customerEmail": "string",
    "invoiceDetails": {
      "streetName": "string",
      "streetNumber": "string",
      "streetLittera": "string",
      "postalCode": "string",
      "city": "string"
    }
  }
}
```

```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
  "spReference": "f3ae2df8-40ae-4cb5-9b52-c9c1dd32020d",
  "products": [
    {
      "productId": "1f94f25b-3ae0-434f-a49e-bc4d3093e399",
      "offeringId": "821cfc90-762a-4272-aacf-ba7ffed8614c",
      "spSubscriptionId": "d02925f0083b4f64993b365accfbb1ac"
    }
  ]
}
```
## coId

The unique Id of the CO network that this notification is made from.

 * Data format: [id](../common/dataformats.md#id)
 * Optional

## coOrderId

The unique Id of the order on the CO side.

 * Data format: [id](../common/dataformats.md#id)
 * Optional

## coAccessId

Identifies a single access in the CO population in the accesses API.

 * Data format: [accessId](../common/dataformats.md#accessid)
 * Mandatory

## orderDateTime

Requested date and time when the order was created in the CO system

* Data format: [dateTime](../common/dataformats.md#datetime)
* Mandatory

## requestedDateTime

Requested date and time for the order to be executed.

* Data format: [dateTime](../common/dataformats.md#datetime)
* Mandatory

## products

List of SP products and associated offerings. The model supports multiple activations for future extension, but currently only allows a single product offering.

### products.productId

The unique Id of the base product provided by the SP. This Id identifies a unique product offering together with products.offeringId.

 * Data format: [id](../common/dataformats.md#id)
 * Mandatory

### products.offeringId

The Id of the product offering provided by the SP. This Id identifies a unique product offering together with products.productId.

 * Data format: [id](../common/dataformats.md#id)
 * Mandatory

### products.coProduct

The CO product that the CO has matched to the SP product and offering and that will be activated as a result of this order. It is recommended that the SP validates that this match is correct.

 * Data format: JSON array of [text](../common/dataformats.md#text)
 * Mandatory

### products.coSubscriptionId

Reference to the subscription on CO side.

* Data format: [subscriptionId](../common/dataformats.md#subscriptionid)
* Mandatory

## customerDetails

Customer details provided by the CO. This information should be validated by the SP.

* Data format: [customerdetails](../common/dataformats.md#customerdetails)
* Mandatory

## Response

### cause

Message that is intended for the CO only. Can always be provided for logging purposes.

### spReference

The unique reference to the customer on the SP side

* Data format: [spReference](../common/dataformats.md#spreference)
* Optional

### products

Used in response to exchange spSubscriptionId for activated subscriptions

* Optional

#### products.spSubscriptionId

The unique reference to the subscription on the SP side

* Data format: [spSubscriptionId](../common/dataformats.md#spsubscriptionid)
* Optional

# Responses

Error handling should use HTTP status codes, and optionally set the "cause" field to communicate what went wrong. If the server has an Id of the error (such as a fault number or, even better, a ticket Id) it should be included in the cause field. 

Status 200 should always be returned as long as the order message itself is correct, mandatory fields are supplied, and the message can be parsed and handled in a managed way.

It is recommended that the CO logs any error messages presented in the cause fields, so that the issue can be handled and resolved. The CO and the SP have a common responsibility for catching and resolving activation notices that either part where unable to handle outside the flow of this API.

Example (whoops, something went wrong):

```http
HTTP/1.1 500 Internal Server Error
Content-Type: application/json

{ "cause": "Unknown error has occured. Error number 12345." }
```

## HTTP status codes used (for full list, see RFC7231)

### 400 Bad request

Invalid data posted

### 401 Unauthorized

Invalid credentials

### 403 Forbidden

Not allowed with current credentials

### 404 Not found

Object not found (on valid API endpoint)

### 409 Conflict

Object is conflicting with other object (on valid API endpoint).

### 429 Too Many Requests

The client is sending too many requests to the server in too short time. If Retry-After is used in the response the
client should honor that time before sending any more requests.

### 500 Internal Server Error

Unrecoverable error

### 501 Not implemented

Response for unknown or unimplemented API endpoints
