# Querying the service provider for service information

This API call is used to fetch the customer information and ordered services _from_ a service provider. The response lists
all ordered services and the related customer information given a specific spReference.

*NB! This API is used in reverse of the other API calls, the SP is the server and the CO is the client.

## Example

Request:
```http
GET /api/2.4/services/?spReference=WloKMvmArcCFiV679uhWpAAtNgyvHxma HTTP/1.1
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/x-ldjson

{ 
  "service": "BB-1000-100", 
  "customer": {
    "name": "John Doe", 
    "email": "john@johndoe.com", 
    "phone": "", "mobilePhone": "" 
  },  
  "accessId": "STTA0001", 
  "spReference": "WloKMvmArcCFiV679uhWpAAtNgyvHxma" 
}
{ 
  "service": "IPTV", 
  "customer": { 
    "name": "John Doe", 
    "email": "john@johndoe.com", 
    "phone": "", 
    "mobilePhone": "" 
  },  
  "accessId": "STTA0001", 
  "spReference": "WloKMvmArcCFiV679uhWpAAtNgyvHxma"
}

```

## Fields

For data format, see [dataformats](dataformats.md)

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
                <code>spReference</code>
            </td>
            <td>
                <p>The spReference value for the service that the end user is using.</p>
                <p>See <a href=dataformats.md>dataformats</a> for specification</p>
            </td>
        </tr>
    </tbody>
</table

Resonse:
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



