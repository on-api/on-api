# Accesses Endpoint

Path /onapi/2.6/accesses/

The accesses endpoint is used to get available accesses from a CO. The accesses contain details about the address where the 
access resides and equipment. 
  
## Operations

### GET

#### All accesses 
```HTTP
GET /onapi/2.6/accesses/ HTTP/1.1
```

Response 
```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
Last-Modified: Mon, 04 Feb 2019 18:22:33 GMT
```

Response if no available accesses
```HTTP
HTTP/1.1 404 NOT FOUND
Content-Type: application/json
Last-Modified: Mon, 04 Feb 2019 18:22:33 GMT
```

#### Updates

To get changes since the last GET operation include the If-Modified-Since header using the value of the "Last-Modified" 
header from the previous response. 

Request
```HTTP
GET /onapi/2.6/accesses/ HTTP/1.1
If-Modified-Since: Mon, 04 Feb 2019 18:12:33 GMT
```

See [RFC-2616](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) for more details about HTTP-headers.


Array listing one or more accesses. The API response must contain the Last-Modified header when returning one or more 
accesses. 


Response
```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
Last-Modified: Mon, 04 Feb 2019 18:22:33 GMT
```

Response if no updates is available 
```HTTP
HTTP/1.1 304 Not Modified
Content-Type: application/json
```

#### Example from all accesses and updates responses

When all accesses or updates are requested the response contains a JSON-array with JSON-objects. 

```JSON
[
  {
    "accessId": "8732c2f065e2490babce820e94b1011a",
    "legacyAccessId": "KGXF49861",
    "streetName": "Testvägen",
    "streetNumber": "100",
    "streetLittera": "",
    "postalCode": "10000",
    "city": "Ankeborg",
    "countryCode": "SE",
    "premisesType": "MDU_APARTMENT",
    "mduApartmentNumber": "1001",
    "mduDistinguisher": "12121212",
    "outlet": "A-11-14",
    "population": "Hemsöhem",
    "priceGroup": 0,
    "accessState": "CONNECTED",
    "services": [
      {
        "service": "BB-100-100",
        "connectionDateTime": "1970-01-01T00:00:00Z",
        "availableDateTime": "1970-01-01T00:00:00Z",
        "disconnectionDateTime": ""
      },
      {
        "service": "BB-100-10",
        "connectionDateTime": "2013-10-12T14:09:23Z",
        "availableDateTime": "2013-10-12T14:09:23Z",
        "disconnectionDateTime": ""
      },
      {
        "service": "BB-10-10",
        "connectionDateTime": "2013-10-12T14:09:23Z",
        "availableDateTime": "2021-05-31T14:09:24Z",
        "disconnectionDateTime": "2021-05-31T14:09:23Z"
      },
      {
        "service": "IPTV",
        "connectionDateTime": "2013-10-12T14:09:23Z",
        "availableDateTime": "2013-10-12T14:09:23Z",
        "disconnectionDateTime": ""
      },
      {
        "service": "VOIP",
        "connectionDateTime": "2013-10-12T14:09:23Z",
        "availableDateTime": "2013-10-13T14:09:23Z",
        "disconnectionDateTime": ""
      }
    ]
  }
]
```


#### Single access

To get a single access use `accessId` as key. The single access contains details about activated services and the services
 available for activation.
 
Request
```http
GET /onapi/2.6/accesses/{accessId} HTTP/1.1
```

Response 
```HTTP
HTTP/1.1 200 OK
Content-Type: application/json
```
#### Example data from a single access response 

When a single access is requested the response contains a single JSON-object.

```JSON
{
  "accessId": "8732c2f065e2490babce820e94b1011a",
  "legacyAccessId": "KGXF49861",
  "streetName": "Testvägen",
  "streetNumber": "100",
  "streetLittera": "",
  "postalCode": "10000",
  "city": "Ankeborg",
  "countryCode": "SE",
  "premisesType": "MDU_APARTMENT",
  "mduApartmentNumber": "1001",
  "mduDistinguisher": "12121212",
  "outlet": "A-11-14",
  "population": "Hemsöhem",
  "priceGroup": 0,
  "accessState": "CONNECTED",
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
  ],
  "subscriptions": [
    {
      "subscriptionId": "8b2ad40b4ffd45e5b48425f57821a7eb",
      "accessId": "8732c2f065e2490babce820e94b1011a",
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
      "accessId": "8732c2f065e2490babce820e94b1011a",
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

## Fields

Some fields are only available when fetching a single access. These fields are marked with "Available with single access"

 * Null is not a valid value for any field
 * Mandatory fields cannot be empty string ("")

### accessId

Identifies a single access. Used as key when fetching a single access and ordering services.

 * Data format: [accessId](../common/dataformats.md#accessid)
 * Mandatory
 
### legacyAccessId

For accesses that have been migrated from another CO the new CO might have information on what access-id was used for this access by the previous CO. If that information is available it could potentially be quite valuable provided to the SP.

 * Data format: [accessId](../common/dataformats.md#accessid)
 * Optional

### streetName

Street name for the address where the access resides.

 * Data format: [text](../common/dataformats.md#text)
 * Mandatory

### streetNumber

In the example of "Kungsgatan 10G", the street number is "10". In the example of "Lantvägen 550-70", the street number 
is "550-7".

 * Optional
 * Data format: json string
 * Numeric or meter's address
 * Matching regular expression ^(([0-9]+)|([0-9]{1,4}-[0-9]{1,4}))$

See [lantmateriets guide (swedish)](https://www.lantmateriet.se/contentassets/45acf232634c44c1a47c5ebcb7598e07/handbok_adress.pdf) 
for more information on meter's address 

### streetLittera

Street littera or entrance. In the example of "Kungsgatan 10G", the street littera is "G". 

 * Data format: text
 * Optional
 
### postalCode

 * Mandatory
 * Data format: [postalCode](../common/dataformats.md#postalcode)
  
### city

 Postal city

 * Data format: [text](../common/dataformats.md#text) 
 * Mandatory
 
### countryCode

 * Data format: [countryCode](../common/dataformats.md#countrycode)
 * Mandatory

### premisesType

Premises type describes the type of building/premises of the access.

 * Data format: [enumeration](../common/dataformats.md#enumeration)
 * Mandatory
 
**Valid values**
 * COMMERCIAL Offices, stores, municipality buildings
 * MDU_APARTMENT Apartment in a apartment building (multi dwelling unit)
 * MDU_COMMON  Common area in a apartment building (multi dwelling unit)
 * MDU_TECHNICAL Machine room or space intended for technical equipment
 * PUBLIC Location where the public has access
 * RESIDENTIAL_HOUSE Single family house (single dwelling unit)
 * UNKNOWN Unknown, preferably not used

### mduApartmentNumber

Used to distinguish between individual apartments in apartment buildings sharing a single postal address.

 * Data format: JSON number
 * Four digits
 * Matching regexp ^[0-9]{4}$
 * See [Lantmäteriet Apartmentnumber](https://www.lantmateriet.se/en/real-property/Fastighetsinformation/Lagenhetsregistret/apartment-register-content/)
 * Mandatory if premisesType is set to MDU_APARTMENT and mduDistinguisher is omitted

### mduDistinguisher

Alternative to mduApartmentNumber used to distinguish between individual apartments in an apartment building sharing a
single postal address. 

 * Data format: [text](../common/dataformats.md#text)
 * Mandatory if premisesType is set to MDU_APARTMENT and mduApartmentNumber is omitted

### outlet

Used to identify the port in the apartment or house. The port is typically labeled with this value. If specified, 
it should be unique per address.

 * Data format: [text](../common/dataformats.md#text)
 * Optional

### population

Describes a subset of all accesses. Used for grouping accesses together for commercial or technical purposes.

 * Data format: [text](../common/dataformats.md#text)
 * Optional

##### priceGroup

A price group that this access is a part of. The value must be an integer larger or equal to 0 (unsigned integer). 
The exact meaning and associated price list is defined by CO. 

 * Data format: [enumeration](../common/dataformats.md#enumeration)
 * Mandatory 

### accessState

Describes the current state of whether the access is connected and can be used.

 * Data format: One of PLANNED, DEPLOYING, HOMESPASSED, CONNECTED, DISCONNECTED
 * Mandatory

**Valid values**
 * PLANNED The CO is planning to connect the access in the future. The field "connectionDateTime" may reflect the planned date for activation, with some uncertainty (+/- a week).
 * DEPLOYING The CO is currently building the access. The field "connectionDateTime" should be set and reflect the planned date for activation, with a minimum of uncertainty (+/- a few days).
 * PASSED The accesss is close to the built out network of the CO. For an SDU address the could be ducts waiting in the street. For an MDU address the appartment might not have been connected, e.g. if a tenant refuse to allow access.  
 * CONNECTED The access is operational and services may be sold freely. If a new CO CPE is required, this should be reflected in the field "availableDateTime" being the needed days in the future. 
 * DISCONNECTED The access has been disconnected from the COs network.
 * INMIGRATION The access is in the process of being migrated into the COs network. The field "connectionDateTime" should be set and reflect the planned date for activation with a minimum of uncertainty (+/- 1-2 days). The access should be freezed during the migration. Orders with delivery date after "availableDateTime" might be accepted, but there is a risk that all services to be migrated are not yet created. 
 * OUTMIGRATION The access is in the process of being migrated out of the COs network. The field "disconnectionDateTime" should be set and reflect the planned date for deactivation with a minimum of uncertainty (+/- 1-2 days). The access should be freezed during the migration. Orders should not be accepted on the access.


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

### subscriptions
List of subscriptions on this access. Same format as the result of the [subscriptions API](subscriptions.md) except
for the accessId that can be omitted here. If there are no subscription for this access an empty JSON array is returned.

 * Data format: [see subscriptions](subscriptions.md)
 * Mandatory
 * Available with single access
