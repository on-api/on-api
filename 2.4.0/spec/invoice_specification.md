# Invoice specification

 * Endpoint /2.4/invoicespecification/

This endpoint aims to provide the service provider (SP) with a specification of each billing item, this enables the SP 
to follow up and verify the invoice and correct service delivery.

The JSON format includes the fields specified in TLF_Faktura-specifikation-2018-02-23_final. 
See [Fields](invoice_specification.md#fields) for references between the different formats.

## Methods

GET without a key lists all available invoice-specification periods.

### GET

```HTTP
GET /onapi/2.4/invoicespecification/ HTTP/1.1
```

Response
```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```

```JSON
[
  {
    "id": "201811",
    "fromDate": "2018-11-01",
    "toDate": "2018-11-30"
  },
  {
    "id": "201812",
    "fromDate": "2018-12-01",
    "toDate": "2018-12-31"
  },
  {
    "id": "201901",
    "fromDate": "2019-01-01",
    "toDate": "2019-01-31"
  }
]
```

A GET operation with a id from the previous list operation as key fetches the specification that invoice.

```HTTP
GET /onapi/2.4/invoicespecification/201901 HTTP/1.1
```

Response
```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```

```JSON
[
    {
        "coID": "Somecity-net",
        "serviceProvider": {
            "name": "Acme"
        },
        "address": {
            "accessID": "6748f377-0d01-49f9-ae62-f18c3a4f719b",
            "streetName": "Some street",
            "streetNumber": "6",
            "streetLittera": "A",
            "postalCode": "12345",
            "city": "Somecity",
            "apartmentNumber": 1012,
            "apartmentAddress": "apartment 15",
            "apartmentOutlet": "ABC123"
        },
        "subscription": {
            "serviceName": "Acme 100/10",
            "connectionDate": "2019-01-03",
            "disconnectionDate": "2019-01-03",
            "spReference": "5d014d56-e86e-4ffc-bdaf-4aaab9a4f4f1",
            "spSubscriptionId": "160c777f-554e-48e9-a990-4cbace468d7d",
            "coSubscriptionId": "ea3d28c0-8ab5-4c2b-81c1-4ec9f57fc3e3"
        },
        "invoice": {
            "listPrice": "0",
            "billingItem": "Acme 100/10",
            "rowType": "PERIODIC_FEE",
            "fromDate": "2019-01-03",
            "toDate": "2019-01-03",
            "creditAmount": "0",
            "invoicedAmount": "0"
        },
        "population": "Test population"
    },
    {
        "coID": "Somecity-net",
        "serviceProvider": {
            "name": "Acme"
        },
        "address": {
            "accessID": "8e81db10-f10a-430f-9bac-ec361306d809",
            "streetName": "Some street",
            "streetNumber": "7",
            "streetLittera": null,
            "postalCode": "12345",
            "city": "Somecity",
            "apartmentNumber": null,
            "apartmentAddress": null,
            "apartmentOutlet": null
        },
        "subscription": {
            "serviceName": "Acme 100/10",
            "connectionDate": "2019-01-03",
            "disconnectionDate": "2019-01-03",
            "spReference": "2fce9449-44c2-4b2d-9c8c-e8a50bacd77c",
            "spSubscriptionId": "7dcb8a94-76b1-412b-a60a-0e8066fb6bf2",
            "coSubscriptionId": "f854141e-6f46-453a-9586-ef670153784c"
        },
        "invoice": {
            "listPrice": "0",
            "billingItem": "Acme 100/10",
            "rowType": "PERIODIC_FEE",
            "fromDate": "2019-01-03",
            "toDate": "2019-01-03",
            "creditAmount": "0",
            "invoicedAmount": "0"
        },
        "population": "Test population"
    }
]
```

## Fields

| API                             | TLF-specification             | Reference in ON-API                                                |
|---------------------------------|-------------------------------|--------------------------------------------------------------------|
| coID                            | coID                          |                                                                    |
| serviceProvider/name            | Service Provider:Name         |                                                                    |
| address/accessID                | Address: accessID             | [accesses/accessId](accesses.md#accessid)                          |
| address/streetName              | Address: Street Name          | [accesses/streetName](accesses.md#streetname)                      |
| address/streetNumber            | Address: Street Number        | [accesses/streetNumber](accesses.md#streetnumber)                  |
| address/streetLittera           | Address: Street Littera       | [accesses/streetLittera](accesses.md#streetlittera)                |
| address/postalCode              | Address: Postal Code          | [accesses/postalCode](accesses.md#postalcode)                      |
| address/city                    | Address: City                 | [accesses/city](accesses.md#city)                                  |
| address/apartmentNumber         | Address: Apartment number     | [accesses/apartmentNumber](accesses.md#mduapartmentnumber)         |
| address/apartmentAddress        | Address: Apartment address    | [accesses/streetName](accesses.md#streetname)                      |
| address/apartmentOutlet         | Address: Apartment outlet     | [accesses/streetName](accesses.md#streetname)                      |
| subscription/serviceName        | Service: Service Name         | [subscription/service](subscriptions.md#service)                   |
| subscription/serviceDescription | Service: Service Description  |                                                                    |
| subscription/connectionDate     | Service: Connection Date      |                                                                    |
| subscription/disconnectionDate  | Service: Disconnection Date   |                                                                    |
| subscription/spReference        | Service Provider: referenceID | [spReference](dataformats.md#spreference)                         |
| subscription/spSubscriptionId   | SP: SubscriptionID            | [subscription/spSubscriptionId](subscriptions.md#spsubscriptionid) |
| subscription/coSubscriptionId   |                               | [subscription/subscriptionId](subscriptions.md#subscriptionid)     |
| invoice/listPrice               | Invoice: List price           |                                                                    |
| invoice/billingItem             | Invoice: Billing Item         |                                                                    |
| invoice/rowType                 | Invoice: Row Type             |                                                                    |
| invoice/fromDate                | Invoice: From Date            |                                                                    |
| invoice/toDate                  | Invoice: To Date              |                                                                    |
| invoice/creditAmount            | Invoice: Credit amount        |                                                                    |
| invoice/invoicedAmount          | Invoice: Invoiced amount      |                                                                    |
| population                      | Population                    | [accesses/population](accesses.md#population)                      |


 
 
 
