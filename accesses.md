# Accesses API

The accesses API is used to get available access points. The accesses contains details about the address where the 
access resides, available services, equipment and activated services. 
  
## Operations

### GET

#### All accesses 
```HTTP
accesses/ HTTP/1.1
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
accesses/ HTTP/1.1
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
    "accessId": "STTA0001",
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
    "services": [
      {
        "service": "BB-100-100",
        "connection": "2014-03-01"
      },
      {
        "service": "BB-100-10",
        "connection": "2013-10-12"
      },
      {
        "service": "BB-10-10",
        "connection": "2013-10-12"
      },
      {
        "service": "IPTV",
        "connection": "2013-10-12"
      },
      {
        "service": "VOIP",
        "connection": "2013-08-13"
      }
    ],
    "coFiberConverter": "LASER_3001X_MK2",
    "coCpeSwitch": "",
    "coCpeRouter": "NETGEAR WNDR4000"
  }
]
```


#### Single access

To get a single access use accessId as key. The single access contains details about activated services and the services
 available for activation.
 
Request
```http
GET /onapi/2.4/accesses/STTA0001 HTTP/1.1
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
    "accessId": "STTA0001",
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
    "services": [
        {
            "service": "BB-100-100",
            "connection": "2014-03-01",
            "available": "2014-01-01",
            "forcedTakeoverPossible": false,
            "comments": [
                "Conflicts with other service on this access"
            ]
        }, {
            "service": "BB-100-10",
            "connection": "2013-10-12",
            "available": "YES",
            "forcedTakeoverPossible": false
        }, {
            "service": "BB-10-10",
            "connection": "2013-10-12",
            "available": "YES",
            "forcedTakeoverPossible": false
        }, {
            "service": "IPTV",
            "connection": "2013-10-12",
            "available": "YES",
            "forcedTakeoverPossible": false
        }, {
            "service": "VOIP",
            "connection": "2013-08-13",
            "available": "NO",
            "forcedTakeoverPossible": true
        }
    ],
    "active": [
        {
            "service": "BB-100-10",
            "option82": "5216010765746820302F31020B31302E31302E31302E3130",
            "equipment": [
                { "vendorId" : "CH_BROADBAND" }
            ],
            "spReference": ""
        }, {
            "service": "IPTV",
            "option82": "5216010765746820302F32020B31302E31302E31302E3130",
            "equipment": [],
            "spReference": ""
        }
    ],
    "coFiberConverter": "LASER_3001X_MK2",
    "coCpeSwitch": "",
    "coCpeRouter": "NETGEAR WNDR4000"
}
```

## Fields

Some fields are only available when fetching a single access. These fields are marked with "Available with single access"

 * Null is not a valid value for any field
 * Mandatory fields cannot be empty string ("")

### accessId

Identifies a single access. Used as key when fetching a single accesss and ordering services.

 * Data format: ID
 * Mandatory
 
### streetName

Street name for the address where the access resides.

 * Data format: text
 * Mandatory

### streetNumber

May only consist of digits.
In the example of "Kungsgatan 10G", the street number is "10". In the example of "Lantvägen 550-70", the street number 
is "550".

 * Data format: number
 * Optional

### streetLittera

Street littera or entrance. In the example of "Kungsgatan 10G", the street littera is "G". In the example of 
"Lantvägen 550-70", the street littera is "70".

 * Data format: text
 * Optional
 
### postalCode

 * Mandatory
 * Data format: postalCode
  
### city

 Postal city

 * Data format: text 
 * Mandatory
 
### countryCode

 * Data format: countryCode
 * Mandatory

### premisesType

Premises type describes the type of building/premises of the access.

 * Data format: enumeration
 * Mandatory
 
**Possible values**
 * COMMERCIAL Offices, stores, municipalty buildings
 * MDU_APARTMENT Apartment in a apartment building (multi dwelling unit)
 * MDU_COMMON  Common area in a apartment building (multi dwelling unit)
 * MDU_TECHNICAL Machine room or space intended for technical equipment
 * PUBLIC Location where the public has access
 * RESIDENTIAL_HOUSE Single family house (single dwelling unit)
 * UNKNOWN Unknown, preferably not used

### mduApartmentNumber

Used to distinguish between individual apartments in apartment buildings sharing a single postal address.

 * Data format: number
 * Four digits
 * Matching regexp ^[0-9]{4}$
 * See [Lantmäteriet Apartmentnumber](https://www.lantmateriet.se/en/real-property/Fastighetsinformation/Lagenhetsregistret/apartment-register-content/)
 * Mandatory if premisesType is set to MDU_APARTMENT and mduDistinguisher is omitted

### mduDistinguisher

Alternative to mduApartmentnumber used to distinguish between individual apartments in an apartment building sharing a
single postal address. 

 * Data format: text
 * Mandatory if premisesType is set to MDU_APARTMENT and mduApartmentNumber is omitted

### outlet

Used to identify the port in the apartment or house. The port is typically labeled with this value. If specified, 
it should be unique per address.

 * Data format: text
 * Optional

### population

Describes a subset of all accesses. Used for grouping accesses together for commercial or technical purposes.

 * Data format: text
 * Optional

### services 
Lists of deliverable services.

 * Data format: array of objects

### services/service

Name of the service, used as reference in the [order API](order.md)

 * Data format: text
 * Mandatory

### services/connection 

Indicates when the service is technically deliverable for the first time. If the date is unknown "YES" or "NO" can 
optionally be used as value.

 * Data format: date (Valid values are also "YES" and "NO")
 * Mandatory

### services/available

Specifies when a service is available for order. If the date is unknown "YES" or "NO" can optionally be used as value. 
 
 * Data format: date (Valid values are also "YES" and "NO")
 * Mandatory
 * Available with single access

### services/forcedTakeoverPossible

Specifies if a service provider can replace another service providers activated service. 

 * Data format: boolean
 * Mandatory

### services/comments

A list of messages intended for the end customer. 

 * Data format: array of text
 * Optional 

### active
List of services that are already activated on the access for the current Service Provider. 

 * Data format: array of objects containing active services
 * Mandatory
 * Available with single access

### active/service
 * Data format: 
 * Mandatory

### active/option82
 * Data format: 
 * Mandatory
 * Available with single access

### active/equipment
 * Data format: 
 * Mandatory
 * Available with single access

### active/spReference 
 * Data format: ID
 * Mandatory
 * Available with single access

Provides references that identifies the unique end-customer or service in the Service Provider's system.
This information can be used by the CO to lookup information about the customer or service on demand. 
See Service Activation for more information.

### active/spSubscriptionId 
 * Data format: ID
 * Optional
 * Available with single access

 Unique ID in the SP-system for the service/subscription.

### active/coSubscriptionId
 * Data format: ID
 * Mandatory
 * Available with single access

 For the current communications operator unique ID for the active service.

### active/characteristics
 Characteristics for the service such as SLA or fixed IP addresses.
 
 * Data format: object
 * Optional

### coFiberConverter
 * Data format: text
 * Optional

### coCpeSwitch
 * Data format: text
 * Optional

### coCpeRouter
 * Data format: text
 * Optional
