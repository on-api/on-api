# Availability API

Availability is used to query a single access. It returns the same information as the Feasibility, but also adds information about active services and evaluates if services can actually be delivered at current time. It is typically used prior to ordering to ensure a service can be activated.

### Example

Request:
```http
GET /api/2.3/accesses/STTA0001 HTTP/1.1
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

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
            "endDate": "",
            "available": "NO",
            "deliveryDate": "",
            "deliveryDays": "0",
            "forcedTakeoverPossible": false,
            "reasons": [
                {
                    "Conflicts with other service on this access"
                }
            ]
        }, {
            "service": "BB-100-10",
            "startDate": "2017-02-10",
            "endDate": "",
            "available": "NO",
            "deliveryDate": "",
            "deliveryDays": "0",
            "forcedTakeoverPossible": false,
            "reasons": [
                {
                    "Conflicts with other service on this access"
                }
            ]
        }, {
            "service": "BB-10-10",
            "startDate": "2015-10-12",
            "endDate": "2019-03-01",
            "available": "NO",
            "deliveryDate": "",
            "deliveryDays": "0",
            "forcedTakeoverPossible": false,
            "reasons": [
                {
                    "Conflicts with other service on this access"
                }
            ]
        }, {
            "service": "IPTV",
            "startDate": "2015-10-12",
            "endDate": "",
            "available": "NO",
            "deliveryDate": "",
            "deliveryDays": "0",
            "forcedTakeoverPossible": false,
            "reasons": [
                {
                    "Conflicts with other service on this access"
                }
            ]
        }, {
            "service": "VOIP",
            "startDate": "2015-10-12",
            "endDate": "",
            "available": "YES",
            "deliveryDate": "2018-08-25",
            "deliveryDays": "3",
            "forcedTakeoverPossible": false,
            "reasons": []
        }
    ],
    "active": [
        {
            "service": "BB-100-10",
            "coSubscriptionId": "76541",
            "dhcpOption": 
                {
                    "circuitId": "",
                    "remoteId": "",
                    "interfaceId": ""
                },
            "equipment": [
                { "vendorId" : "CH_BROADBAND" }
            ],
            "spReference": {
                "customer": "124679",
                "subscription": "3564576"
            }
        }, {
            "service": "IPTV",
            "coSubscriptionId": "83718",
            "dhcpOption": 
                {
                    "circuitId": "",
                    "remoteId": "",
                    "interfaceId": ""
                },
            "equipment": [],
            "spReference": {
                "customer": "124679",
                "subscription": "3564855"
            }
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
```

## Data fields

This list shows additional fields and differences in the description of a field in the Availability, which are not already described in the <a href="feasibility.md">Feasibility</a>.

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
            <td>services</td>
            <td>YES</td>
            <td></td>
            <td>Lists services that could potentially be delivered on the access.<br>
            In contrast to the Feasibility, this list includes if a service can actually be activated on the specific access and date.</td>
        </tr>
        <tr>
            <td>services / available</td>
            <td>YES</td>
            <td>YES<br>NO</td>
            <td>
                Indicate if the service is available for activation on the specified date. If NO, <code>deliveryDate</code> may indicate the earliest possible date when the delivery of the service can be fully completed.<br>
                If the service can not be delivered on the specified date but on a future date, <code>available</code> should be NO and <code>deliveryDate</code> should show the future date.
            </td>
        </tr>
        <tr>
            <td>services / deliveryDate</td>
            <td>NO</td>
            <td>2018-08-25</td>
            <td>
                The first possible date when the delivery of the service can be fully completed.<br>
                If the service can not be delivered on the specified date but on a future date, <code>available</code> should be NO and <code>deliveryDate</code> should show the future date.
            </td>
        </tr>
        <tr>
            <td>services / deliveryDays</td>
            <td>NO</td>
            <td>3</td>
            <td>
                Number of days required to fully deliver this service. This is typically used if a service can not be instantly activated because other delivery activaties are needed.<br>
                In the example of 3 deliveryDays, this effectively means that the earliest possible <code>deliveryDate</code> is three days in future assumed that order is received today.
            </td>
        </tr>
        <tr>
            <td>services / forcedTakeoverPossible</td>
            <td>YES</td>
            <td>YES<br>NO</td>
            <td>
                Indicates if "force takeover" is supported on this service. If YES, the "forcedTakeover" flag can be set when ordering to inform the CO that a service from other Service Provider should be disconnected and replaced.<br>
                If "forced takeover" is not supported this flag should be NO.
            </td>
        </tr>
        <tr>
            <td>services / reasons</td>
            <td>YES</td>
            <td></td>
            <td>
                List of reasons for why a service is not available.
            </td>
        </tr>
        <tr>
            <td>active</td>
            <td>YES</td>
            <td></td>
            <td>
                List of services that are already activated on the access for the current Service Provider.
            </td>
        </tr>
        <tr>
            <td>active / service</td>
            <td>YES</td>
            <td>BB-100-100<br>IPTV<br>VOIP</td>            
            <td>Id or name of the service. Used to identify the service when ordering.</td>
        </tr>
        <tr>
            <td>active / coSubscriptionId</td>
            <td>YES</td>
            <td>83718<br>S-83718</td>
            <td>
                Unique ID in the CO-system for the service/subscription.<br> May only consist of a-z, A-Z , 0-9, '-' and '.'. Max length 32 characters.<br>
                This ID is required when deactivating a service when there are multiple subscriptions of this service.
            </td>
        </tr>
        <tr>
            <td>dhcpOption</td>
            <td>YES</td>
            <td></td>
            <td>
                Provides DHCP option information, which may be required by the Service Provider to correlate a DHCP request with the access and service.<br>
                Typically used by DHCP, Radius or TR69-servers to find access specific information.
            </td>
        </tr>
        <tr>
            <td>dhcpOption / circuitId</td>
            <td>NO</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>dhcpOption / remoteId</td>
            <td>NO</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>dhcpOption / interfaceId</td>
            <td>NO</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>active / equipment</td>
            <td>YES</td>
            <td></td>
            <td>
                List of devices that the Service Provider has provided for the service<br>
                See <a href="order.md">Service Activation</a> for more information.
            </td>
        </tr>
        <tr>
            <td>spReference</td>
            <td>NO</td>
            <td></td>            
            <td>
                Provides references that identifies the unique end-customer or service in the Service Provider's system.<br>
                This information can be used by the CO to lookup information about the customer or service on demand.
                See <a href="order.md">Service Activation</a> for more information.
            </td>
        </tr>
        <tr>
            <td>spReference / customer</td>
            <td>NO</td>
            <td>124679<br>C-124679</td>            
            <td>
                Unique ID in the SP-system for the end-customer behind the service.<br> May only consist of a-z, A-Z , 0-9, '-' and '.'. Max length 32 characters.<br>
            </td>
        </tr>
        <tr>
            <td>spReference / subscription</td>
            <td>NO</td>
            <td>3564576<br>S-3564576</td>            
            <td>
                Unique ID in the SP-system for the service/subscription.<br> May only consist of a-z, A-Z , 0-9, '-' and '.'. Max length 32 characters.<br>
            </td>
        </tr>
    </tbody>
</table>
