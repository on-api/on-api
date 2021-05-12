# CO Order

This API is intended to be used by the CO send an order for approval to the SP before connecting the transmission
products.

It is designed to support two main integration paths:

* The CO captures and passes the order details directly to the SP for confirmation before any order is registered (
  coOrderId is not set). The SP is required to send an ACTIVATE order.
* The CO captures and registers an order, and then passes the order details to the SP for approval before allowing the
  order to proceed (coOrderId is set). The SP only needs to confirm or reject the order and should not send an ACTIVATE
  order.

## Usage

The CO captures the order details on a given access, including selected product offering and customer information, and
sends a CO order request to the SP. The SP validates the order and customer and either rejects or confirms the order. If
the order has already been registered by the CO (path 2), the SP does not need to take any further actions. If the order
is not yet registered (path 1), the SP is required to also send an ACTIVATE order. In any case the order will initially
have the status AWAITINGCONFIRMATION. The SP may respond with CONFIRMEDNOTREADY, allowing the SP to stall the order
until a PUT or PATCH operation has been carried out on the order. This allows the SP to complement the order with
additional information, such as characteristics.

Depending on the results, the CO will present relevant feedback to the customer.

#### Place CO order

```http
POST coorder/ HTTP/1.1
Content-Type: application/json
```

```json
{
  "coId": "Acme",
  "coOrderId": "f3f26446f6e8407aae876ea8e52d7417",
  "coAccessId": "3d663ca5-9020-415c-9412-53282b168738",
  "operation": "ACTIVATE",
  "state": "AWAITINGCONFIRMATION",
  "orderDateTime": "2021-05-03T20:31:15Z",
  "requestedDateTime": "2019-02-05T00:00:00Z",
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
      "apartmentNumber": "string",
      "postalCode": "string",
      "city": "string"
    }
  }
}
```

## coOrderId

The unique ID of the order on the CO side. If coOrderId is provided, the SP should never send an ACTIVATE order. If
coOrderId is not provided, the SP is required to send an ACTIVATE order.

* Data format: [id](../common/dataformats.md#id)
* Optional

## coAccessId

Identifies a single access point in the CO population in the accesses API.

* Data format: [accessId](../common/dataformats.md#accessid)
* Mandatory

## operation

The type of operation this order is intended to perform.

* Data format: [enumeration](../common/dataformats.md#enumeration)
* Mandatory
* Only ACTIVATE is currently supported

**Values**

* ACTIVATE
    * Activation of transmission product

## state

The status of the order

* Data format: [enumeration](../common/dataformats.md#enumeration)
* Mandatory
* Initially AWAITINGCONFIRMATION

**Values**

* AWAITINGCONFIRMATION
    * The order is waiting for confirmation
* REJECTED
    * The SP rejects the order
* CONFIRMED
    * The SP confirms the order
* CONFIRMEDNOTREADY
    * The SP confirms the order, but instructs the CO that it is not ready for provisioning and that a PATCH or PUT
      operation can be expected later.

## requestedDateTime

Requested date and time for the order to be executed

* Data format: [dateTime](../common/dataformats.md#datetime)
* Mandatory

## products

List of SP products and associated offerings. The model supports multiple activations for future extension, but
currently only allows a single product offering.

### products.productId

The unique ID of the base product provided by the SP. This ID identifies a unique product offering together with
products.offeringId.

* Data format: [id](../common/dataformats.md#id)
* Mandatory

### products.offeringId

The ID of the product offering provided by the SP. This ID identifies a unique product offering together with
products.productId.

* Data format: [id](../common/dataformats.md#id)
* Mandatory

### products.coProduct

The CO product that the CO has matched to the SP product and offering and that will be activated as a result of this
order. It is recommended that the SP validates that this match is correct.

* Data format: JSON array of [text](../common/dataformats.md#text)
* Optional

### products.coSubscriptionId

Reference to the subscription on CO side. If it is not set, the SP will receive this later when order has been handled.
It may however be required in case coOrderId is set if the susbcription have already been created on the CO side.

* Data format: [subscriptionId](../common/dataformats.md#subscriptionid)
* Optional

## customerDetails

Customer details provided by the CO. This information should be validated by the SP.

* Data format: [customerDetails](../common/dataformats.md#customerdetails)
* Mandatory

# Responses

```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
  "state": "CONFIRMED",
  "externalMessage": "Thanks for ordering. You will receive an email with order confirmation and information about how to get started.",
  "cause": "",
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

### externalMessage

Message that is intended for the customer

### cause

Message that is intended for the CO only. Can always be provided for logging purposes.

### spReference

The unique reference to the customer on the SP side

* Data format: [spReference](../common/dataformats.md#spreference)
* Mandatory if state is CONFIRMED

#### products.spSubscriptionId

The unique reference to the subscription on the SP side

* Data format: [spSubscriptionId](../common/dataformats.md#spsubscriptionid)
* Mandatory if state is CONFIRMED

Error handling should use HTTP status codes, and optionally set the "cause" field to communicate what went wrong. If the
server has an ID of the error (such as a fault number or, even better, a ticket ID) it should be included in the cause
field. The message included in the "cause" field must never be displayed to the customer, but it may be logged on the CO
system.

Anything else than status 200 will result in an immediate cancellation of the order, and only the "cause" field is
allowed. This should be seen as an exception, and a generic error message should be presented for the customer.

Status 200 should always be returned as long as the order message itself is correct, mandatory fields are supplied, and
the message can be parsed and handled in a managed way, and there is nothing specific in the error that is not suitable
to present to the customer.

For instance, if there are any mandatory information missing in the customer details that the order capture portal would
be assumed to validate and prevent, this should result in status 400. On the other hand, if the customer cannot be
accepted because the credit check fails, this should be communicated to the customer in an informative way.

Example 1 (invalid data):

```http
HTTP/1.1 400 Bad Request
Content-Type: application/json
```

```json
{
  "cause": "Invalid offeringId: bf134676-0830-4d61-8af0-94f00a0270da"
}
```

Example 2 (whoops, something went wrong):

```http
HTTP/1.1 500 Internal Server Error
Content-Type: application/json
```

```json
{
  "cause": "Unknown error has occurred. Error number 12345."
}
```

Example 3 (offering not available):

```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
  "state": "REJECTED",
  "externalMessage": "We are sorry, but the selected offering is no longer available on your location. Please contact us for more information and alternatives."
}
```

Error handling according to [common responses](../common/responses.md)
