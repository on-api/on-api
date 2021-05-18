# Order Notice

This API is intended to be used to notify the SP that the CO has activated a new SP product offering and corresponding
CO transmission product. It is not possible to reject a subscription through this API. To disconnect a subscription that
is unwanted, a DEACTIVATE order needs to be sent through the CO order API.

The purpose of this API is to support integration paths used historically where the CO or external portal activates the
CO transmission products and then notifies the SP, commonly via email. This API provides a more structured way to handle
this in an automatic approach. This API allows exchanging subscription and customer references automatically.

## Usage

The CO or external portal captures the order details on a given access, including selected product offering and customer
information, and places an activation order to the CO. As part of handling the order, the CO or external portal sends an
activation notice to the SP. The SP receives and validates the order, but is unable to reject the order directly in the
response. If the order is unwanted, the SP must instead handle this through the CO order API. If order is OK, the SP may
respond back with subscription and customer references.

## Request

```http
POST activationnotice/ HTTP/1.1
Content-Type: application/json
```

```json
{
  "coOrderId": "f3f26446f6e8407aae876ea8e52d7417",
  "coAccessId": "8732c2f065e2490babce820e94b1011a",
  "operation": "ACTIVATE",
  "orderDateTime": "2021-05-03T20:31:15Z",
  "requestedDateTime": "2021-05-06T00:01:00Z",
  "products": [
    {
      "productId": "8732c2f065e2490babce820e94b1011a",
      "offeringId": "8732c2f065e2490babce820e94b1011a",
      "coProduct": "100/10",
      "coSubscriptionId": "35738e19ab534dff9f9becb3a064a7d5"
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

## coOrderId

The unique Id of the order on the CO side.

* Data format: [id](../common/dataformats.md#id)
* Optional

## coAccessId

Identifies a single access in the CO population in the accesses API.

* Data format: [accessId](../common/dataformats.md#accessid)
* Mandatory

### operation

The type of operation this order is intended to perform.

* Data format: [enumeration](../common/dataformats.md#enumeration)
* Mandatory
* Only ACTIVATE is currently supported

## orderDateTime

Requested date and time when the order was created in the CO system

* Data format: [dateTime](../common/dataformats.md#datetime)
* Mandatory

## requestedDateTime

Requested date and time for the order to be executed.

* Data format: [dateTime](../common/dataformats.md#datetime)
* Mandatory

## products

List of SP products and associated offerings. The model supports multiple activations for future extension, but
currently only allows a single product offering.

### products.productId

The unique Id of the base product provided by the SP. This Id identifies a unique product offering together with
products.offeringId.

* Data format: [id](../common/dataformats.md#id)
* Mandatory

### products.offeringId

The Id of the product offering provided by the SP. This Id identifies a unique product offering together with
products.productId.

* Data format: [id](../common/dataformats.md#id)
* Mandatory

### products.coProduct

The CO product that the CO has matched to the SP product and offering and that will be activated as a result of this
order. It is recommended that the SP validates that this match is correct.

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

An empty response with http code 200 is considered a successful transaction.

```http
HTTP/1.1 200 OK Content-Type: application/json
```

Error handling according to [common responses](../common/responses.md)
