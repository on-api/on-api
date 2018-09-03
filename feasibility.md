# Feasibility API

Feasibility is used to find accesses and to determine the connection status of houses and apartments. It also shows a list of services that can potentially be ordered on each access and its commercial circumstances.

## Example

Request:
```http
GET /api/2.3/accesses/ HTTP/1.1
```

Response:
```http
HTTP/1.1 200 OK
Last-Modified: Fri, 31 Aug 2012 12:03:28 GMT
Content-Type: application/json
[
    {
        "accessId": "STTA0001",
        "streetName": "Testvägen",
        "streetNumber": "100",
        "streetLittera": "",
        "postalCode": "10000",
        "city": "Teststad",
        "countryCode": "SE",
        "premisesType": "MDU_APARTMENT",
        "mduApartmentNumber": "1001",
        "mduDistinguisher": "12121212",
        "outlet": "A-11-14",
        "population": "Testpopulation",
        "networkAgreement": "NOT_REQUIRED",
        "services": [
            {
                "service": "BB-100-100",
                "startDate": "2017-02-10",
                "endDate": ""
            }, {
                "service": "BB-100-10",
                "startDate": "2017-02-10",
                "endDate": ""
            }, {
                "service": "BB-10-10",
                "startDate": "2015-10-12",
                "endDate": "2019-03-01"
            }, {
                "service": "IPTV",
                "startDate": "2015-10-12",
                "endDate": ""
            }, {
                "service": "VOIP",
                "startDate": "2015-10-12",
                "endDate": ""
            }
        ],
        "cpe": {
            "coCpe": "MODEL X",
            "servicePort": "FREE_SEATING"
        },
        "accessStatus": {
            "startDate": "2015-08-01",
            "endDate": "",
            "sellable": "YES",
            "status": "CONNECTED",
            "deliveryPoint": "APARTMENT"
        }
    }
]
```

## Data fields

* `null` is not a valid value for any field
* Mandatory fields cannot be empty string ("")

<table>
  <tbody>
  <tr>
    <td><strong>Field</stong></td>
    <td><strong>Mandatory</stong></td>
    <td><strong>Sample(s)</stong></td>
    <td><strong>Explanation</stong></td>
  </tr>
  <tr>
    <td>accessId</td>
    <td>YES</td>
    <td>123456<br>ADA1343-12</td>
    <td>One, per communication operator, unique ID for an access.<br> May only consist of a-z, A-Z , 0-9, '-' and '.'. [a-zA-Z0-9-.]+. Max length 32 characters.</td>
  </tr>
  <tr>
    <td>streetName</td>
    <td>YES</td>
    <td>Kungsgatan</td>
    <td>Street name<br> Exclude street number or street littera. In the example of "Kungsgatan 10G", the street name is "Kungsgatan".</td>
  </tr>
  <tr>
    <td>streetNumber</td>
    <td>NO</td>
    <td>10</td>
    <td>Street number<br> May only consist of digits.<br> In the example of "Kungsgatan 10G", the street number is "10". In the example of "Lantvägen 550-70", the street number is "550".</td>
  </tr>
  <tr>
    <td>streetLittera</td>
    <td>NO</td>
    <td>G</td>
    <td>Street littera/Entrance<br> In the example of "Kungsgatan 10G", the street littera is "G". In the example of "Lantvägen 550-70", the street littera is "70".</td>
  </tr>
  <tr>
    <td>postalCode</td>
    <td>YES</td>
    <td>41369</td>
    <td>Postal code<br> Must be a 5 digits value between 10000 and 99999.</td>
  </tr>
  <tr>
    <td>city</td>
    <td>YES</td>
    <td>Göteborg</td>
    <td>Postal city</td>
  </tr>
  <tr>
    <td>countryCode</td>
    <td>YES</td>
    <td>SE</td>
    <td>Country code according to the ISO 3166-1 alpha-2 standard</td>
  </tr>
  <tr>
    <td>premisesType</td>
    <td>YES</td>
    <td>
        <dl>
            <dt>MDU_APARTMENT</dt>
                <dd>Apartment in apartment building (Multiple Dwelling Units). Same cadastral reference.</dd>
            <dt>MDU_COMMON</dt>
                <dd>Common space i apartment building. Same cadastral reference.</dd>
            <dt>RESIDENTIAL_HOUSE</dt>
                <dd>Free-standing residential building with its own cadastral reference.</dd>
            <dt>COMMERCIAL</dt>
                <dd>Commercial premises with no public access, e.g. an office.</dd>
            <dt>PUBLIC</dt>
                <dd>Public premises with public access, e.g. a restaurant or health center.</dd>
            <dt>UNKNOWN</dt>
                <dd>Unknown premises</dd>
        </dl>
    </td>
    <td>Premises type describes the type of building/premises of the access.<br> If premises type is MDU_APARTMENT or MDU_COMMON, either MduDistinguisher or MduApartmentNumber must be provided to be able to distinguish between individual accesses.</td>
  </tr>
  <tr>
    <td>mduApartmentNumber</td>
    <td>YES*</td>
    <td>1101</td>
    <td>Apartment number must be a 4 digits value according to the specification of Lantmäteriet. Used to distinguish between individual accesses in apartment blocks.<br>
    (*) If premises type is `MDU_APARTMENT` or `MDU_COMMON`, either `MduDistinguisher` or `MduApartmentNumber` must be provided.</td>
  </tr>
  <tr>
    <td>mduDistinguisher</td>
    <td>YES*</td>
    <td>28<br>65113<br>1234-1919</td>
    <td>Alternative identification of the access used to distinguish between individual accesses in apartment blocks. This field does not need to follow the specification of Lantmäteriet.<br>
    (*) If premises type is `MDU_APARTMENT` or `MDU_COMMON`, either `MduDistinguisher` or `MduApartmentNumber` must be provided.</td>
  </tr>
  <tr>
    <td>outlet</td>
    <td>NO</td>
    <td>A-11-14</td>
    <td>Outlet number identifies the port in the apartment or house. The port is typically labeled with this number. If specified, it should be unique per address.</td>
  </tr>
  <tr>
    <td>population</td>
    <td>NO</td>
    <td>Hemsöhem</td>
    <td>Describes a subset of all accesses. Used for grouping accesses together for commercial purposes.</td>
  </tr>
  <tr>
    <td>networkAgreement</td>
    <td>YES</td>
    <td>NOT_REQUIRED<br>REQUIRED<br>EXISTS</td>
    <td>Indicates if a network agreement is required between the communication operator and the end customer. Used to determine the commercial circumstances of the access.</td>
  </tr>
  <tr>
    <td>services</td>
    <td>YES</td>
    <td></td>
    <td>Lists services that could potentially be delivered on the access and may also show the first and last date a service is available for ordering.<br>
    To determine if a service can actually be activated on a specific access and date, the service provider performs an availability on the access.</td>
  </tr>
  <tr>
    <td>services / service</td>
    <td>YES</td>
    <td>BB-100-100<br>IPTV<br>VOIP</td>
    <td>Id or name of the service. Used to identify the service when ordering.</td>
  </tr>
  <tr>
    <td>services / startDate</td>
    <td>NO</td>
    <td>2017-02-10</td>
    <td>Indicates the date when a service can be activated for the first time when introducing new services. Dates must be specified according to ISO-8601 (YYYY-MM-DD). Empty value means that activation is possible at any time.</td>
  </tr>
  <tr>
    <td>services / endDate</td>
    <td>NO</td>
    <td>2019-01-01</td>
    <td>Indicates the date when a service can be activated for the last time when phasing out services. Dates must be specified according to ISO-8601 (YYYY-MM-DD). Empty value means that no end date is set for this service.</td>
  </tr>
  <tr>
    <td>cpe</td>
    <td>YES</td>
    <td></td>
    <td>Shows information about the CPE installed on an access. Only be used if CPE is provided by the communication operator.</td>
  </tr>
  <tr>
    <td>cpe / coCpe</td>
    <td>NO</td>
    <td>NETGEAR WNDR4000</td>
    <td>Type of CPE installed on access (vendor, model).</td>
  </tr>
  <tr>
    <td>cpe / servicePort</td>
    <td>NO</td>
    <td>PORT FORWARDING<br>FREE_SEATING</td>
    <td>Indicates if services are delivered port mapped or allows free seating.</td>
  </tr>
  <tr>
    <td>accessStatus</td>
    <td>YES</td>
    <td></td>
    <td>Shows information about the overall status of an access, e.g. if services can be sold and when the access is available for the first time.</td>
  </tr>
  <tr>
    <td>accessStatus / startDate</td>
    <td>NO</td>
    <td>2017-01-01<br>2017-01-01-2017-03-01</td>
    <td>Indicates the date, or between two dates, when an access will be activated for ordering for the first time when adding new accesses. Dates must be specified according to ISO-8601 (YYYY-MM-DD). Empty value means that access is active.</td>
  </tr>
  <tr>
    <td>accessStatus / endDate</td>
    <td>NO</td>
    <td>2017-01-01<br>2017-01-01-2017-03-01</td>
    <td>Indicates the date, or between two dates, when an access will be unavailable for ordering when removing accesses. Dates must be specified according to ISO-8601 (YYYY-MM-DD). Empty value means that no end date is set for this access.</td>
  </tr>
  <tr>
    <td>accessStatus / sellable</td>
    <td>YES</td>
    <td>YES<br>NO</td>
    <td>Indicates if services are allowed to be sold on the access.</td>
  </tr>
  <tr>
    <td>accessStatus / status</td>
    <td>YES</td>
    <td>
        <dl>
            <dt>PLANNED</dt>
                <dd>This is a planned access. `startDate` may show the planned activation date.</dd>
            <dt>PASSED</dt>
                <dd>Access is passed.</dd>
            <dt>CONNECTED</dt>
                <dd>Access is connected.</dd>
            <dt>TO_BE_DISCONNECTED</dt>
                <dd>Access is about to be disconnected. `endDate` may show the disconnection date.</dd>
            <dt>DISCONNECTED</dt>
                <dd>Access is disconnected.</dd>
        </dl>
    </td>
    <td>The connection status of the access.</td>
  </tr>
  <tr>
    <td>accessStatus / deliveryPoint</td>
    <td>YES</td>
    <td>APARTMENT<br>BUILDING<br>NODE</td>
    <td>The type of delivery point for services to this access.</td>
  </tr>
  </tbody>
</table>

## Limiting mechanism

If-Modified-Since is used to request incremental updates of accesses. Used to receive only changed accesses since last request, hence saving bandwidth and improving performance.

In the first request, no limitation is performed. The service provider requests all accesses. In subsequent requests the If-Modified-Since header is applied, and should be the Last-Modified value from last request.

The "Last-Modified" header is Mandatory if HTTP Status 200 OK. HTTP Status 304 Not Modified is returned if nothing has changed since last request.

Se [RFC-2616][rfc2616-sec14]. Exemplen använder ingen autentisering.

```
If-Modified-Since = "If-Modified-Since" ":" HTTP-date
```

When an access is included in the response, it must always be complete with all fields provided. Partial access data are not allowed.

## Limiting mechanism - Example

Example of sequence of requests and responses

Request:
```http
GET /api/2.3/accesses/ HTTP/1.1
```

Response:
```http
HTTP/1.1 200 OK
Last-Modified: Fri, 31 Aug 2012 12:03:28 GMT
Content-Type: application/json
...
```

In the subsequent request "If-Modified-Since"-header is applied to limit the response.

Request:
```http
GET /api/2.3/accesses/ HTTP/1.1
If-Modified-Since: Fri, 31 Aug 2012 12:03:28 GMT
...
```

If there are updated accesses the response may look like this:

Response:
```http
HTTP/1.1 200 OK
Last-Modified: Mon, 03 Sep 2012 09:54:55 GMT
Content-Type: application/json
...
```

If there are no updated accesses the response will look like this:

Response:
```http
HTTP/1.1 304 Not Modified
```

[rfc2616-sec14]: http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html "HTTP/1.1 RFC-2616 Section 14, Header Field Definitions"
