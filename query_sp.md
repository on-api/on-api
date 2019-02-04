# Querying the service provider for service information

This API call is used to fetch the customer information and ordered services _from_ a service provider. The response lists
all ordered services and the related customer information given a specific spReference.

*NB! This API is used in reverse of the other API calls, the SP is the server and the CO is the client.

## Example

Request:
```http
GET /api/2.3.1/services/?spReference=WloKMvmArcCFiV679uhWpAAtNgyvHxma HTTP/1.1
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/x-ldjson

{ "service": "BB-1000-100", "customer": { "name": "John Doe", "email": "john@johndoe.com", "phone": "", "mobilePhone": "" },  "accessId": "STTA0001", "spReference": "WloKMvmArcCFiV679uhWpAAtNgyvHxma" }
{ "service": "IPTV", "customer": { "name": "John Doe", "email": "john@johndoe.com", "phone": "", "mobilePhone": "" },  "accessId": "STTA0001", "spReference": "WloKMvmArcCFiV679uhWpAAtNgyvHxma" }

```



