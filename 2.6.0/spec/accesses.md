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
    "technicalStartDateTime": "1970-01-01T00:00:00Z",
    "technicalEndDateTime": "2024-12-01T00:00:00Z",
    "commercialStartDateTime": "1970-01-01T00:00:00Z",
    "commercialEndDateTime": "2024-12-01T00:00:00Z",
    "nationalAddressUUID": "1ce88c93-b310-11eb-bdc2-000c29f11131"
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
  "technicalStartDateTime": "1970-01-01T00:00:00Z",
  "technicalEndDateTime": "2024-12-01T00:00:00Z",
  "commercialStartDateTime": "1970-01-01T00:00:00Z",
  "commercialEndDateTime": "2024-12-01T00:00:00Z",
  "nationalAddressUUID": "1ce88c93-b310-11eb-bdc2-000c29f11131"
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

### priceGroup

A price group that this access is a part of. The value must be an integer larger or equal to 0 (unsigned integer). 
The exact meaning and associated price list is defined by CO. 

 * Data format: [enumeration](../common/dataformats.md#enumeration)
 * Mandatory 

### accessState

Describes the current state of whether the access is connected and can be used.

 * Data format: One of PLANNED, DEPLOYING, HOMESPASSED, CONNECTED, DISCONNECTED, INMIGRATION and OUTMIGRATION
 * Mandatory

**Valid values**
 * PLANNED The CO is planning to connect the access in the future. The field "connectionDateTime" may reflect the planned date for activation, with some uncertainty (+/- a week).
 * DEPLOYING The CO is currently building the access. The field "connectionDateTime" should be set and reflect the planned date for activation, with a minimum of uncertainty (+/- a few days).
 * PASSED The accesss is close to the built out network of the CO. For an SDU address the could be ducts waiting in the street. For an MDU address the appartment might not have been connected, e.g. if a tenant refuse to allow access.  
 * CONNECTED The access is operational and services may be sold freely. If a new CO CPE is required, this should be reflected in the field "availableDateTime" being the needed days in the future. 
 * DISCONNECTED The access has been disconnected from the COs network.
 * INMIGRATION The access is in the process of being migrated into the COs network. The field "connectionDateTime" should be set and reflect the planned date for activation with a minimum of uncertainty (+/- 1-2 days). The access should be freezed during the migration. Orders with delivery date after "availableDateTime" might be accepted, but there is a risk that all services to be migrated are not yet created. 
 * OUTMIGRATION The access is in the process of being migrated out of the COs network. The field "disconnectionDateTime" should be set and reflect the planned date for deactivation with a minimum of uncertainty (+/- 1-2 days). The access should be freezed during the migration. Orders should not be accepted on the access.

### technicalStartDateTime

Indicates when the access is technically deliverable for the first time. If you don't have a date when it was connected, you can specify the date as "1990-01-01T00:00:01Z". If you don't know when it will be connected, you can specify the date as "3030-12-12T00:00:01Z" for example.

 * Data format: [ISO 8601 date time](../common/dataformats.md#datetime)
 * Mandatory

### technicalEndDateTime

Indicates when the access is technically deliverable for the last time.

 * Data format: [ISO 8601 date time](../common/dataformats.md#datetime)
 * Optional

### commercialStartDateTime

Indicates when the access is commercially debitable for the first time. If you don't have a date , you can specify the date as "1990-01-01T00:00:01Z". If you don't know when it will be connected, you can specify the date as "3030-12-12T00:00:01Z" for example.

 * Data format: [ISO 8601 date time](../common/dataformats.md#datetime)
 * Mandatory

### commercialEndDateTime

Indicates when the access is commercially debitable for the last time.

 * Data format: [ISO 8601 date time](../common/dataformats.md#datetime)
 * Optional
 
### nationalAddressUUID

Universally Unique Identifier for the property the address belongs to. 
The value may differ from country to country depending on national preferences. 

 * Data format: [text](../common/dataformats.md#text)
 * Sweden: [uuid](../common/dataformats.md#uuid). PTS (The Swedish Post and Telecom Authority) uses the [Lantmäteriet Real Property UUID](https://www.lantmateriet.se/en/geodata/geodata-products/product-list/real-property-information-download/)
 * Optional


