# API: Alla aktiva tjänster

Syftet med API är att låta TL hämta en förteckning över alla sina aktiva tjänster från KO.

## Exempel

Request:
```http
GET /api/2.3/services/
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/x-ldjson

{ "service": "BB-1000-100", "accessId": "STTA0001", "spReference": "WloKMvmArcCFiV679uhWpAAtNgyvHxma" }
{ "service": "IPTV", "accessId": "STTA0001", "spReference": "WloKMvmArcCFiV679uhWpAAtNgyvHxma" }

```

