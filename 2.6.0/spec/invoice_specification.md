# Invoice specification

 * Endpoint /onapi/2.6/invoicespecification/

This endpoint aims to provide the service provider (SP) with a specification of each billing item, this enables the SP 
to follow up and verify the invoice and correct service delivery.

This specification is the master and makes the previous specification (TLF_Faktura-specifikation-2018-02-23_final) obsolete.

### Excel option
The response may be implemented in CO Software systems to allow an Excel export option. The Excel should then follow the field specification below replacing forward slash (/) with dot (.).
Example: The column for the Access AccessID should be named "access.accessID".


## Methods

GET without a key lists all available invoice-specification periods.

### GET

```HTTP
GET /onapi/2.6/invoicespecification/ HTTP/1.1
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

#### Single invoice

A GET operation with an `id` from the previous list operation as key fetches the specification for that invoice.

```HTTP
GET /onapi/2.6/invoicespecification/{id} HTTP/1.1
```

Response
```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```

```JSON
[
    {
        "coId": "Somecity-net",
        "spName": "Acme",
        "access": {
            "accessId": "6748f377-0d01-49f9-ae62-f18c3a4f719b",
            "streetName": "Some street",
            "streetNumber": "6",
            "streetLittera": "A",
            "postalCode": "12345",
            "city": "Somecity",
            "countryCode": "SE",
            "mduApartmentNumber": 1012,
            "mduDistinguisher": "apartment 15",
            "outlet": "ABC123",
            "population": "Test population",
            "premisesType": "RESIDENTIAL_HOUSE",
            "priceGroup": "0"
        },
        "subscription": {
            "service": "Acme 100/10",
            "connectionDate": "2019-01-03",
            "disconnectionDate": "2019-01-03",
            "spReference": "5d014d56-e86e-4ffc-bdaf-4aaab9a4f4f1",
            "spSubscriptionId": "160c777f-554e-48e9-a990-4cbace468d7d",
            "coSubscriptionId": "ea3d28c0-8ab5-4c2b-81c1-4ec9f57fc3e3"
        },
        "invoice": {
            "listPrice": "0",
            "billingItem": "Acme 100/10",
            "invoiceType": "DEBIT",
            "rowType": "PERIODIC_FEE",
            "fromDate": "2019-01-03",
            "toDate": "2019-01-03",
            "invoicedAmount": "200"
        }
    },
    {
        "coId": "Somecity-net",
        "spName": "Acme",
        "access": {
            "accessId": "8e81db10-f10a-430f-9bac-ec361306d809",
            "streetName": "Some street",
            "streetNumber": "7",
            "streetLittera": "",
            "postalCode": "12345",
            "city": "Somecity",
            "countryCode": "SE",
            "mduApartmentNumber": "",
            "mduDistinguisher": "",
            "outlet": "",
            "population": "Test population",
            "premisesType": "RESIDENTIAL_HOUSE",
            "priceGroup": "1"
        },
        "subscription": {
            "service": "Acme 100/10",
            "connectionDate": "2019-01-03",
            "disconnectionDate": "2019-01-03",
            "spReference": "2fce9449-44c2-4b2d-9c8c-e8a50bacd77c",
            "spSubscriptionId": "7dcb8a94-76b1-412b-a60a-0e8066fb6bf2",
            "coSubscriptionId": "f854141e-6f46-453a-9586-ef670153784c"
        },
        "invoice": {
            "listPrice": "0",
            "billingItem": "Acme 100/10",
            "invoiceType": "CREDIT",
            "rowType": "PERIODIC_FEE",
            "fromDate": "2019-01-03",
            "toDate": "2019-01-03",
            "invoicedAmount": "-100",
            "comment": "Credit due to wrong port connected"
        }
    }
]
```

## Fields

General rules:

 * Null is not a valid value for any field
 * Mandatory fields cannot be empty string ("")

### coId

Name of the current CO.

 * Data format: [text](../common/dataformats.md#text)
 * Mandatory

 ### spName

Name of the SP the specification is generated for.

 * Data format: [text](../common/dataformats.md#text)
 * Mandatory


### access 

Information about the current access.
Note: All child objects are defined and specified in the [accesses](accesses.md) endpoint and must follow data formats defined there.

 * Data format: JSON array of JSON objects. 
 * Mandatory

#### access/accessId
 * Mandatory

#### access/streetName
 * Mandatory

#### access/streetNumber
 * Optional

#### access/streetLittera
 * Optional
 
#### access/postalCode
 * Mandatory
  
#### access/city
 * Mandatory
 
#### access/countryCode
 * Mandatory

#### access/mduApartmentNumber
 * Mandatory if premisesType is set to MDU_APARTMENT and mduDistinguisher is omitted

#### access/mduDistinguisher
 * Mandatory if premisesType is set to MDU_APARTMENT and mduApartmentNumber is omitted

#### access/outlet
 * Optional

#### access/population
 * Optional

#### access/premisesType
 * Mandatory

#### access/priceGroup
 * Mandatory


### subscription 

Information about the current subscription.
Note: All child objects are defined and specified in the [subscriptions](subscriptions.md) endpoint and must follow data formats defined there.

 * Data format: JSON array of JSON objects. 
 * Mandatory

#### subscription/service
 * Mandatory

#### subscription/connectionDate
 * Mandatory

#### subscription/disconnectionDate
 * Mandatory if disconnection date is set.

#### subscription/spReference
 * Mandatory if value exists.

#### subscription/spSubscriptionId
 * Mandatory if value exists.

#### subscription/coSubscriptionId
 * Mandatory


### invoice 

Information about the current subscription's invoice items.

 * Data format: JSON array of JSON objects. 
 * Mandatory

#### invoice/listPrice

The standard price fot the item.

 * Data format: [number](../common/dataformats.md#number)
 * Mandatory

#### invoice/billingItem

Invoiced transmission product name.

 * Data format: [text](../common/dataformats.md#text)
 * Mandatory

#### invoice/invoiceType

An enumeration of the type the current invoice item.

 * Data format: [enumeration](../common/dataformats.md#enumeration)
 * Mandatory
 
**Valid values**
| Enumeration Value | Specification |
|---------------------------------|-------------------------------|
| DEBIT | Normal invoice row |
| CREDIT | Credit invoice row. Should be used with a specification in Comment |

#### invoice/rowType

An enumeration of the type of fee for the current invoice item.

 * Data format: [enumeration](../common/dataformats.md#enumeration)
 * Mandatory
 
**Valid values**
| Enumeration Value | Specification |
|---------------------------------|-------------------------------|
| PERIODIC_FEE | Normal (standard) periodic fee |
| PARTIAL_PERIODIC_FEE | Used when a the invoiced period is less than a full invoice period or when listPrice has changed during the period |
| USAGE_FEE | Periodic fee for metered subscriptions |
| TRANSMISSION_FEE | Periodic transmission (fixed) fee |
| START_FEE | One time start fee |
| UPGRADE_FEE | One time upgrade fee |
| DOWNGRADE_FEE | One time downgrade fee |
| MOVE_FEE | One time move fee |
| END_FEE | One time end/termination fee |
| TROUBLESHOOTING_FEE | One time troubleshooting fee |
| OTHER | Other fees not matching any of the above. Should be used with a specification in Comment |

#### invoice/fromDate

Transmission product invoiced from this date.

 * Data format: [date](../common/dataformats.md#date)
 * Mandatory

#### invoice/toDate

Transmission product invoiced to this date.

 * Data format: [date](../common/dataformats.md#date)
 * Mandatory


#### invoice/invoicedAmount

The calculated sum for the specific transmission product, rowType and dates that CO intends to invoice SP.
If positive number then it is a debit sum.
If negative number then it is a credit sum.
 
 * Data format: [number](../common/dataformats.md#number)
 * Mandatory

#### invoice/comment

Free text comment. Should be used with invoiceType CREDIT and for rowType OTHER.

 * Data format: [text](../common/dataformats.md#text)
 * Optional