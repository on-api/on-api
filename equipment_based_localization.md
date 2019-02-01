# Equipment based localization
## Description
In some scenarios, it is difficult to determine what accessid to use when ordering a service for an end user.

In these scenarios the possibility it is beneficial if the communication operator can inform the service provider where in the network the end users show up.
Then the service provider can order the service to the access where the end user shows up.

There are two parts of the API. In the first the service provider registers Vendors ID's (DHCPv4 option60) or MAC addresses.
Secondly, whenever a client that matches either the MAC address or the VendorID, the communication provider notifies the service provider.
The service provider can then use the order API to order a service to the accessID where the client showed up. 

## APIs
* Registration
  * [Register Vendor IDs](#register-vendor-ids)
  * [Unregister Vendor IDs](#unregister-vendor-ids)
  * [Register MAC addresses](#register-mac-addresses)
  * [Unregister MAC addresses](#unregister-mac-addresses)
* [Notification](#notification)


## Register Vendor IDs

***Request***

The service provider register the vendorIDs (DHCP option 60) of interest using this API. 

When equipment with a matching vendorID is found by the communication operator, the [Notification API](#notification) is used to notify the service provider.    

```html
POST /ebl/vendorids
{
    vendorids: [{"vendorid":"sp_specific",
                 "match_type: "partial_match"}]
}
```
The vendorID **MUST** be specific to the service provider. A generic vendor ID may not be used. 
See the [fields](#fields) section for the description of the fields.

***Response***
* `201 Created`
* `400 Bad Request`

The response should contain a Json structure with the added vendorids. If no vendorID was added then `vendorids` should be an empty list.
The format is the same as in the request.


## Unregister Vendor IDs

This API is used by the service provider to remove VendorIDs from the communication operator, so that they do not generate any notifiactions any more.

***Request***

```html
DELETE /ebl/vendorids
{
    vendorids: [{"vendorid":"sp_specific"}]
}
```
See the [fields](#fields) section for a description of the fields.

***Response***
* `200 OK`
* `400 Bad Request`
* `404 Not Found`
* `409 Conflict`


The response should contain a Json structure with the removed vendorIDs. If no VendorID was removed, the `vendorids` list should be an empty list.
The format for the JSON is the same as in the request.


## Register MAC addresses

The service provider register the MAC address of interest using this API.

When equipment with a matching MAC address is found by the communication operator, the [Notification API](#notification) is used to notify the service provider.    

***Request***

```html
POST /ebl/mac-addresses
{
    macs: [
            {"mac":"11:22:33:44:55:66",
             "delete_on_match": "true",
             "valid_until": "2019-04-15T00:00:00.000Z"}
          ]
}
```

See the [fields](#fields) section for a description of the fields.

***Response***
* `201 Created`
* `400 Bad Request`

The response should contain a Json structure with the added mac adresses. If no mac address is added then `macs` should be an empty list.
The format is the same as in the request.

The response should set the values `delete_on_match` and `valid_until` to actual value.

## Unregister MAC addresses

This API is used by the service provider to remove MAC addresses from the communication operator, so that they do not generate any notifiactions any more.

***Request***

```html
DELETE /ebl/mac-addresses
{
    macs: [{"mac":"11:22:33:44:55:66"}]
}
```

***Response***
* `200 OK`
* `400 Bad Request`
* `404 Not Found`
* `409 Conflict`

The response should contain a Json structure with the removed MAC addresses. If no MAC address was removed, the `macs` list should be an empty list.
The format for the JSON is the same as in the request.


## Notification
As soon as the Communication provider in some way discover any client matching either a vendorID or a MAC address, the communication operator should notify the service provider using this API.

How the client is discovered is not part of this API. It might be through analysis of DHCP or Radius logs, integration towards the DHCP server or any other means.

*Note*:<br/>
The Service provider hosts the notification API, and the communication provider calls it.

***Request***

```html
POST /ebl/notification

{
    "mac":"11:22:33:44:55:66",
    "accessID": "abc123",
    "vendorID": "sp_rgw_01",
    "timestamp": "2019-02-01T13:05:23.234Z"
}
```

See the [fields](#fields) section for a description of the fields.


***Response***
* `200 OK`


## Fields
**Registration & unregistration**
<table>
    <thead>
        <tr>
            <th>Field</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><b>vendorids</b></td>
            <td><p>List of Vendor IDs to be matched.</p></td>
        </tr>
        <tr>
            <td>vendorid</td>
            <td>
                <p>The vendorID to match against the DHCP Vendor ID (DHCP option 60)</p>
                <p>Text, max length 255 characters.</p>
            </td>
        </tr>
        <tr>
            <td>match_type</td>
            <td>
                <p>One of <code>partial_match</code> and <code>exact</code>.</p>
                <p>If partial_match is used, matching from left to right should be used.
                If exact match is used, the complete vendorID should match.
                There is no support for wildcards regular expressions.</p>
            </td>
        </tr>
        <tr>
            <td><b>macs</b></td>
            <td><p>List of MAC address objects to be matched.</p></td>
        </tr>
        <tr>
            <td>mac</td>            
            <td>
                <p>
                    The MAC address that should trigger a notification to the service provider.
                </p>
                <p>
                    The dataformat is MAC address as described in <a href="dataformats.md">dataformats.md</a>
                </p>
            </td>
        </tr>
        <tr>
            <td>delete_on_match</td>
            <td>
                <p>One of <code>true</code> and <code>false</code></p>
                <p>
                    If the <code>delete_on_match</code> flag is set to true, the MAC address should only generate *one* notification to the service provider.
                </p>
                <p>
                    If the flag is set to false, a notification is sent to the service provider every time the communication provider identified the MAC address.
                </p> 
           </td>
        </tr>
        <tr>
            <td>valid_until</td>
            <td>
                <p>
                    After <code>valid_until</code> no notifications should be sent to the service provider regarding the specific MAC address. 
                </p>
                <p>
                    The dataformat is dateTime, described in <a href="dataformats.md">dataformats.md</a>
                </p>
            </td>
        </tr>
    </tbody>
</table>

**Notification**

<table>
    <thead>
        <tr>
            <th>Field</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>mac</td>
            <td>
                <p>
                    The MAC address of the client that triggered the notification.
                </p>
                <p>
                    The dataformat is MAC address as described in <a href="dataformats.md">dataformats.md</a>
                </p>
            </td>
        </tr>
        <tr>
            <td>accessID</td>
            <td>
            <p>The accessID of the access where the  client was discovered.</p>
			<p>See accessID in <a href="dataformats.md">dataformats</a></p>
            </td>
        </tr>
        <tr>
            <td>vendorID</td>
            <td>
                <p>If available; the complete vendorID of the client.</p>
                <p>If not available; this field is represented by an empty string</p>
                <p>Dataformat is text, max 255 characters.</p>
            </td>
        </tr>
        <tr>
            <td>timestamp</td>
            <td>
                <p>Timestamp of when the client was discoverd</p>
                <p>The dataformat is dateTime, described in <a href="dataformats.md">dataformats.md</a></p>
            </td>
        </tr>
    </tbody>
</table>

