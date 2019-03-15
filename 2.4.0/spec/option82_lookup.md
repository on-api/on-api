# DHCPv4 Option82 Lookup API

## Description

The API enables service providers to lookup **access-id** using the **option82** from the DHCP log.

The DHCPv4 option82 from the DHCP log should be encoded in hex as is, without any parsing, before it is used in the API.

## Specification
Request:
<pre>GET /2.4/option82/<b>&lt;hex-encoded option82&gt;</b></pre>

Response:
<pre>
HTTP/1.1 200 OK
Content-Type: application/json

{
    "accessId": "<b>&lt;access-id&gt;</b>"
}
</pre>


## Example

Request:
```http
GET /api/2.3.1/option82/5216010765746820302F31020B31302E31302E31302E3130
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "accessId": "SMBA0002"
}
```

If no access-id can be found, the response should be `HTTP 404 Not Found`

## Fields
See [data formats](dataformats.md) for specification of option82 and access-id.

