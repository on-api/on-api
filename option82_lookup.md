# Option82 Lookup API

För att stöda utrustningsbaserad autoaktivering behöver Tjänsteleverantör kunna slå upp vilken Access ett Option82-värde avser.

Tjänsteleverantör samlar in DHCP-loggar med MAC-adress och Option82 (port). På så vis kan TL avgöra vilken port en kund är inkopplad i. För att kunna fortsätta aktiveringsprocessen och beställa tjänster på rätt port (via Access) behöver TL kunna avgöra vilket AccessId som hör till en given port.

Beroende på hur stadsnätet förmedlar loggar till Tjänsteleverantör kommer TL att skicka anrop med olika suboptions.

Om DHCP-loggen enbart innehåller RemoteId, kommer anropet enbart innehålla RemoteId, och vice versa.

## Exempel: Uppslagning av Option82 som hittas.

Request:
```http
GET /api/2.3/option82/5216010765746820302F31020B31302E31302E31302E3130 HTTP/1.1
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "accessId": "SMBA0002"
}
```

Option82 är case-insensitive.

## Exempel: Uppslagning av Option82 som inte hittas.

Request:
```http
GET /api/2.3/option82/5216010765746820302F31020B31302E31302E31302E3130 HTTP/1.1
```

Response:
```http
HTTP/1.1 404 Not Found
```
