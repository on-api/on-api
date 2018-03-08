# TL API: Sökning efter beställda tjänster

Syftet med API är att låta KO hämta kundinformation om en access från Tjänsteleverantör.

*OBS! Till skillnad mot andra APIer är KO klient och TL server i detta API.*

## Exempel

Request:
```http
GET /api/2.3/services/?spReference=WloKMvmArcCFiV679uhWpAAtNgyvHxma HTTP/1.1
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/x-ldjson

{ "service": "BB-1000-100", "customer": { "name": "Kalle Anka", "email": "karl@ankeborg.se", "phone": "", "mobilePhone": "" },  "accessId": "STTA0001", "spReference": "WloKMvmArcCFiV679uhWpAAtNgyvHxma" }
{ "service": "IPTV", "customer": { "name": "Kalle Anka", "email": "karl@ankeborg.se", "phone": "", "mobilePhone": "" },  "accessId": "STTA0001", "spReference": "WloKMvmArcCFiV679uhWpAAtNgyvHxma" }

```

APIt erbjuder Kommunikationsoperatör att söka på beställda tjänster hos Tjänsteleverantör.

