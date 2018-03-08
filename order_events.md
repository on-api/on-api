# Order Events API

Vid orderläggning i API kan kommunikationsoperatören svara med state `RECEIVED`. Det betyder att tjänsteleverantören skall fråga regelbundet om ordern status.

Order Event API erbjuder möjlighet att fråga om alla nya Order Event sedan senaste anrop. Så att Tjänsteleverantören kan ställa en fråga för status på alla utestående ordrar. På det viset kan intervallet mellan statushämtningar minskas och kunden får sina tjänster aktiverade snabbare.

API:et används enbart då en orderläggning resulterar i state `RECEIVED`.

Fälten beskrivs i <a href="service_activation.md">Service Activation API</a>.

## Exempel: Hämtning av nya events

Request:
```http
GET /api/2.3/orderevents/?since=cc537e54-e59c-11e3-a593-3c970e806452 HTTP/1.1
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

[
    {
        "event": "2a6d6432-e59d-11e3-9a52-3c970e806452",
        "order": {
            "path": "/api/2.3/orders/ec4bc754-6a30-11e2-a585-4fc569183061",
            "accessId": "STTA0001",
            "service": "BB-100-10",
            "operation": "DEACTIVATE",
            "state": "DONE_SUCCESS",
            "message": ""
        }
    },
    {
        "event": "251825a8-e59d-11e3-bf71-3c970e806452",
        "order": {
            "path": "/api/2.3/orders/3393123a-e59f-11e3-9371-3c970e806452",
            "accessId": "STTA0002",
            "service": "BB-100-10",
            "operation": "ACTIVATE",
            "state": "DONE_FAILED",
            "message": "Port is too busy for you. You can't handle the truth!"
        }
    }
 ]
```

Anropet skall returnera samtliga events som skett sedan Eventet `since`.
Event som `since` avser skall inte ingå i svaret.

Listan är oföränderlig. Vid två tidpunkter, t1 och t2, där t2 inträffar efter t1, skall tjänstens svar vid t2 alltid omfatta hela t1. Svaret kan alltså enbart växa, inte förändras.

Av denna anledningen är det viktigt att tjänstens svar inte är en projektion på ordrar, som kan ändra status, utan är baserad på oföränderliga events.

`event` skall vara unikt över alla events tjänsten har returnerat.
Det måste inte vara ett UUID, utan KO kan bestämma innehållet så länge det är unikt.

Listan över events skall vara stigande i kronologisk ordning (senaste eventet sist). Tjänsteleverantören skall att använda det sista lästa eventet som `since`-parameter i nästföljande anrop.

Enbart order-event av typen order.event `DONE_SUCCESS` eller `DONE_FAILED` får förekomma.

## Exempel: Hämtning av alla events

Request:
```http
GET /api/2.3/orderevents/ HTTP/1.1
```

Response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

[
    {
        "event": "251825a8-e59d-11e3-bf71-3c970e806452",
        "order": {
            "path": "/api/2.3/orders/3393123a-e59f-11e3-9371-3c970e806452",
            "accessId": "STTA0002",
            "service": "BB-100-10",
            "operation": "ACTIVATE",
            "state": "DONE_FAILED",
            "message": "Port is too busy for you. You can't handle the truth!"
        }
    },
    ...
]
```

Om ingen _since_ parameter skickas med i anropet skall _samtliga_ events returneras.
