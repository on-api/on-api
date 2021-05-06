# CO Order

This API is intended to be used by CO that connects the transmission service when the order is approved by SP.

```json
{
  "coOrderId": "f3f26446f6e8407aae876ea8e52d7417",
  "coAccessId": "8732c2f065e2490babce820e94b1011a",
  "operation": "ACTIVATE",
  "state": "AWAITING_CONFIRMATION",
  "requestedDateTime": "2019-02-05T00:00:00Z",
  "products": [
    {
      "spProductOfferingId": "8732c2f065e2490babce820e94b1011a",
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
      "apartmentNumber": "string",
      "postalCode": "string",
      "city": "string"
    }
  }
}
```

HTTP/1.1 200 OK Content-Type: application/json

```json
{
  "state": "CONFIRMED",
  "externalNote": "Thanks for ordering",
  "spReference": "a6cc5da980034948ba654ae6ceda03f4",
  "products": [
    {
      "spProductOfferingId": "35738e19ab534dff9f9becb3a064a7d5",
      "spSubscriptionId": "d02925f0083b4f64993b365accfbb1ac"
    }
  ]
}
```