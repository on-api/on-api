
# Contact information to end user
## Description
The API enables communication providers to query the service provider for contact details to the end users.

***Note:*** This API is hosted by the service provider, and the communication provider is the client.

## Specification

There are two end points:
* /2.4/access/access-id
  - Uses access-id as input
* /2.4/access_sp_ref/{spReference}
  - Uses the spReference value supplied by the service provider as input
* /2.4/access_sp_sub_id/{spSubscriptionId}
* /2.4/access_sp_ticket_ref/{spTicketReference}

 
It is possible to `POST` a Json structure containing reference to ticket id's.
The rationale is to be able to track requests of contact information.
 

Request:
```http
GET /2.4/access/{ accessId }

GET /2.4/access_sp_ref/{ spReference }

GET /2.4/access_sp_sub_id/{ spSubscriptionId }

GET /2.4/access_sp_ticket_ref/{ spTicketReference }

POST /2.4/access/{ accessId }
Content-Type: application/json

{
    "koTicketReference": "Reference to a ticket at the Communication provider",
    "spTicketReference": "Reference to a ticket at the Servier provider",
    "reason": "Reason for request"
}
```

```http
POST /2.4/access_sp_ref/spReference
Content-Type: application/json

{
    "koTicketReference": "Reference to a ticket at the Communication provider",
    "spTicketReference": "Reference to a ticket at the Servier provider",
    "reason": "Reason for request"
}
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "service": {
        "customer": {
            "name": "Name of contact person",
            "email": "e-mail to contact person",
            "phone": "phone to contact person",
            "mobilePhone": "phone to contact person"
        },
        "spReference": "spReference",
        "accessId": "access-id" 
    }
}
```

If no contact person can be found, the response should be `HTTP 404 Not Found`


## Example
Request:
```http
GET /2.4/access/STTA0001
```

```http
GET /2.4/access_sp_ref/1337
```

```http
POST /2.4/access/STTA0001
Content-Type: application/json

{
    "koTicketReference": "123123",
    "spTicketReference": "123123",
    "reason": "Exchange of CPE required"

}
```
```http
POST /2.4/access_sp_ref/1337 HTTP/1.1
Content-Type: application/json

{
    "koTicketReference": "123123",
    "spTicketReference": "123123",
    "reason": "Exchange of CPE required"
}
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "BB-1000-100": {
        "customer": {
            "name": "Kalle Anka",
            "email": "karl@ankeborg.se",
            "phone": "",
            "mobilePhone": ""
        },
        "spReference": "1337",
        "accessId": "STTA0001" 
    }
}
```
Reference to a ticket at the Communication provider
Reference to a ticket at the Server provider
Reason for request
Uses access-id as input
Uses the spReference value supplied by the service provider as input

## Fields

For data format, see [data formats](dataformats.md)

Request

<table>
    <thead>
        <tr>
            <th>Field</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <code>access-id</code>
            </td>
            <td>
                <p>The access-id of the access. </p>
                <p>See <a href=dataformats.md>dataformats</a> for specification</p>
            </td>
        </tr>
        <tr>
            <td>
                <code>spReference</code>
            </td>
            <td>
                <p>The spReference value for the service that the end user is using.</p>
                <p>See <a href=dataformats.md>dataformats</a> for specification</p>
            </td>
        </tr>
        <tr>
            <td>
                <code>koTicketReference</code>
            </td>
            <td>
                <p>Reference number to a ticket in the Communications Providers ticketing system, describing why contact information is required.</p>
                <p>Format is <b>ticketReference</b> as described in <a href=dataformats.md>dataformats</a></p>                
                <p><em>Optional field</em</p>
            </td>
        </tr>
        <tr>
            <td>
                <code>spTicketReference</code>
            </td>
            <td>
                <p>Reference number to a ticket in the Service Providers ticketing system, to be used if the requst of contact information is a result of a support request.</p>
                <p>Format is <b>ticketReference</b> as described in <a href=dataformats.md>dataformats</a></p>                
                <p><em>Optional field</em</p>
            </td>
        </tr>
        <tr>
            <td>
                <code>reason</code>
            </td>
            <td>
                <p>Text describing the reason for the request.</p>
                <p><em>Data format is text, max 256 characters</em></p>
                <p><em>Optional field</em</p>
            </td>
        </tr>
    </tbody>
</table

Response:
<table>
    <thead>
        <tr>
            <th>Field</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <code>service</code>
            </td>
            <td>
                <p>The service that should be active on the access.</p>
                <p><em>Mandatory field</em></p>
            </td>
        </tr>
        <tr>
            <td>
                <code>customer</code>
            </td>
            <td>
                <p>Object representing contact information to the end user or someone appointed by the end-user</p>
                <p><em>Mandatory field</em></p>
            </td>
        </tr>
        <tr>
            <td>
                <code>customer.phone</code>
            </td>
            <td>
                <p>See <a href=dataformats.md>dataformats</a> for specification</p>
                <p><em>Mandatory field</em>. However, the value might be empty</p>
            </td>
        </tr>
        <tr>
            <td>
                <code>customer.mobilePhone</code>
            </td>
            <td>
                <p>See <a href=dataformats.md>dataformats</a> for specification</p>
                <p><em>Mandatory field</em>. However, the value might be empty</p>
            </td>
        </tr>
        <tr>
            <td>
                <code>spReference</code>
            </td>
            <td>
                <p>The spReference value for the service that the end user is using.</p>
                <p>See <a href=dataformats.md>dataformats</a> for specification</p>
                <p><em>Mandatory field</em>.</p>
            </td>
        </tr>
        <tr>
            <td>
                <code>accessId</code>
            </td>
            <td>
                <p>The access-id of the access. </p>
                <p>See <a href=dataformats.md>dataformats</a> for specification</p>
                <p><em>Mandatory field</em>. </p>
            </td>
        </tr>
    </tbody>
</table>



